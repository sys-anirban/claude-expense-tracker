# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install       # Install dependencies
npm run dev       # Start dev server (http://localhost:5173)
npm run build     # Production build
npm run lint      # Run ESLint
npm run preview   # Preview production build
```

## Architecture

This is a single-component React app (Vite + React 19). All application logic lives in `src/App.jsx` — there are no sub-components, routing, or external state management.

**State in `App.jsx`:**
- `transactions` — array of `{ id, description, amount, type, category, date }`. `amount` is stored as a string; the `reduce` calls use `+` so they concatenate instead of summing (known bug — fix by parsing with `Number()` or `parseFloat()`).
- `filterType` / `filterCategory` — drive client-side filtering of the transaction list.
- Form fields (`description`, `amount`, `type`, `category`) are controlled inputs reset on submit.

**Derived values** (computed inline on each render, not stored in state):
- `totalIncome`, `totalExpenses`, `balance` — reduced from the `transactions` array.
- `filteredTransactions` — filtered view used by the table.

**Categories** are a hardcoded array: `["food", "housing", "utilities", "transport", "entertainment", "salary", "other"]`.

There is no persistence — all data resets on page refresh. Seed transactions have hardcoded `date` strings (`"2025-01-*"`); new transactions use `new Date().toISOString().split('T')[0]`.
