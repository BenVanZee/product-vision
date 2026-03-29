# product-vision

A Claude Code plugin that guides creation and maintenance of structured product vision documents.

## What it does

Runs a phased interview to help you articulate your product's vision, personas, roadmap, and milestones — then writes a structured markdown document that AI agents and sprint planning tools can consume to make better decisions about what to build.

## Install

From the Claude Code plugin marketplace:

```bash
claude plugin add BenVanZee/product-vision
```

Or from a local clone:

```bash
claude plugin add /path/to/product-vision
```

## Usage

The skill triggers when you mention creating, updating, or auditing a product vision:

- **"Create a product vision for this project"** — Guided interview, builds the doc from scratch
- **"Update the product vision"** — Revise specific sections of an existing doc
- **"Audit the vision document"** — Check completeness, specificity, and freshness

Output lands at `docs/product-vision.md` in your project root.

## What's in the vision doc

12 sections covering strategy, priorities, and scope:

1. Background
2. Vision Statement
3. Design Philosophy
4. User Personas
5. Current State vs. Target State
6. Core Principles
7. Key Workflows
8. Prioritized Roadmap (Now / Next / Later)
9. Dependencies & Constraints
10. Integration Architecture
11. What This Product is NOT
12. Success Metrics & Milestones
