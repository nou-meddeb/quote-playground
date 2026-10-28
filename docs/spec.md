# Pricing & Quoting Platform: Requirements Spec

Nouha Meddeb · October 2026 · [Live prototype](https://nou-meddeb.github.io/quote-playground/) · [Backlog sample](backlog.md)

## Context and my role

This spec covers the in-house pricing and quoting platform I designed to replace quote creation inside an over-customized CRM at a B2B technology company. Company, system and client names are removed.

- **My role:** Business Consultant (Product Owner scope). I ran discovery with sales, finance, legal and the internal platform team, wrote the requirements and acceptance criteria, and owned delivery with engineering through rollout.
- **Scope:** offer and quote creation across four revenue streams, connected to finance invoicing, legal review and the internal product platform.

## Problem

One quote took 7+ steps and up to six people to approve, and the result was often wrong by the time it reached invoicing.

**How a quote was created before:**

1. A sales manager starts the quote in the CRM, which is so customized it is slow and unreliable.
2. A CRM support specialist helps, because most sales managers cannot complete a quote alone.
3. A solution engineer configures product specifics in a separate internal product platform, which depends on conditions set in the CRM.
4. The head of product approves the product configuration.
5. The CEO approves the product configuration.
6. The sales director approves the CRM quote.
7. If the offer includes custom development, customer project managers scope it and their lead approves it. The quote cannot be sent before this.
8. Legal reviews through a separate Jira ticket, outside the quote flow.

**What went wrong:**

- **Price changes broke active quotes.** A new unit price meant a new price version, and every active quote had to be updated by rule. Many needed manual fixes.
- **Manual edits broke invoicing.** Invoicing reads from the quote, so manually edited quotes made invoices fail or come out wrong.
- **Discounts were painful.** Adjusting a quote to match a negotiation meant repeated edits and new approval loops.
- **Text added to the PDF by hand was lost.** It was not saved in the system, so it was not tracked.
- **Users could not follow the system,** even after training workshops, and complained constantly.

## Affected users

| User | Today's pain | Need |
| --- | --- | --- |
| Sales managers | Cannot build or adjust a quote alone; discounts take several loops | Build and adjust quotes alone, see prices before saving |
| Approvers (sales director, head of product, CEO) | Back-and-forth approvals on each change | Review and decide together with the requester, in one place |
| Solution engineers | Configure product specifics in a separate platform that depends on CRM conditions | Configure inside the same flow |
| Finance | Invoices fail when quotes were edited by hand; payment schedule changes after signing are hard | Clean data from offer to invoice; adjust payment schedules after signing |
| Legal | Reviews arrive as separate Jira tickets, outside the quote | Notified inside the flow when their review is needed |
| CRM and platform support team | Pulled into most quotes to help or fix errors | Fewer support requests and manual fixes |

## Proposed behavior

A dedicated in-house platform replaces quote creation in the CRM. Requester and approver work in one shared editor, and every change is tracked from offer to invoice.

| # | Capability | Behavior |
| --- | --- | --- |
| 1 | Quote "playground" editor | All options on one screen with drag and drop and no pop-up chains. Prices and discounts preview before saving. Requester and approver edit together, replacing the back-and-forth loop. |
| 2 | Discount guardrails | Discounts within a defined range are approved automatically. Only larger discounts go to an approver. |
| 3 | Validation rules | Invalid product or price combinations are blocked before saving. |
| 4 | Automatic price versioning | A new unit price applies to active quotes by rule, with no manual fixes. |
| 5 | Extension deals | A new offer can start from a past deal and stays linked to it. |
| 6 | Saved custom PDF text | Extra text for the customer PDF is entered and saved in the system, never added by hand. |
| 7 | One-click PDF | The PDF always matches the saved quote data. |
| 8 | Offer-to-invoice data link | Invoicing reads clean, saved quote data. |
| 9 | Payment schedule changes | Finance adjusts payment schedules after signing without breaking the deal record. |
| 10 | Legal notifications | Legal is notified in the flow when an offer needs review. No separate ticket. |
| 11 | Audit trail | Every price or quote change logs who, when and why. |
| 12 | Role-based views | Sales, finance and legal each see the fields and actions they need. |

## Acceptance criteria

Each capability is done when its criteria pass in UAT with real users from sales, finance and legal.

| # | Capability | Given / When / Then |
| --- | --- | --- |
| 1 | Playground editor | **Given** a draft quote, **when** the sales manager changes a quantity or discount, **then** the new total previews instantly and nothing is saved until they confirm. |
| 1 | Playground editor | **Given** a quote shared with an approver, **when** both have it open, **then** both see the same live version and the approver can approve from that screen. |
| 2 | Discount guardrails | **Given** a discount inside the allowed range, **when** the quote is saved, **then** it is approved with no approver step. **Given** a discount above the range, **then** it is routed to the approver. |
| 3 | Validation rules | **Given** an invalid product or price combination, **when** the user tries to save, **then** saving is blocked and the reason is shown. |
| 4 | Price versioning | **Given** a new unit price, **when** it is published, **then** all active quotes in scope update by rule and the change shows in their history. |
| 5 | Extension deals | **Given** a signed past deal, **when** a user creates an extension, **then** the new offer is prefilled from it and stays linked. |
| 6 | Custom PDF text | **Given** custom text entered on a quote, **when** the PDF is generated, **then** the text appears and stays saved on the quote. |
| 8 | Offer-to-invoice link | **Given** a signed quote, **when** finance creates the invoice, **then** all line items, prices and discounts carry over with no manual re-entry. |
| 9 | Payment schedule changes | **Given** a signed deal, **when** finance changes the payment schedule, **then** future invoices follow the new schedule and the change is logged. |
| 10 | Legal notifications | **Given** an offer that needs legal review, **when** it is submitted, **then** legal is notified in the platform and the offer cannot be sent before approval. |
| 11 | Audit trail | **Given** any change to price, discount or terms, **when** it is saved, **then** user, time and reason are logged and visible on the quote. |

## Out of scope and dependencies

**Out of scope (v1):**

- Templates for recurring offer types (moved to a later release)
- Customer-specific invoicing logic hard-coded for single clients. These are handled as configurable rules or a documented manual step.

**Dependencies:**

- CRM: quoting moves out of the CRM completely. The new platform becomes the single place for offers and quotes.
- Internal product platform: product specifics move into the quote flow, so their approval rules must be aligned first.
- Finance invoicing: depends on the offer-to-invoice data link being live before cut-over.
- Legal: agreement on which offer types trigger a review.

## Outcome

Time-to-market for new offers dropped roughly 3x, and 30+ users across four to five teams adopted the platform.

- Approvals moved from a sequential back-and-forth into one shared editing session.
- Invoicing runs on clean, saved quote data instead of manually edited quotes.
- Legal reviews happen inside the flow, with no separate tickets.
- The process is fast, and sales managers now create quotes on their own, without support stepping in each time.
