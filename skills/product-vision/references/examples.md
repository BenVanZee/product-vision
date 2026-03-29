# Vision Document Examples

Annotated examples showing good vs. weak writing for each section type.
Reference these when drafting or auditing vision docs to calibrate quality.

---

## Vision Statements

### Weak

> FM22 will be the best IFTA reporting platform, providing a world-class
> experience for our users with cutting-edge technology.

**Why it's weak:** "Best," "world-class," and "cutting-edge" are empty. No one
can read a GitHub issue and determine whether it advances this vision. It could
describe any product in any domain.

### Good

> FM22 transforms IFTA reporting from a manual data-entry chore into an
> intelligent fuel and mileage tax platform. Analysts shift from typing numbers
> into spreadsheets to reviewing AI-flagged anomalies, resolving client issues
> through a structured portal, and delivering quarterly filings that clients
> trust because the data pipeline caught errors before they did.

**Why it's good:** Concrete capabilities (AI-flagged anomalies, structured portal,
data pipeline). A developer can read an issue like "Add variance detection for
mileage totals" and say "yes, this advances the vision — it's part of 'the data
pipeline caught errors.'" Scorable.

---

## User Personas

### Weak

> **User**: Someone who uses the system.
> - Goal: Get work done efficiently
> - Pain: System is sometimes slow
> - Success: Happy users

**Why it's weak:** Describes every user of every product. No specificity about
THIS product, THIS person, or THIS workflow. Cannot inform feature prioritization.

### Good

> ### Tax Analyst (primary: Erasmo, team of 3)
> - **Goal:** Process 200+ carrier IFTA filings per quarter with zero
>   jurisdiction-level errors
> - **Pain:** Manually comparing fuel purchases against mileage to spot
>   discrepancies. One missed non-contiguous jurisdiction gap can trigger
>   an audit for the client.
> - **Success looks like:** Anomalies flagged automatically before review.
>   Filing prep time per client drops from 45 minutes to 15 minutes.

**Why it's good:** Names real people. Goals are specific to the product domain
(IFTA filings, jurisdiction errors). Pain points describe actual daily
frustrations. Success criteria are measurable (45→15 minutes). A sprint planner
can look at this and prioritize "automated anomaly detection" because it directly
serves the primary persona's biggest pain point.

---

## Current State vs. Target State

### Weak

| Capability | Today | Target | Gap |
|-----------|-------|--------|-----|
| Data | Manual | Automated | Big |
| UI | Basic | Better | Medium |
| Reports | Exists | Improved | Small |

**Why it's weak:** Too vague to be actionable. "Manual" what? "Automated" how?
"Better" by what measure? No one can map a GitHub issue to "Better UI."

### Good

| Capability | Today | Target | Gap |
|-----------|-------|--------|-----|
| Data ingestion | CSV upload with manual column mapping | ELD auto-sync via adapter layer, client self-upload with validation | Large — adapter layer + upload UI needed |
| Anomaly detection | Analyst eyeballs every line | Rules engine flags issues by severity; analyst reviews exceptions only | Medium — rules engine scaffolded, needs 40+ rules |
| Client communication | Email/phone, no tracking | Structured portal: client sees flagged issues, responds with corrections, resolution tracked | Large — new subsystem |
| Quarterly filing | Manual PDF generation per carrier | Batch generation with variance warnings, filing history queryable | Medium — PDF engine exists, needs batch + history |

**Why it's good:** Each row is specific enough that a developer can read it and
know what to build. "Rules engine needs 40+ rules" tells sprint planning that
individual rule issues are valuable. The gap sizing (Large/Medium) helps
prioritization — tackle medium gaps for quicker wins, plan for large gaps over
multiple sprints.

---

## Roadmap Items

### Weak

> ### Now
> - Make the app better
> - Fix bugs
> - Improve performance

**Why it's weak:** Not capabilities — just categories of work. Every product's
roadmap could say this. No persona mapping, no dependencies, no way to score
issues against it.

### Good

