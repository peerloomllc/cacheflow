# Cache Flow

Personal cash flow and budgeting app. Track recurring income and expenses, forecast future balances and manage Bitcoin DCA - all with AES-256-GCM encryption and local-only data storage.

Single HTML file. No build system, no dependencies, no server. Open it in a browser.

Companion app to [Cache](https://github.com/peerloomllc/cache) (a net worth ledger). Both share the same design language but are fully independent - separate passwords, separate data.

## Features

- Recurring transactions with flexible frequencies: weekly, biweekly, monthly, quarterly, annual and custom day intervals
- One-off transactions for non-recurring income and expenses
- Dashboard with balance header, income/expense summary, spending breakdown donut chart, balance history sparkline and financial runway estimate
- 12-month rolling forecast with weekly drill-down, projected balance and net cash flow
- Bitcoin integration: BTC balance tracking, DCA recurring buys and sat stacking with live BTC price from CoinGecko (fallback: Coinbase)
- AES-256-GCM encryption with PBKDF2-derived keys; data encrypted at rest in localStorage
- Auto-lock: 15-minute idle timeout clears the session key and wipes data from memory
- Multi-currency support: USD, EUR, GBP, CAD, AUD, CHF, JPY with live exchange rates
- Category tagging for expenses (Housing, Food & Dining, Subscriptions etc.) and income (Salary, Freelance etc.)
- Mark paid / undo paid with balance adjustment and 30-day history
- Import recurring transactions from a Cache JSON export
- JSON export and import for backup and restore
- Dark and light themes
- Guided onboarding tutorial for first-time users
- Mobile-friendly responsive layout
- PWA install for standalone app experience on desktop and mobile

## Getting started

```bash
# Clone and open
git clone https://github.com/peerloomllc/cacheflow.git
cd cacheflow
xdg-open cacheflow.html    # Linux
open cacheflow.html         # macOS
start cacheflow.html        # Windows
```

Or just double-click `cacheflow.html`. No install required.

On first launch, set a password. This derives your encryption key. You can change your password later in Settings, but there is no reset or recovery if you forget it.

## How it works

All data stays on your device. The only network requests are:

| Request | Purpose |
|---------|---------|
| CoinGecko / Coinbase API | BTC price |
| frankfurter.dev | Currency exchange rates |

### Data storage

- `cacheflow-v1-enc` in localStorage: AES-256-GCM ciphertext of your data
- `cacheflow-v1-meta` in localStorage: PBKDF2 salt (not secret)

The password is never stored. The derived `CryptoKey` is held in memory only and cleared on lock or idle timeout.

### Architecture

Everything lives in one file (`cacheflow.html`):

| Section | Purpose |
|---------|---------|
| CSS | Dark/light themes, responsive layout, animations |
| HTML | Lock screen, dashboard, transactions, forecast, settings |
| JS: Encryption | AES-256-GCM, PBKDF2, session management |
| JS: Rendering | Dashboard, transactions list, forecast table |
| JS: Actions | Mark paid/undo, quick add, inline edit and recurring CRUD |
| JS: Forecast | 12-month projection with weekly granularity |
| JS: BTC | Price ticker, DCA processing, sat balance tracking |
| JS: Persistence | Save, load, export, import and Cache import |

## Security model

- AES-256-GCM with PBKDF2-derived keys (310,000 iterations, SHA-256)
- No plaintext ever hits disk; data is encrypted before writing to localStorage
- 15-minute idle auto-lock destroys the in-memory key
- No server, no cookies, no analytics and no telemetry

## License

Copyright PeerLoom LLC. All rights reserved.
