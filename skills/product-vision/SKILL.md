---
name: product-vision
version: 0.1.0
description: >
  This skill should be used when the user asks to "create a product vision",
  "write a vision doc", "update the product vision", "audit the vision document",
  "review the product vision", "build a vision document", or mentions
  "product-vision.md". Guides creation and maintenance of structured product
  vision documents that serve as strategic context for AI agents, sprint
  planning tools, and human alignment.
---

# Product Vision Skill

Create and maintain structured product vision documents that make AI better at
building your product. The output is a markdown file at `docs/product-vision.md`
that serves as the strategic north star for feature development.

## What the Vision Doc Does

A product vision document answers three questions:
1. **Where are we going?** (Vision, Roadmap, Milestones)
2. **Who are we building for?** (Personas, Workflows)
3. **Where are we today?** (Current State vs Target State, Constraints)

AI agents read this document when building features to understand strategic
context. Sprint planning tools can consume it to score issues by vision
alignment. Humans use it to align on priorities and scope.

## Output Location

Write the vision document to `docs/product-vision.md` in the project root.
Create the `docs/` directory if it does not exist. This path is the standard
location that AI agents and planning tools look for.

## Three Modes

### Create Mode

Trigger: No `docs/product-vision.md` exists, or user asks to create one.

Run a phased interview. Each phase asks 2-4 focused questions, then drafts
its sections so the user sees progress incrementally. Do not ask all questions
upfront — show written output after each phase.

**Phase 1: Discovery**
Read existing repo context before asking anything. Check: CLAUDE.md, README,
any files in `docs/`, and the project structure. Pre-populate what the codebase
already answers. Note what is missing.

**Phase 2: Vision & Identity**
Ask about: What does this product do? Who is it for? Where is it going?
Draft: Background, Vision Statement, User Personas.

**Phase 3: Philosophy & Principles**
Ask about: What are the hard rules? What patterns guide decisions?
Draft: Design Philosophy, Core Principles.

**Phase 4: State & Gaps**
Ask about: What works today? What is painful? What is the dream state?
Draft: Current State vs Target State, Key Workflows.

**Phase 5: Prioritization**
Ask about: What matters most right now? What depends on what? What are the
concrete milestones?
Draft: Prioritized Roadmap, Dependencies & Constraints, Success Metrics &
Milestones.

**Phase 6: Boundaries**
Ask about: What is this product NOT? What do people wrongly assume it does?
Draft: What This Product is NOT, Integration Architecture.

**Phase 7: Assembly & Review**
Assemble the full document. Present it for review. Iterate on feedback.
Write the final version to `docs/product-vision.md`.

**Phase 8: CLAUDE.md Integration**
Check the project's CLAUDE.md for a reference to `docs/product-vision.md`.
If missing, add a section:

```markdown
## Product Vision
Read `docs/product-vision.md` for strategic context when planning features
or evaluating priorities.
```

### Update Mode

Trigger: `docs/product-vision.md` exists and user asks to update it.

1. Read the current vision document completely.
2. Ask what changed or what sections need attention.
3. Update specific sections, preserving content that is still accurate.
4. Update the `updated` date in YAML frontmatter.
5. Check CLAUDE.md reference (add if missing).

### Audit Mode

Trigger: User asks to audit, review, or check the vision document.

1. Read the current vision document.
2. Read `references/template.md` for the expected section list and quality
   criteria.
3. Read `references/examples.md` to calibrate what "good" and "weak" look
   like for each section type.
4. Check each section for:
   - **Presence** — is the section there?
   - **Specificity** — is it concrete enough to score issues against?
   - **Freshness** — does it reflect the current state of the product?
   - **Measurability** — are metrics and milestones specific and dated?
5. Produce a report with ratings and specific recommendations.
6. Offer to fix issues interactively.

## Document Structure

The vision doc has 12 sections plus YAML frontmatter. Read
`references/template.md` for the full annotated template with guidance and
quality criteria per section. The sections in order:

1. **Background** — What this product is and why it exists
2. **Vision Statement** — The north star (most important for AI consumption)
3. **Design Philosophy** — How decisions get made
4. **User Personas** — Who uses it and what they care about
5. **Current State vs Target State** — Gap analysis table (highest value for AI)
6. **Core Principles** — Implementation rules
7. **Key Workflows** — Critical user journeys
8. **Prioritized Roadmap** — Now / Next / Later horizons
9. **Dependencies & Constraints** — What blocks what
10. **Integration Architecture** — System boundaries
11. **What This Product is NOT** — Scope boundaries
12. **Success Metrics & Milestones** — Measurable checkpoints

## Quality Standards

Read `references/examples.md` for annotated good-vs-weak examples. Key
quality tests:

- **Vision Statement:** Can someone read a GitHub issue and determine whether
  it advances this vision? If not, it is too vague.
- **Personas:** Are they based on real people with specific goals, or generic
  archetypes? Real people with measurable success criteria.
- **Current vs Target:** Is "Today" honest? Is "Target" concrete? Are gaps
  sized? All three must be true.
- **Roadmap:** Does "Now" have 2-4 items (not 10)? Are dependencies explicit?
  Does each item name which persona benefits?
- **Milestones:** Do they have target dates, checkboxes, and measurable
  criteria? Vague milestones are worse than none.

## Sprint Planning Integration

The vision doc format is designed to be consumed by sprint planning tools.
For details on how planning tools map the document to value scoring, read
`references/sprint-integration.md`. This integration is optional — the
vision doc is valuable on its own.

## Interview Guidelines

When running the phased interview in Create mode:

- **Read before asking.** Phase 1 (Discovery) should eliminate questions the
  codebase already answers. Do not ask the user to re-state what is in the
  README or CLAUDE.md.
- **Draft after each phase.** Show the user written sections after each phase,
  not all at the end. They should see progress and can course-correct early.
- **Ask focused questions.** 2-4 questions per phase. Frame them as
  conversations, not forms. Suggest answers when context is available.
- **Push for specificity.** If the user gives a vague answer ("make it better"),
  ask follow-up questions to make it concrete. Reference examples from
  `references/examples.md` to calibrate.
- **Respect the user's voice.** The vision doc should sound like the user,
  not like a template. Use their terminology and frame things the way they
  described them.
