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

This is a single-component React app (Vite + React 19). All logic lives in `src/App.jsx` — there is no routing, no state management library, and no component split.

**State in `App.jsx`:**
- `transactions` — array of `{ id, description, amount, type, category, date }`. `amount` is stored as a **string** (this causes the known summation bug where `reduce` concatenates instead of adding).
- Form fields (`description`, `amount`, `type`, `category`) drive the Add Transaction form.
- `filterType` / `filterCategory` control which rows are shown in the table.

**Known intentional issues (course material):**
- `amount` stored as string → `totalIncome`/`totalExpenses` use string concatenation instead of numeric addition, producing garbage values in the summary cards.
- "Freelance Work" seed data is typed as `"expense"` but categorized as `"salary"`.
- UI and code structure are intentionally rough — the course progressively refactors them.

**Styling:** plain CSS in `src/App.css`, no CSS framework. Key classes: `.income-amount` (green), `.expense-amount` (red), `.balance-amount`.
