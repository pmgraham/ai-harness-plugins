# Tiller Finance Plugin

Connects Antigravity to [Tiller Money](https://www.tiller.com)'s official remote MCP server (`https://ai-tools.tillermoney.com/mcp`) for personal finance analysis and spreadsheet management.

## What's Included

- **MCP Server (`tiller-mcp`)**: Streamable HTTP connection to `https://ai-tools.tillermoney.com/mcp` using Tiller's OAuth flow.
- **Skill (`tiller-finance`)**: Guided workflows for spending and cash flow analysis, uncategorized transaction review, recurring subscription audits, savings rate tracking, and business/tax expense separation.
- **Rules (`rules/AGENTS.md`)**: Always-on guardrails requiring explicit confirmation before writing to your spreadsheet, excluding internal transfers from spending/income totals, and keeping numbers strictly grounded in tool outputs.

## Setup

1. Ensure you have an active Tiller subscription feeding your Google Sheets or Excel workbook.
2. Enable the **Tiller Finance** plugin in Customizations (enabled by default once installed).
3. Complete the OAuth sign-in prompt for `tiller-mcp` under **Additional Options (...) > MCP Servers** when first connecting.

## Example Prompts

- *"Summarize my spending by category this month compared to last month"*
- *"Find uncategorized transactions and suggest categories for my review"*
- *"Identify recurring subscriptions and flag any recent price changes"*
- *"What was my savings rate over the last 3 months?"*
