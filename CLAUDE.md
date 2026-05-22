# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev      # start dev server at http://localhost:5173
npm run build    # production build
npm run lint     # ESLint
npm run preview  # preview production build
```

No test suite is configured.

## Architecture

React + Vite app with no routing and no state management library. State lives in `App.jsx` and flows down via props; events flow up via callbacks.

**Component tree:**
```
App
├── Summary          — calculates and displays totalIncome, totalExpenses, balance
├── TransactionForm  — owns form field state, calls onAdd(transaction) on submit
└── TransactionList  — owns filterType/filterCategory state, renders the table
```

**Data model:** `transactions` is an array of `{ id, description, amount, type, category, date }` where `amount` is a number, `type` is `"income"` or `"expense"`, and `category` is one of `["food", "housing", "utilities", "transport", "entertainment", "salary", "other"]`.

**Data flow:** `App` holds `transactions` and passes it to all three children. `TransactionForm` receives `onAdd` and calls it with a fully-formed transaction object (amount already coerced to `Number`). `TransactionList` and `Summary` are read-only — they only receive `transactions`.

**Styling:** plain CSS in `src/App.css`, no CSS framework. Key classes: `.income-amount` (green), `.expense-amount` (red), `.balance-amount`.
