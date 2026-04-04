# TODO

## Format

Each item: `- [ ] Description` with metadata tags: `[type]` `[complexity]` `[priority]`

**Types:** `feature`, `bug`, `polish`, `refactor`
**Complexity:** `small`, `medium`, `large`
**Priority:** `high`, `medium`, `low`

---

### Dashboard Redesign
- [ ] Add side-by-side pie charts on Dashboard showing income and expense breakdowns by category `[feature]` `[large]` `[high]`

### Recurring Cash Flow Page
- [ ] Add a dedicated Recurring Cash Flow tab/page (like Cache's Cash Flow page) for managing all recurring income/expenses setup `[feature]` `[large]` `[high]`

### Transactions Page Overhaul
- [ ] Transactions page should forecast out 6 months with +/- controls to increase/decrease the horizon `[feature]` `[medium]` `[high]`

### UX Improvements
- [ ] Animate individual element removal on delete/paid/received instead of full page re-render; same for "Show Paid" toggle `[polish]` `[medium]` `[medium]`

### Forecast Page Enhancements
- [ ] Add line chart to Forecast page showing balance projections as time series (individual income/expense items and overall balance) `[feature]` `[large]` `[high]`
- [ ] Add slider at top of Forecast page to adjust forecast horizon by monthly intervals, with graph and table updating dynamically `[feature]` `[medium]` `[high]`

### Bitcoin Integration
- [ ] Add Bitcoin price tracker banner at top (with live API calls), matching Cache's BTC ticker bar `[feature]` `[large]` `[high]`
- [ ] Support dual balances: Cash balance and Bitcoin balance. Option to display combined balance as cash + cash equivalent of BTC holdings `[feature]` `[large]` `[high]`
