# Product Vision Document Template

This is the full annotated template for vision documents produced by this skill.
Read this file when drafting or auditing a vision doc. HTML comments contain
guidance for each section — they are invisible in rendered markdown but inform
the writing process.

---

## YAML Frontmatter

Every vision doc starts with frontmatter for AI-parseable metadata:

```yaml
---
product: Product Name
updated: YYYY-MM-DD
author: Author Name
stage: build  # discovery | build | growth | mature
---
```

### Stage definitions

| Stage | Meaning | Implications |
|-------|---------|--------------|
| discovery | Exploring problem space, no committed solution | Vision is directional, expect major pivots |
| build | Solution identified, actively building core | Vision is solidifying, roadmap is short-horizon |
| growth | Core works, expanding capabilities and users | Vision is stable, roadmap extends further out |
| mature | Product is established, focus on optimization | Vision focuses on refinement and sustainability |

---

## Section 1: Background

<!-- GUIDANCE:
What this product is, how it came to exist, and what it replaced.
2-4 paragraphs. Write for someone encountering the product for the first time.
Include: what problem it solves, who it serves, what existed before it,
and why the previous solution was insufficient.
Avoid: implementation details, tech stack, or architecture.
-->

### Quality criteria
- A new team member could read this and understand why the product exists
- Mentions the problem, the audience, and the predecessor (if any)
- Does NOT describe how the product works technically

---

## Section 2: Vision Statement

<!-- GUIDANCE:
One paragraph, 2-4 sentences. This is the north star.
Describe the future state — what the product BECOMES, not what it does today.
Write aspirationally but specifically. Avoid vague language like "best in class"
or "world-class platform." Instead, describe concrete capabilities that don't
exist yet.

This is the single most important section for AI agents. Sprint planning tools
use this to determine whether an issue "directly advances the vision" (highest
priority). Make it concrete enough that someone can read a GitHub issue and
say "yes, this moves us toward the vision" or "no, this is maintenance."
-->

### Quality criteria
- Concrete enough to score issues against (not "be the best" but "automate X so users can focus on Y")
- Forward-looking — describes a future state, not the current product
- Fits in one paragraph

---

## Section 3: Design Philosophy

<!-- GUIDANCE:
3-5 short paragraphs or a bulleted list. How decisions get made.
These are the principles that resolve ambiguity when building features.
Example: "Think generic, build specific" or "Automate the boring, assist the complex."
Each philosophy statement should be actionable — a developer should be able to
use it to decide between two implementation approaches.
-->

### Quality criteria
- Each statement resolves a real tension (speed vs. correctness, flexibility vs. simplicity)
- Actionable — not just aspirational platitudes
- 3-5 statements (more dilutes their power)

---

## Section 4: User Personas

<!-- GUIDANCE:
Operational personas, not marketing personas. These describe real people who use
the system today or will use it soon. Each persona needs:
- Name and role (use real names if appropriate, or role-based names)
- Primary goal — what they are trying to accomplish
- Pain points — what frustrates them today
- "Success looks like" — the observable outcome when the product works for them

Format as H3 subheadings per persona. 3-5 personas is ideal.
Fewer than 3 suggests the product may be too narrowly scoped.
More than 5 suggests personas should be consolidated.

AI agents use personas to understand WHO benefits from a feature.
Sprint planning tools can map issues to personas to ensure balanced investment.
-->

### Example format

```markdown
### Analyst (primary: Jane, Pat)
- **Goal:** Process quarterly filings accurately with minimal manual effort
- **Pain:** Manual data entry, hunting for anomalies in spreadsheets
- **Success looks like:** Fewer hours per client per quarter, anomalies flagged automatically
```

### Quality criteria
- Based on real users, not hypothetical archetypes
- Goals are specific to THIS product, not generic ("wants things to work")
- Pain points describe today's reality, not theoretical problems
- Success criteria are observable and measurable

---

## Section 5: Current State vs. Target State

