# Prioritized CRM Backlog

Nouha Meddeb · October 2026 · [Spec sample](spec.md) · [Live prototype](https://nou-meddeb.github.io/quote-playground/)

## Context and my role

These seven requests came from sales, finance, partnerships, marketing and leadership during and after a CRM rollout at a B2B technology company. Names are removed.

- **My role:** Junior Business Consultant (Product Owner scope). I owned the CRM requirements pipeline: collecting requests, separating one-offs from patterns, ranking them, and explaining decisions back to each requester.
- **Note:** the scores below are reconstructed for this sample to show the method. The decisions, including the two reshaped requests and their alternatives, are what happened at the time.

## Prioritization method

Each request is scored 1 to 5 on three criteria, and the weighted total sets the rank.

| Criterion | Weight | What a 5 means |
| --- | --- | --- |
| Retention risk | 40% | Not doing it puts a key customer relationship or user adoption at risk |
| Revenue impact | 35% | Directly speeds up or unlocks revenue |
| Reach | 25% | Affects most users or teams |

Score = 0.40 × retention + 0.35 × revenue + 0.25 × reach. Before scoring, I check two things: is it a one-off or a pattern, and is it already covered by a planned feature?

## Ranked backlog

New deal types rank first because they unlock small, fast revenue for every sales rep; two requests were reshaped rather than built as asked.

| Rank | Request | Raised by | Retention (40%) | Revenue (35%) | Reach (25%) | Score | Decision |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | New deal types: support-only deals and one-time fees, with the full flow from opportunity to invoicing | Sales | 3 | 5 | 4 | 3.95 | Built |
| 2 | Special invoicing for one key customer, based on accumulated quantities from past projects | Finance | 5 | 3 | 1 | 3.30 | Reshaped: no hard-coding. Quick workaround now, configurable rule next time it is needed |
| 3 | Approvals routed per region, one approver per region, instead of the standard CRM flow | COO | 3 | 3 | 4 | 3.25 | Built |
| 4 | Shared leads module with each team's own fields, views and workflows | Partnerships, sales, marketing | 2 | 3 | 5 | 3.10 | Reshaped: one shared core with team-specific views, not separate customizations |
| 5 | One-click view of a deal's full financials, including the past deals it extends, per revenue stream and change | CEO | 2 | 4 | 2 | 2.70 | Built after rank 1 (it needed the new deal types) |
| 6 | Revenue forecasting analytics for the next 5 years, built on CRM data | Finance | 1 | 4 | 2 | 2.30 | Built |
| 7 | Dashboard of customer project tickets by type (bugs, features, custom requests) to track the bug-to-request ratio | Customer project management director | 3 | 1 | 2 | 2.05 | Redirected: built in Power BI from Jira data, outside the CRM backlog |

## Saying no, with an alternative

I declined two requests as asked, and gave each requester another way to get what they needed.

**Customer-specific invoicing (rank 2)**

- **The ask:** finance wanted one key customer invoiced with logic negotiated only for them, based on quantities accumulated across past projects.
- **Why not as asked:** hard-coding one customer's logic into the standard invoicing flow breaks it for everyone else and is hard to maintain.
- **What we did instead:** a quick workaround so finance could invoice correctly right away, and a plan to build it as a configurable rule the next time a customer needs it.

**Team-specific leads module (rank 4)**

- **The ask:** partnerships, sales and marketing each wanted their own fields, views and workflows in one shared leads module.
- **Why not as asked:** heavy per-team customization is what had made the CRM slow and unreliable in the first place.
- **What we did instead:** one shared core module, with a separate solution for the team whose needs the core could not cover.

**How I closed the loop:** each requester heard the decision and the reason directly, along with what they would get instead and when.
