# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Cache Flow is a single-file personal cash flow and budgeting app (`cacheflow.html`). It is the companion app to [Cache](~/peerloomllc/cache/cache.html) (a net worth ledger). Both share the same dark theme design language but are fully independent — separate passwords, separate localStorage keys, separate data.

No build system, no server, no frameworks. Opens directly in a browser.

## Development

There is no build step, test suite, or linter. To develop:

1. Open `cacheflow.html` in a browser
2. Edit the file
3. Refresh the browser

To test encryption, clear `cacheflow-v1-enc` and `cacheflow-v1-meta` from localStorage (DevTools → Application → Local Storage) to reset to first-run state.

## Architecture

Everything lives in one file organized in this order:

1. **`<style>`** (~200 lines) — CSS custom properties at `:root`, then styles grouped by component (lock screen, header, summary bar, tabs, sections, transaction rows, forms, settings modal, forecast table, responsive breakpoints)
2. **`<body>` HTML** (~80 lines) — Lock screen overlay, `#app` div (header, summary bar, tab nav, three `.view` containers), settings modal, toast
3. **`<script>`** (~1150 lines) — organized as:
   - Constants and state (`STORAGE_ENC`, `STORAGE_META`, `appData` object)
   - Crypto helpers (`deriveKey`, `encryptPayload`, `decryptPayload`)
   - Lock screen functions (`showLockScreen`, `submitUnlock`, `submitSetPassword`, `lockApp`)
   - Idle timer (`resetIdleTimer`, 15-min auto-lock)
   - `encryptAndSave()` — encrypts `appData` and writes to localStorage; also prunes history older than the configured retention window (`appData.settings.historyRetentionDays`, default 30; `0` = keep everything)
   - Helpers (`generateId`, `fmtMoney`, `normalizeToMonthly`, `advanceDate`, `getUpcomingTransactions`)
   - Tab switching
   - `renderAll()` → calls `renderDashboard()`, `renderTransactions()`, `renderForecast()`
   - Action handlers (`markPaid`, `showQuickAdd`, `submitAddRecurring`, inline edit, etc.)
   - Settings, Cache import, export, clear data
   - Boot sequence (IIFE at bottom)

## Key Design Decisions

- **Encryption**: AES-256-GCM + PBKDF2 (310k iterations) via Web Crypto API. Session key held in memory, cleared on lock. Salt in `cacheflow-v1-meta`, ciphertext in `cacheflow-v1-enc`.
- **Single balance model**: One checking account balance, adjusted by Paid/Received actions. No multi-account.
- **Transaction lifecycle**: Recurring items have `nextDue` dates. `markPaid()` adjusts balance, pushes to `history[]`, advances `nextDue`. History pruned on save to the user-configurable retention window (Settings → History Retention; default 30 days, `0` = keep everything).
- **Rendering**: All views re-render via `innerHTML` on each `renderAll()` call. No virtual DOM, no diffing. State lives in the `appData` object.
- **Cache import**: Reads the `recurring` array from a Cache JSON export. Matches existing items by `sourceId` for re-import updates.

## Companion App Reference

The visual design (CSS custom properties, component patterns, fonts) is intentionally matched to `~/peerloomllc/cache/cache.html`. When making visual changes, check that file for the canonical design language.
