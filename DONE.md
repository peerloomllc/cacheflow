# DONE

## Format

Each item: `- [x] Description` with metadata tags and completion date.

---

- [x] Envelope / zero-based budgeting Phase 1: explicit Fixed/Envelope kind on recurring expenses; one-offs in matching category deduct from the monthly envelope; progress bar on Recurring row + Budgets card on Dashboard; validate one envelope per category; added Groceries + Dining default categories `[feature]` `[large]` `[medium]` — 2026-05-02
- [x] Allow recurring expenses/income to be denominated in sats (extend FIAT/SATS toggle from one-off form to recurring add/edit) `[feature]` `[small]` `[high]` — 2026-05-02
- [x] Default Transactions and Forecast horizon to 1 month and persist user's chosen horizon to settings `[polish]` `[small]` `[high]` — 2026-05-02
- [x] Summary bar moved from persistent header into Dashboard view; mobile header diet (hide title block, drop Total Balance label, shrink balance font, remove BTC fiat-equivalent line) `[polish]` `[medium]` `[high]` — 2026-05-02
- [x] Transactions tab: sticky toolbar (horizon, Show paid, Quick Add, search, Collapse All) pins under tab nav while rows scroll; required overflow-x:clip on html/body and animation override on .tx-section to fix containing-block conflicts `[feature]` `[medium]` `[medium]` — 2026-05-02
- [x] Recurring tab polish: sections collapsed by default, equal-width Save/Cancel via flex row, brighter + Add buttons (text-muted → text + accent-glow hover), centered + Add bar with flex-wrap, wider tables on desktop (1100px → 1280px view max-width) `[polish]` `[medium]` `[medium]` — 2026-05-02
- [x] Quick Add + bottom-bar polish: Quick Add Unit/Type toggles equal-width on mobile (50/50 split) with centered button text; Cancel/Add form buttons share equal height (matched 1px border box) and equal width (min-width 80px desktop, flex-equal up to 200px on mobile); bottom menu hides text labels on mobile (icons-only) for About/Settings/Lock — Save keeps "Save ✓" `[polish]` `[small]` `[medium]` — 2026-04-30
- [x] Edit/remove custom categories: Settings modal "Custom Categories" section lists user-added expense + income categories with Rename and Delete actions; rename propagates the new name to all referencing recurring/oneoff/override transactions in the same group; delete confirms with usage count and nulls referencing transactions to Uncategorized; built-in categories remain immutable `[feature]` `[medium]` `[medium]` — 2026-04-30
- [x] Custom user-defined categories: "+ New category…" option at bottom of every Category dropdown (Quick Add, Add Recurring, recurring inline edit, Transactions edit modal); prompts for a name, validates uniqueness case-insensitively, persists in `appData.customCategories.{expense,income}`; merged with built-in list (sorted, "Other" last); income/expense groups kept separate `[feature]` `[medium]` `[medium]` — 2026-04-30
- [x] Quick Add categories + $/₿ unit toggle: one-off transactions can be denominated in USD or sats (e.g. 50k-sat coffee); sats one-offs settle against BTC balance; data model is direction × unit with migration from prior btc-expense shape; Bonus added to Income categories `[feature]` `[medium]` `[medium]` — 2026-04-28
- [x] Dashboard ±60-day windowing: Income/Expense Breakdown charts include one-offs from past 60 days and next 60 days averaged across the 120-day window; one-offs feed category breakdowns; sats one-offs convert to fiat-equivalent for aggregation; legends moved below doughnuts `[feature]` `[medium]` `[medium]` — 2026-04-28
- [x] Quick Add layout polish: reduced Description field width, fixed Category dropdown arrow overlapping selected text, centered Save/Cancel buttons on mobile inline forms `[polish]` `[small]` `[medium]` — 2026-04-28
- [x] Privacy mode toggle in bottom menu (eye icon next to Lock) — blurs balance, summary bar, recurring/forecast/transaction amounts, dashboard charts, and runway; persists with data; mobile layout collapses to icon-only `[feature]` `[medium]` `[medium]` — 2026-04-28
- [x] Add Fiat/SATS toggle (matching Cache) under Total Balance — denominates all fiat values in sats when active, persists with data, disables when BTC price unavailable `[feature]` `[medium]` `[medium]` — 2026-04-28
- [x] Add Dues & Memberships category for HOA, club, and membership fees (distinct from Subscriptions) `[feature]` `[small]` `[low]` — 2026-04-28
- [x] Add more recurring expense categories: Taxes, Childcare, Fees & Charges, Gifts & Donations, Personal Care, Pets, Travel `[feature]` `[small]` `[medium]` — 2026-04-28
- [x] Remove Weekly sections/collapsibles from Transactions tab — group transactions by Month only `[refactor]` `[small]` `[medium]` — 2026-04-27
- [x] Scale all CSS font sizes ~25% larger across the UI for better readability, matching Cache's typography scaling `[polish]` `[medium]` `[medium]` — 2026-04-19
- [x] Mobile view - Recurring tab - 2-row stacked card layout (toggle · name · amount · delete on top; category · frequency · start · end below) eliminates horizontal scroll `[polish]` `[small]` `[medium]` — 2026-04-17
- [x] Editing a transaction on the Transactions tab should NOT update the recurring template on the Recurring tab — transactions are separate instances (recurring is an estimate; actuals can vary when a bill comes due) `[bug]` `[medium]` `[medium]` — 2026-04-17
- [x] Income profitability dashboard: per-income-source stacked bar visualization on Dashboard + expense-to-income linking via dropdown on recurring expense edit `[feature]` `[medium]` `[low]` — 2026-04-17
- [x] Add a dedicated Recurring Cash Flow tab/page for managing all recurring income/expenses setup `[feature]` `[large]` `[high]` — 2026-04-05
- [x] Add bottom menu bar matching Cache: About button, Settings button, Lock button, Save button, and same disclaimer text about data `[feature]` `[medium]` `[high]` — 2026-04-04
- [x] Import JSON Confirm/Cancel buttons need to be horizontally centered `[bug]` `[small]` `[medium]` — 2026-04-04
- [x] Top banners/menus (header, summary bar, tab nav) sticky/frozen on scroll `[polish]` `[small]` `[high]` — 2026-04-04
- [x] Remove "Upcoming This Week" and "Upcoming This Month" sections from Dashboard `[refactor]` `[small]` `[high]` — 2026-04-04
- [x] Move Quick Add button from Dashboard to Transactions page toolbar `[refactor]` `[small]` `[high]` — 2026-04-04
- [x] JSON import now restores balance when present in imported file `[bug]` `[small]` `[high]` — 2026-04-04
- [x] Skip/delete transaction button (✕) without affecting balance `[feature]` `[small]` `[high]` — 2026-04-04
- [x] Search/filter transactions on Transactions tab `[feature]` `[small]` `[high]` — 2026-04-04
- [x] Remove "Add Recurring" button from Transactions page `[refactor]` `[small]` `[medium]` — 2026-04-04
- [x] Transactions page grouped by month with expand/collapse `[feature]` `[medium]` `[high]` — 2026-04-04
- [x] Transactions page should forecast out 6 months with +/- controls to increase/decrease the horizon `[feature]` `[medium]` `[high]` — 2026-04-04
- [x] Add slider at top of Forecast page to adjust forecast horizon by monthly intervals, with graph and table updating dynamically `[feature]` `[medium]` `[high]` — 2026-04-04
- [x] Add line chart to Forecast page showing balance projections as time series (individual income/expense items and overall balance) `[feature]` `[large]` `[high]` — 2026-04-04
- [x] Animate transaction removal (slide-out on paid/skip), month/week collapse/expand, and edit panel toggle without full page re-render `[polish]` `[medium]` `[medium]` — 2026-04-04
- [x] Animate "Show Paid" toggle (staggered fade-in for history rows) `[polish]` `[small]` `[low]` — 2026-04-05
- [x] Font sizes too small on 1440p desktop monitors; review and adjust for better readability `[polish]` `[medium]` `[medium]` — 2026-04-05
- [x] JSON import of recurring transactions from Cache export should navigate to the Recurring tab `[bug]` `[small]` `[medium]` — 2026-04-05
- [x] Add Bitcoin price tracker banner at top (with live API calls), matching Cache's BTC ticker bar `[feature]` `[large]` `[high]` — 2026-04-06
- [x] Support dual balances: Cash balance and Bitcoin balance with combined total display `[feature]` `[large]` `[high]` — 2026-04-06
- [x] Recurring BTC transaction types: btc-income (mining/stacking) and btc-buy (DCA) with forecast integration `[feature]` `[large]` `[high]` — 2026-04-06
- [x] Add category field to recurring transactions with direction-aware dropdowns, sortable columns, and inline editing `[feature]` `[medium]` `[high]` — 2026-04-06
- [x] Recurring tab polish: remove Monthly column, column sorting, date format (yyyy/mm/dd), dark date picker theme, surgical transaction edit saves `[polish]` `[medium]` `[medium]` — 2026-04-06
- [x] Cancel blank recurring item instead of creating "(unnamed)" entry `[bug]` `[small]` `[medium]` — 2026-04-06
- [x] Add side-by-side pie charts on Dashboard showing income and expense breakdowns by category `[feature]` `[large]` `[high]` — 2026-04-06
- [x] Add BTC vs Fiat allocation visualization (donut/bar showing % of combined balance in BTC vs cash) `[feature]` `[medium]` `[medium]` — 2026-04-06
- [x] Add cash runway indicator ("X days until balance hits zero" based on current burn rate) `[feature]` `[medium]` `[medium]` — 2026-04-06
- [x] Guided tutorial walkthrough (same method as Cache app) highlighting Bitcoin-based features (BTC balances, price ticker, recurring BTC transactions) `[feature]` `[large]` `[high]` — 2026-04-06
- [x] CacheFlow JSON backup import/restore in Settings `[feature]` `[medium]` `[high]` — 2026-04-06
- [x] Move Cache import to Dashboard empty state only (first-run onboarding) `[refactor]` `[small]` `[medium]` — 2026-04-06
- [x] Remove redundant balance fields from Settings (header supports inline editing) `[refactor]` `[small]` `[low]` — 2026-04-06
- [x] Fix mobile bottom menu centering `[bug]` `[small]` `[medium]` — 2026-04-06
- [x] Make header/footer bars fully opaque (no scroll-through bleed) `[polish]` `[small]` `[low]` — 2026-04-06
- [x] Hyperlink Cache on Dashboard welcome page `[polish]` `[small]` `[low]` — 2026-04-06
- [x] Dark/Light mode option (same as Cache app) `[feature]` `[medium]` `[medium]` — 2026-04-06
- [x] Undo option for recently paid transactions (when revealed through Show Paid toggle) `[feature]` `[medium]` `[medium]` — 2026-04-06
- [x] Currency switching in Settings with live exchange rates `[feature]` `[medium]` `[medium]` — 2026-04-06
- [x] Set up automated merging to website repo for automated updates `[feature]` `[medium]` `[high]` — 2026-04-06