> ### Now (Q2 2026)
> - **Automated anomaly detection** — Rules engine flags mileage/fuel
>   discrepancies, non-contiguous jurisdictions, and duplicate entries.
>   Serves: Tax Analyst. Dependencies: Data pipeline cleansing stage must
>   be reliable.
> - **Quarterly filing batch mode** — Generate filings for all clients in one
>   pass with variance warnings. Serves: Tax Analyst, Manager.
>   Dependencies: None (PDF engine exists).

**Why it's good:** Capability-level items (not issue-level). Each names what it
does, who it serves, and what it depends on. Sprint planning can look at
"Automated anomaly detection" and give value-5 to any issue that adds detection
rules or improves the rules engine.

---

## Milestones

### Weak

> - Make users happy by Q3
> - Ship new features by Q4
> - Grow revenue

**Why it's weak:** Not measurable, not tied to capabilities, no checkboxes.
"Make users happy" is an outcome, not a milestone.

### Good

> #### M1: Automated Review Coverage (target: end of Q2 2026)
> - [ ] 80% of known issue types have automated detection rules
> - [ ] Analyst review time per client drops from 45 min to under 30 min
> - [ ] Zero missed non-contiguous jurisdiction gaps in Q2 filings
>
> #### M2: Client Portal MVP (target: Q3 2026)
> - [ ] 3 pilot clients actively using portal for issue resolution
> - [ ] Average issue response time < 48 hours (vs. current 5+ days via email)
> - [ ] Client satisfaction score > 4/5 on portal exit survey

**Why it's good:** Each milestone has a target date and 2-4 concrete,
measurable criteria. The checkbox format makes progress visible. Sprint
planning can identify "vision gaps" — if M1 says "80% of issue types" but
only 30% have detection rules, that is a clear set of issues to create.

---

## Dependencies & Constraints

### Weak

> We have some dependencies on other systems. There are also some resource
> constraints we need to work around.

**Why it's weak:** Says nothing specific. Completely unactionable.

### Good

> ### Technical
> - ELD adapter layer must exist before client self-upload (adapter defines
>   the internal data format that uploads must conform to)
> - Automated review must be reliable (< 5% false positive rate) before
>   client portal goes live (clients should not see bad flags)
>
> ### External
> - Motive API access requires enterprise agreement (in progress, ETA April)
> - Samsara provides a webhook-based integration — requires endpoint deployment
>
> ### Team
> - Single developer (AI-assisted) + product owner — prefer server-rendered
>   UI (Rails/Hotwire) over SPA to reduce frontend complexity
> - Analyst team (3 people) available for UAT 2 hours/week

**Why it's good:** Dependencies are directional (A must happen before B, with
explanation of why). External dependencies name specific vendors and status.
Team constraints explain the reasoning so AI agents make appropriate
architecture decisions.

---

## Design Philosophy

### Weak

> We believe in quality, innovation, and user-centric design.

**Why it's weak:** Every company says this. It resolves zero ambiguity.

### Good

> **Automate the boring, assist the complex.** Repetitive data validation
> should happen without human involvement. Complex judgment calls (is this
> variance a data error or a real change in operations?) should be flagged
> for a human with context, not auto-resolved.

**Why it's good:** A developer facing "should this be automated or flagged?"
can apply this principle directly. It resolves a real tension (full automation
vs. human-in-the-loop) with a clear heuristic.

---

## What This Product is NOT

### Weak

> This product is not everything. We focus on what matters.

**Why it's weak:** Says nothing. What would someone wrongly assume it does?

### Good

> - **Not a general-purpose accounting system.** FM22 handles fuel tax
>   compliance (IFTA, state mileage taxes). Accounts receivable, payroll,
>   and general ledger belong in the client's accounting software.
> - **Not a fleet management platform.** FM22 ingests fleet data (mileage,
>   fuel purchases) but does not manage dispatch, maintenance, or driver
>   scheduling. Integrate with fleet systems, don't replace them.
> - **Not a tax advisory service.** FM22 calculates taxes based on rules and
>   rates. Tax strategy, audit defense, and regulatory interpretation are
>   human responsibilities.

**Why it's good:** Each item names a specific misconception and explains
where that concern IS handled. Prevents AI agents from building features
that belong in other systems.
