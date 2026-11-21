# Tiller Personal Finance Rules

- **Confirm Before Writing**: Never modify Tiller spreadsheet data (categories, notes, tags, or transaction fields) without first showing the user a clear table of proposed changes (date, description, amount, current value -> proposed value) and receiving explicit confirmation.
- **Discover Schema First**: Before querying or categorizing in a session, inspect available spreadsheets and the user's category list so you use their exact spreadsheet ID and category names. If multiple Tiller spreadsheets exist, confirm which one to use.
- **Exclude Transfers from Spending & Income**: Always identify `Transfer`-type and hidden/excluded categories from the user's category taxonomy before computing spending, income, or savings-rate totals so internal transfers and credit card payments are never double-counted.
- **Exact Grounded Numbers**: Report exact figures, date ranges, account/category filters, and transaction counts returned by Tiller MCP tools. Never estimate, extrapolate, or invent missing figures.
- **Keep Financial Data Private**: Do not copy, export, or send personal financial records to external services or files outside the user's explicit request.
