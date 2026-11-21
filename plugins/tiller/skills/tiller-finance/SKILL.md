---
name: tiller-finance
description: >-
  Manage personal finances through Tiller Money's official MCP server: analyze
  spending and cash flow, compare budgets period-over-period, audit recurring
  subscriptions, review and categorize transactions, and organize tax or
  business expenses in Tiller spreadsheets. Use whenever the user asks about
  their Tiller spreadsheets, transactions, spending, budget, income, savings
  rate, subscriptions, or personal finance categorization.
---

# Tiller Personal Finance

Use the bundled `tiller-mcp` server (`https://ai-tools.tillermoney.com/mcp`) to query and manage the user's Tiller-powered financial spreadsheets.

## 1. Preflight & Authentication

1. Verify that Tiller MCP tools are loaded in the current session (e.g., tools under the `tiller_tiller-mcp` / `tiller-mcp` server). Inspect each tool's schema before calling it; do not assume parameter names.
2. If the Tiller MCP tools are missing or return an authentication error:
   - Inform the user that Tiller requires OAuth sign-in.
   - Direct them to authorize the `tiller-mcp` server via **Additional Options (...) > MCP Servers** (or the `tiller` plugin page in Customizations), then retry once connected.

## 2. Session Discovery

At the start of any financial analysis or categorization task:

1. **Identify the spreadsheet**: List the user's available Tiller spreadsheets (e.g., `list_spreadsheets`). If more than one spreadsheet is returned, ask the user which spreadsheet to target unless they already named it.
2. **Load the category taxonomy**: Fetch the spreadsheet's categories (e.g., `list_categories`) and note each category's:
   - Exact name (case-sensitive)
   - Group
   - Type (`Income`, `Expense`, `Transfer`)
   - Hidden / exclude-from-reports flag

## 3. Core Workflows

### A. Spending & Cash Flow Analysis

1. Clarify or state the exact date range (default to current calendar month vs. previous calendar month if the user says "this month").
2. Query transactions for the target period(s) using server-side filters where supported (date range, category, account, description). If a query spans a long timeframe or returns truncated results, split by month or quarter and aggregate deterministically.
3. Separate transactions by category type:
   - **Income**: Categories typed `Income` (excluding hidden categories unless requested).
   - **Expenses**: Categories typed `Expense` (excluding hidden categories unless requested).
   - **Transfers**: Categories typed `Transfer` (e.g., credit card payments, bank-to-bank transfers) — list separately or omit from spending/income totals and explicitly note that transfers were excluded.
   - **Uncategorized**: Flag uncategorized transactions separately so totals are transparent and not silently skewed.
4. Present results in a compact Markdown table sorted by magnitude, showing amount, share of total, and period-over-period delta (`$` and `%`).

### B. Transaction Categorization & Cleanup

1. Query uncategorized transactions (or transactions matching the user's filter).
2. Review historical transactions for the same merchant/description when helpful to match the user's established categorization conventions.
3. Map each transaction strictly to an existing category from the user's category list (or explicitly flag if no existing category fits).
4. Group similar merchants and present a review table:
   `| Date | Description | Account | Amount | Proposed Category | Notes |`
5. **Wait for explicit user approval** before calling any write/update tool (e.g., `update_transactions`). Apply only approved rows, then verify the updated count and report any failures verbatim.

### C. Recurring Subscriptions & Bill Audit

1. Query at least the trailing 3 months (or 12 months when checking annual renewals) of Expense transactions.
2. Normalize merchant descriptions and detect repeating charges by cadence (weekly, monthly, quarterly, annual).
3. Highlight:
   - Active recurring subscriptions with estimated monthly and annualized cost
   - Price increases between billing cycles
   - Potential duplicate or overlapping services

### D. Savings Rate & Budget Health

1. Compute Net Cash Flow (`Total Income - Total Expenses`) and Savings Rate (`(Total Income - Total Expenses) / Total Income`) using non-transfer, non-hidden categories.
2. Explicitly call out any uncategorized inflows/outflows that could shift the rate.
3. Surface the top 3–5 spending drivers or variance outliers with specific backing transactions.

### E. Tax & Business Expense Review

1. Filter transactions by the relevant tax year and business categories, tags, notes, or dedicated business accounts.
2. Flag ambiguous or mixed-use merchants for user review rather than reclassifying them automatically.
3. Present a categorized summary table suitable for review; remind the user to confirm tax treatment with a qualified tax professional.

## 4. Quality & Safety Guardrails

- **Never fabricate numbers**: Every dollar figure must come directly from Tiller MCP tool output.
- **Check sign conventions**: Confirm whether outflows are negative and inflows are positive in the user's sheet before summing or computing net deltas.
- **Batch safely**: When updating multiple transactions, update only confirmed rows and report exact counts of succeeded vs. failed updates.