<!-- GUIDANCE:
This is the highest-value section for AI consumption. A table showing where each
major capability is TODAY vs. where the vision takes it.

Use a markdown table with columns: Capability | Today | Target | Gap

"Today" should be honest — if something doesn't exist, say "None" or "Manual."
"Target" should describe the envisioned end state for that capability.
"Gap" is a brief note on the size/nature of the gap (e.g., "Large — requires new
subsystem" or "Small — extend existing module").

This section tells AI agents: "when you see an issue that closes one of these gaps,
it is high-value work." Sprint planning tools can map issues directly to
Today→Target transitions.

Include 6-12 capabilities. Fewer means the vision is too vague.
More means the scope may be too broad — consider grouping.
-->

### Example format

```markdown
| Capability | Today | Target | Gap |
|-----------|-------|--------|-----|
| Data ingestion | CSV import, manual entry | ELD auto-sync, client self-upload | Large — adapter layer needed |
| Data quality | Manual review by analyst | Automated rules flag issues by severity | Medium — rules engine exists, needs coverage |
| Reporting | PDF generation only | Structured JSON + PDF, queryable history | Medium — data model supports it |
```

### Quality criteria
- "Today" column is honest, not aspirational
- "Target" column is concrete, not vague
- Gaps are sized (small/medium/large) so priorities are obvious
- Covers all major product capabilities, not just the exciting ones

---

## Section 6: Core Principles

<!-- GUIDANCE:
Numbered list of 4-8 principles that guide implementation decisions.
These are more specific than Design Philosophy — they are rules about HOW
the product is built, not WHY.

Examples:
- "Client-centric, not mode-centric navigation"
- "Data pipeline processes must be idempotent"
- "Every automated action must have an audit trail"

Each principle should have a brief explanation (1-2 sentences) of why it exists
and what violation looks like.
-->

### Quality criteria
- Each principle is falsifiable — you can point to code that violates it
- Explanations include the "why" so developers can apply judgment in edge cases
- 4-8 principles (fewer is too abstract, more becomes a style guide)

---

## Section 7: Key Workflows

<!-- GUIDANCE:
The major user journeys through the product. Write these as narratives or
numbered steps — not technical specs.

Each workflow should cover:
- Who initiates it (which persona)
- What triggers it (time-based, event-based, user-initiated)
- The happy path (what happens when everything works)
- Key decision points (where a human makes a judgment call)

3-6 workflows is typical. These are the flows that, if broken, mean the product
is not working.

Product-specific: a tax platform may have a data pipeline, a document system
may have a lifecycle workflow, a CRM has a sales funnel. Name them after what
the user experiences, not the technical implementation.
-->

### Quality criteria
- Written from the user's perspective, not the system's
- Covers the critical paths (not every edge case)
- Decision points are identified — these often become features

---

## Section 8: Prioritized Roadmap

<!-- GUIDANCE:
Three horizons, each with concrete items:

### Now (this quarter)
Actively building. These represent the highest-priority work.

### Next (next 1-2 quarters)
Planned and scoped but not started. Dependencies on "Now" work should be noted.

### Later (6+ months)
Directional. Not committed. May change as the product evolves.

Each item should include:
- Capability name
- Brief description (1-2 sentences)
- Which persona it primarily serves
- Dependencies (what must be done first)

Sprint planning tools use this section to calibrate value scores:
- "Now" items signal highest priority work
- "Next" items are medium priority
- "Later" items are lower priority but represent the direction

Keep items at the capability level, not the issue level. "Automated data review"
is a roadmap item. "Add validation rule for negative mileage" is an issue.
-->

### Quality criteria
- "Now" has 2-4 items (more means nothing is actually prioritized)
- "Next" has 3-6 items
- "Later" can be more expansive but still scoped
- Dependencies between items are explicit
- Each item names which persona benefits

---

## Section 9: Dependencies & Constraints

<!-- GUIDANCE:
What blocks what. Organized by category:

### Technical
Internal dependencies between capabilities or systems.
"X must exist before Y can be built."

### External
Dependencies on third parties, APIs, vendors, or other teams.
"Requires access to Motive API for ELD data."

### Team / Resource
Capacity constraints, skill gaps, or organizational factors.
"Single developer + AI — prefer server-rendered over SPA."

### Business
Budget, compliance, timeline, or contractual constraints.
"Must maintain backwards compatibility with legacy export format through Q4."

This section prevents sprint planning from selecting work that is blocked.
It also helps AI agents understand why certain approaches are preferred.
-->

### Quality criteria
- Dependencies are directional (A blocks B, not just "A and B are related")
- External dependencies name the specific system/vendor/API
- Constraints explain WHY they exist, not just WHAT they are

---

## Section 10: Integration Architecture

<!-- GUIDANCE:
How this product connects to other systems. What it owns vs. what it delegates.

Include:
- Systems this product sends data TO
- Systems this product receives data FROM
- Shared databases or APIs
- Authentication/authorization boundaries

A simple list or diagram is fine. This section helps AI agents understand the
product's boundaries — what is in scope to change vs. what is an external contract.
-->

### Quality criteria
- Clear ownership boundaries (what this product controls vs. what it consumes)
- Integration points are named specifically (not "external systems")
- Direction of data flow is clear

---

## Section 11: What This Product is NOT

<!-- GUIDANCE:
Scope boundaries. 3-6 bullet points of things this product explicitly does NOT do.
Each should be something someone might reasonably assume it does.

Format: "This product is NOT a [thing]. [Brief explanation of why not or what IS.]"

This section prevents feature creep and helps AI agents avoid building the wrong
thing. It is especially valuable when the product's name or domain could imply
broader scope than intended.
-->

### Quality criteria
- Each item is something someone might actually request or assume
- Explains what the product IS instead (or where that concern is handled)
- Not a laundry list — only the most common misconceptions

---

## Section 12: Success Metrics & Milestones

<!-- GUIDANCE:
Two parts:

### Metrics
Ongoing measures of product health. How do we know the product is working?
These are evergreen — they don't have a target date.
Examples: "Average processing time per client," "Percentage of issues caught automatically."

### Milestones
Phased, measurable checkpoints tied to roadmap horizons.
Use checkbox format so progress is visible at a glance.
Each milestone should have a target date and 2-4 concrete criteria.

Sprint planning tools use milestones to identify "vision gaps" — if a milestone
criterion doesn't have corresponding GitHub issues, that is a gap worth filling.
-->

### Example format

```markdown
### Metrics
- Average analyst hours per client per quarter
- Percentage of known issue types with automated detection
- Client self-service resolution rate

### Milestones

#### M1: Automated Review Coverage (target: Q2 2026)
- [ ] 80% of known issue types have automated detection rules
- [ ] Analyst review time per client drops by 30%

#### M2: Client Portal MVP (target: Q3 2026)
- [ ] 3 pilot clients using portal for issue resolution
- [ ] Average response time < 48 hours
```

### Quality criteria
- Metrics are measurable (not "user satisfaction" without defining how)
- Milestones have target dates
- Milestone criteria use checkboxes for trackability
- Milestones map to roadmap horizons (M1 → Now, M2 → Next, etc.)

---

## Section Order

The sections above are listed in the recommended order. This order optimizes for
AI agents that may process the document top-to-bottom:

1. **Background** — establish context
2. **Vision Statement** — the north star (first thing a planning tool needs)
3. **Design Philosophy** — how decisions get made
4. **User Personas** — who cares
5. **Current State vs. Target State** — where we are vs. where we're going
6. **Core Principles** — implementation rules
7. **Key Workflows** — critical user journeys
8. **Prioritized Roadmap** — what order to build
9. **Dependencies & Constraints** — what blocks what
10. **Integration Architecture** — system boundaries
11. **What This Product is NOT** — scope boundaries
12. **Success Metrics & Milestones** — how we know it's working
