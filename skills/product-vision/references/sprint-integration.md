# Sprint Planning Integration Guide

This reference documents how sprint planning tools can consume a product vision
document to improve issue scoring and prioritization. This is optional — the
vision doc is valuable on its own for AI agents and human alignment.

---

## How Planning Tools Read the Document

The standard vision doc lives at `{REPO_ROOT}/docs/product-vision.md`. Planning
tools should:

1. Read the full markdown file
2. Parse YAML frontmatter for metadata (product name, stage, last updated)
3. Use the narrative content to inform scoring — no enforced schema required

The document is standard GitHub-flavored markdown. No custom syntax, no XML
tags, no special markers needed.

---

## Value Scoring Using the Vision

When scoring issues for sprint selection, the vision doc informs the "value"
dimension. A recommended mapping:

| Value Score | Criteria | Vision Doc Signal |
|-------------|----------|-------------------|
| 5 | Directly advances the vision | Issue closes a gap in "Current State vs Target State" or implements a "Now" roadmap item |
| 4 | Significant workflow improvement | Issue improves a key workflow or serves a primary persona's main pain point |
| 3 | Useful enhancement | Issue serves a persona need but is not on the roadmap |
| 2 | Minor improvement or enabling tech debt | Issue doesn't map to the vision directly but unblocks future vision work |
| 1 | Cosmetic or very low impact | No connection to vision, personas, or roadmap |

### Roadmap horizon mapping

The "Prioritized Roadmap" section has three horizons that map naturally to value:

- **Now** (this quarter) → Issues in this area are value-5 candidates
- **Next** (next 1-2 quarters) → Issues here are value-3 to value-4
- **Later** (6+ months) → Issues here are value-2 unless they also unblock "Now" work

### Vision as tiebreaker

When two issues score similarly on the composite formula, prefer the one that
advances the product vision. A sprint that makes visible progress toward the
vision is worth more than one that clears an equal number of points in
unrelated fixes.

---

## Identifying Vision Gaps

A "vision gap" is a capability described in the vision doc that has no
corresponding GitHub issues. Planning tools can surface these by:

1. Reading the "Current State vs Target State" table
2. Reading the "Prioritized Roadmap" items
3. Reading the "Milestones" checklist items
4. Comparing against open GitHub issues
5. Flagging capabilities/milestones with no matching issues as gaps

Suggest up to 3 vision gaps per planning cycle as "issues to create." These
go in the backlog, not the current sprint.

---

## Key Sections for Planning

Not all sections are equally useful for sprint planning. Priority order:

1. **Vision Statement** — The north star for value-5 scoring
2. **Prioritized Roadmap** — Direct mapping to value scores by horizon
3. **Current State vs Target State** — Gap identification and issue mapping
4. **Success Metrics & Milestones** — Concrete criteria for gap analysis
5. **User Personas** — Ensures balanced investment across user types
6. **Dependencies & Constraints** — Prevents selecting blocked work

The remaining sections (Background, Philosophy, Principles, Workflows,
Architecture, Scope Boundaries) provide context but rarely change scoring
directly.

---

## Staleness Detection

Check the `updated` field in YAML frontmatter. If the vision doc has not been
updated in 90+ days, flag it as potentially stale. Vision docs should be
reviewed at least quarterly — priorities shift, milestones are reached, and
new capabilities emerge.

If the document's `stage` field doesn't match reality (e.g., marked as "build"
but the product is clearly in "growth"), suggest updating it.
