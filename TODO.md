# TODO

## Format

Each item: `- [ ] Description` with metadata tags: `[type]` `[complexity]` `[priority]`

**Types:** `feature`, `bug`, `polish`, `refactor`
**Complexity:** `small`, `medium`, `large`
**Priority:** `high`, `medium`, `low`

---

### Bugs
- [x] Import JSON Confirm/Cancel buttons need to be horizontally centered `[bug]` `[small]` `[medium]`
- [x] JSON Exports not capturing current balance `[bug]` `[small]` `[high]`

### Bottom Menu & Chrome
- [x] Add bottom menu bar matching Cache: About button, Settings button, Lock button, Save button, and same disclaimer text about data `[feature]` `[medium]` `[high]`
- [x] Top banners/menus (header, summary bar, tab nav) should be sticky/frozen so they're always visible on scroll `[polish]` `[small]` `[high]`

### Dashboard Redesign
- [ ] Add side-by-side pie charts on Dashboard showing income and expense breakdowns by category `[feature]` `[large]` `[high]`
- [x] Remove "Upcoming This Week" and "Upcoming This Month" sections from Dashboard `[refactor]` `[small]` `[high]`
- [x] Move Quick Add button from Dashboard to Transactions page, pinned/frozen at the top so it's always visible `[refactor]` `[small]` `[high]`

### Recurring Cash Flow Page
- [ ] Add a dedicated Recurring Cash Flow tab/page (like Cache's Cash Flow page) for managing all recurring income/expenses setup `[feature]` `[large]` `[high]`

### Transactions Page Overhaul
- [ ] Transactions page should forecast out 6 months with +/- controls to increase/decrease the horizon `[feature]` `[medium]` `[high]`
- [ ] Transactions page should be grouped by month with expand/collapse capability `[feature]` `[medium]` `[high]`
- [ ] Remove "Add Recurring" button from Transactions page (recurring items managed on Recurring Cash Flow page) `[refactor]` `[small]` `[medium]`

### UX Improvements
- [ ] Animate individual element removal on delete/paid/received instead of full page re-render; same for "Show Paid" toggle `[polish]` `[medium]` `[medium]`
- [x] Add ability to delete a transaction without affecting balance (separate from paid/received) `[feature]` `[small]` `[high]`

### Forecast Page Enhancements
- [ ] Add line chart to Forecast page showing balance projections as time series (individual income/expense items and overall balance) `[feature]` `[large]` `[high]`
- [ ] Add slider at top of Forecast page to adjust forecast horizon by monthly intervals, with graph and table updating dynamically `[feature]` `[medium]` `[high]`

### Bitcoin Integration
- [ ] Add Bitcoin price tracker banner at top (with live API calls), matching Cache's BTC ticker bar `[feature]` `[large]` `[high]`
- [ ] Support dual balances: Cash balance and Bitcoin balance. Option to display combined balance as cash + cash equivalent of BTC holdings `[feature]` `[large]` `[high]`
