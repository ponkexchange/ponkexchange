# Security

ponk runs on Solana mainnet and holds real user funds. This file states what has
been assessed by someone outside ponk, what has not, and how to report something.

## Reporting a vulnerability

Report privately, before disclosing anywhere else.

- **Preferred:** GitHub private vulnerability reporting on this repository
  (Security tab, "Report a vulnerability"). It is private to the maintainers.
- **Alternative:** Telegram [@ponkexchange](https://t.me/ponkexchange), asking
  for a private channel before sending any detail.

Please include what you found, where, and the steps to reproduce it. If a
finding moves or exposes funds, say so in the first line.

Do not test against mainnet with other people's positions, and do not run
denial-of-service or spam traffic against the API. A local validator or devnet
reproduction is always preferred and is never treated as a weaker report.

## Assessments

| Assessor | Date | Scope | Depth | Findings |
| --- | --- | --- | --- | --- |
| zauth (Vector) | 29 September 2026 | Web application, API surface and MCP server | Deep scan, 389 turns | 3 high, 5 medium, 1 low, 3 informational. No critical. |

The report is published unedited:

- [Report (PDF)](https://ponk.exchange/audits/zauth-ponk-exchange-2026-09-29.pdf)
- [Audits](https://ponk.exchange/docs/audits) in the docs, with the open findings
  and the coverage table

The engagement exercised 51 endpoints, 5 subdomains, 4 forms and 58 input
vectors through browser automation, crawling and JavaScript analysis, and
verified findings with browser-based proof of concept.

**Three high-severity findings are open as of the report date.** They are named
on the audits page. A published report with open findings is the honest state of
a system assessed today, and each row stays visible until it is closed, with the
date and the change that closed it.

## What has NOT been reviewed by a third party

An assessment only speaks about what it looked at, so this half matters as much
as the table above.

| Area | Third-party reviewed |
| --- | --- |
| ponk.exchange web application | Yes, zauth Vector, 29 Sep 2026 |
| Public API and authenticated endpoints | Yes, zauth Vector, 29 Sep 2026 |
| MCP server and its tools | Yes, zauth Vector, 29 Sep 2026 |
| Ponk Clouds on-chain program | **No** |
| Auto LP agent decision engine | **No**, internal review only |

The **Ponk Clouds** program is deployed on mainnet and has had no third-party
review. Nothing in the zauth assessment speaks to its bin math, its swap
accounting or its vault invariants. Its source and math crate are published so
the numbers can be checked independently, but published source is not a
substitute for a review and is not presented as one here. The
[ponk-rain](https://github.com/ponkexchange/ponk-rain) repository carries an
UNAUDITED warning on the program, and that warning stands.

## Scope of this repository

This repository is the public profile and documentation entry point. The
production application is closed source. The public code lives in
[ponk-rain](https://github.com/ponkexchange/ponk-rain) (Ponk Clouds SDK and
launchpad) and [ponk-sdk](https://github.com/ponkexchange/ponk-sdk) (API
clients). Findings in either are in scope for the reporting process above.
