# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install      # install dependencies
npm run dev      # start dev server at http://localhost:5173
npm run build    # production build
npm run preview  # preview production build
npm run lint     # run ESLint
```

There is no test suite in this project.

## Architecture

This is a single-page React app (Vite + React 19), decomposed into the following components:

- `src/App.jsx` — root component; holds the `transactions` array in state and passes data/callbacks down to children.
- `src/Summary.jsx` — displays total income, expenses, and balance; receives `transactions` as a prop and computes totals internally.
- `src/TransactionForm.jsx` — form for adding a new transaction; owns its own form field state and calls `onAdd(transaction)` on submit.
- `src/TransactionList.jsx` — displays the filtered transaction table; receives `transactions` as a prop and owns filter state (`filterType`, `filterCategory`).
- `src/App.css` — all styles, scoped by class names (`.summary`, `.add-transaction`, `.transactions`, `.filters`, `.delete-btn`, etc.).
- `src/main.jsx` — entry point, mounts `<App />` into `#root`.

The `categories` array is duplicated in `TransactionForm.jsx` and `TransactionList.jsx` — not yet extracted to a shared location.

### Known intentional issues (part of the course curriculum)

- **Seeded data:** Transaction #4 ("Freelance Work") is typed `"expense"` but categorized as `"salary"` — intentional inconsistency.
- **UI:** No delete functionality wired up (`.delete-btn` CSS exists but no button is rendered).
