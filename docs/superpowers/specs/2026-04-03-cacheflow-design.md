# Cache Flow — Personal Cash Flow & Budgeting App

## Overview

Single-file (`cacheflow.html`) personal cash flow tracker. No build system, opens directly in a browser. Companion app to [Cache](~/peerloomllc/cache/cache.html) (net worth ledger) — same dark theme and visual design language, fully independent data and encryption.

**Core workflow:** Log in daily, see what's due, mark items paid/received, watch your balance update.

## Architecture

- Single HTML file with inline CSS and JS
- No external dependencies (except Google Fonts for DM Serif Display, DM Mono, DM Sans)
- localStorage persistence with AES-256-GCM encryption
- No server, no build, no frameworks

## Data Model

```json
{
  "balance": 5000.00,
  "recurring": [
    {
      "id": "abc123",
      "name": "Utility - Alabama Power",
      "amount": 325,
      "frequency": "monthly",
      "direction": "expense",
      "nextDue": "2026-04-15",
      "enabled": true,
      "sourceId": "pa16sb5",
      "category": null,
      "_liabId": null
    }
  ],
  "oneoffs": [
    {
      "id": "def456",
      "name": "New tires",
      "amount": 800,
      "direction": "expense",
      "date": "2026-04-10",
      "paid": false
    }
  ],
  "history": [
    {
      "id": "ghi789",
      "name": "Utility - Internet",
      "amount": 110,
      "direction": "expense",
      "paidAt": "2026-04-01T14:30:00Z",
      "recurringId": "a05dvsw"
    }
  ],
  "settings": {
    "currency": "USD"
  },
  "importedAt": null,
  "savedAt": "2026-04-03T12:00:00Z"
}
```

### Field Details

- **balance**: Single checking account balance. "Paid" deducts expenses, "Received" adds income.
- **recurring**: Repeating transactions. `frequency` is one of: `weekly`, `biweekly`, `monthly`, `quarterly`, `annual`. `sourceId` links back to the Cache export `id` for re-import matching. `enabled` allows disabling without deleting.
- **oneoffs**: One-time transactions (expenses or income). `paid` marks completion.
- **history**: Paid/received transactions. Pruned to 30 days on each save. `recurringId` links back to the recurring source if applicable.
- **importedAt**: ISO timestamp of last Cache import, or null. Displayed in settings.

### Transaction Lifecycle

1. **Recurring** transaction exists with `nextDue` date
2. Appears in Transactions feed when within 45-day lookahead
3. User clicks "Paid" / "Received"
4. Balance adjusts (subtract for expense, add for income)
5. Entry moves to `history` with `paidAt` timestamp
6. `nextDue` advances to next occurrence based on `frequency`
7. History entries older than 30 days are pruned on each encrypted save

For **one-offs**: same flow but no recurrence — after "Paid", the item moves to history and that's it.

## Encryption

Independent from Cache — separate password, separate salt, separate localStorage keys.

- **Keys**: `cacheflow-v1-enc` (encrypted payload), `cacheflow-v1-meta` (salt)
- **Algorithm**: AES-256-GCM via Web Crypto API
- **Key derivation**: PBKDF2, 310,000 iterations, SHA-256
- **Salt**: 32 random bytes, stored unencrypted in meta
- **IV**: 12 random bytes, generated fresh on each save
- **Password**: minimum 8 characters, never stored
- **Session key**: CryptoKey held in memory, cleared on lock

### Auto-Lock

- 15-minute idle timeout
- Activity events (mousemove, keydown, click, touchstart) reset timer
- On lock: clear `sessionKey`, clear in-memory data arrays, show lock screen
- Lock screen: password input, "Decrypting..." progress feedback

## Views

### Header

- Left: "Cache *Flow*" (italic accent on "Flow"), subtitle "personal cash flow" in mono uppercase
- Right: current balance display (large serif number, green if positive, red if negative)
- Settings gear icon → opens settings modal
- Lock icon → manual lock

### Tab Navigation

Three tabs: **Dashboard** | **Transactions** | **Forecast**

### Dashboard Tab

**Summary bar** (3-column grid, same as Cache):
- Monthly Income (green)
- Monthly Expenses (red)
- Net Cash Flow (gold if positive, red if negative)

Monthly figures are calculated by normalizing all enabled recurring transactions to their monthly equivalent (weekly x 4.33, biweekly x 2.17, quarterly / 3, annual / 12).

**Upcoming This Week** section:
- Transactions due in the next 7 days
- Each row: name, amount, due date, "Paid"/"Received" button
- Income rows: green left border + subtle green background tint
- Sorted by due date ascending

**Upcoming This Month** section:
- Remaining transactions due this month (after the 7-day window)
- Same row format

