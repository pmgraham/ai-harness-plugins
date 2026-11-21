# Security Policy

## Reporting a Vulnerability

Please report security issues privately using [GitHub Private Vulnerability Reporting](https://github.com/pmgraham/ai-harness-plugins/security/advisories/new).

Do **not** open a public GitHub issue for security vulnerabilities.

## Scope

This policy covers plugin manifests, MCP configurations, rules, skills, and CI workflows maintained in this repository, including:

- Unsafe or misleading MCP server URLs or configurations
- Prompt-injection or data-exfiltration weaknesses in plugin skills or rules
- Missing confirmation guardrails around destructive or write operations
- CI/CD workflow security issues

## Third-Party Services

Plugins in this repository connect to external third-party MCP servers and services (for example, Tiller Money) and run inside AI harnesses (for example, Antigravity). Vulnerabilities in those upstream services or harnesses should be reported directly to their respective vendors.

## Response Timeline

Reports will be acknowledged within 7 days. Once confirmed, a fix and coordinated disclosure timeline will be shared in the private advisory.
