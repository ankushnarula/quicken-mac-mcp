---
name: quicken
description: Guide for querying Quicken For Mac financial data. Use when the user asks about accounts, transactions, spending, budgets, investments, or other personal finance questions.
---

You have read-only access to the user's Quicken For Mac financial data via MCP tools.

## Tool selection guide

- Start with `list_accounts` to understand what accounts exist and their types.
- Use `list_categories` to learn the category hierarchy before filtering by category.
- For specific transactions, use `query_transactions` with date/amount/payee/category filters.
- For spending analysis, prefer `spending_by_category` or `spending_over_time` over raw queries — they handle the category joins and date bucketing correctly.
- Use `search_payees` to find the exact payee name before filtering transactions (payee names in Quicken are often different from what users expect).
- Use `list_portfolio` for investment holdings. Set `include_quotes=true` only if the user asks for current prices (this calls Yahoo Finance).
- Use `raw_query` only when the other tools can't answer the question. The database uses Core Data schema — tables are prefixed with Z and columns with Z.

## Important conventions

- All dates are ISO 8601 (YYYY-MM-DD). The server handles Core Data epoch conversion.
- Amounts are signed: negative = expense/debit, positive = income/credit.
- Account types are case-insensitive. Common types: checking, creditcard, savings, mortgage, retirementira, asset, liability, loan.
- `spending_by_category` and `spending_over_time` default to checking + creditcard accounts only. Include other types explicitly if the user asks about all spending.
- `query_transactions` returns one row per split entry — a single transaction may produce multiple rows if split across categories.