**Quick-add** button (bottom of dashboard):
- Expands inline form: name, amount, direction toggle (expense/income), date (defaults to today)
- Creates a one-off transaction

### Transactions Tab

**Single chronological feed** — no separate income/expense sections.

- **45-day lookahead** from today, sorted by due date ascending (today's items at top, furthest dates at bottom)
- Generates instances from recurring transactions by projecting `nextDue` forward based on `frequency`
- Includes one-off transactions within the 45-day window
- **Income rows**: subtle `--accent-glow` background, `--accent` left border
- **Expense rows**: default styling
- Each row shows: name, amount (mono), frequency badge (small uppercase pill), due date
- **"Paid" / "Received" button** on each row
- **Toggle switch** at top: "Show paid (last 30 days)" — off by default
  - When on: paid history entries appear inline by date with strikethrough name, muted colors, "paid [relative date]" badge
- **Add recurring** button → inline form: name, amount, frequency, direction, next due date
- **Click row to expand** → inline edit panel (Cache's entry-card pattern): edit all fields, delete with confirm, enabled toggle

### Forecast Tab

**12-month forward projection table.**

Each row = one month:
- Month label (e.g., "Apr 2026")
- Expected income (sum of all recurring income normalized to that month)
- Expected expenses (sum of all recurring expenses + one-offs in that month)
- Net for month
- Projected end-of-month balance (running total from current balance)

**Visual treatment:**
- Alternating row shading (`--surface` / `--surface2`)
- Negative balance months: entire row highlighted with `--red-glow` background, balance in `--red`
- Positive net months: net value in `--accent`
- Negative net months: net value in `--red`
- Current month row has a subtle left border accent

## Cache Import

**Accessed via:** Settings modal → "Import from Cache" button

**Flow:**
1. Click "Import from Cache" → file picker opens (accepts `.json`)
2. Reads the file, extracts `recurring` array
3. Filters out items with `amount == 0`
4. Shows preview: "Found N recurring items (X income, Y expenses)"
5. User confirms → items are added to `recurring` array
   - Each imported item gets `sourceId` set to the Cache item's `id`
   - `nextDue` is calculated from today based on `frequency`
   - `enabled` defaults to `true`
6. `importedAt` is set to current timestamp

**Re-import behavior:** If `sourceId` matches an existing recurring item, it is updated (name, amount, frequency, direction). Manually added items (no `sourceId`) are preserved. This allows re-importing after updating Cache data.

**Import button state:** Shows "Imported on [date]" after import, but remains clickable for re-import.

## Visual Design

Matches Cache exactly:

```css
:root {
  --bg:#0d0f0e; --surface:#141714; --surface2:#1a1e1a;
  --border:#252a25; --border-light:#2e352e;
  --accent:#a8d08d; --accent-dim:#6a9e52; --accent-glow:rgba(168,208,141,0.12);
  --red:#e07070; --red-dim:#a84f4f; --red-glow:rgba(224,112,112,0.10);
  --gold:#d4a843;
  --text:#e8ede8; --text-muted:#7a8a7a; --text-dim:#4a5a4a;
  --mono:'DM Mono',monospace; --serif:'DM Serif Display',serif; --sans:'DM Sans',sans-serif;
  --radius:6px;
}
```

- Dark theme only (no light theme)
- Subtle green grid background on body (`body::before`)
- Same component patterns as Cache: section cards, monospace uppercase labels, entry-card expand/collapse
- Fonts: DM Serif Display (headings/balance), DM Mono (numbers/labels), DM Sans (body)
- Frequency badges: small monospace uppercase pills with border
- Paid button: border button, green highlight on hover for income, default for expenses
- Animations: `fadeUp` on sections, slide/fade on paid dismissal

## Lock Screen

Same pattern as Cache:
- Full-screen overlay, centered card
- First run: "Set a password to protect your data" → new password + confirm
- Returning: "Enter your password to unlock" → single input
- Progress bar during PBKDF2 derivation
- Error shake + message on wrong password
- Hint text: "AES-256-GCM encryption - PBKDF2 310k iterations - password never stored"
- Change password accessible from settings

## Settings Modal

- **Change Password** button
- **Import from Cache** button + status
- **Export Data** (JSON, unencrypted — for backup)
- **Clear All Data** (with double-confirm)

## Error Handling

- Decryption failure (wrong password): clear error message, don't clear input focus
- Corrupt localStorage: offer to clear and start fresh
- Import invalid JSON: toast error with details
- Balance going negative: allowed, but shown in red as warning

## Scope Exclusions

- No light theme (can be added later)
- No multi-account support
- No categories/tags on transactions
- No charts or graphs
- No PWA/service worker
- No undo on "Paid" (can be recovered from 30-day history by re-adding)
