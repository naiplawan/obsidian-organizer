# Obsidian Organizer

**Version 2.3.0** — Reframed as an Obsidian knowledge vault system with seven operating modes and durable documentation contracts

A Claude Skill for building and maintaining structured Obsidian knowledge vaults for humans and AI. It organizes notes, improves retrieval, maintains documentation, reads codebases, creates durable knowledge structures, generates diagrams, and transforms scattered information into a long-term knowledge system.

> Transform scattered notes and existing repositories into atomic, interlinked, evidence-backed knowledge optimized for people first and AI-assisted retrieval.

## What's New in v2.1

- **Brownfield Codebase Documentation** — Read existing repositories and generate implementation-grounded docs
- **Spec Kit-Style Artifacts** — Create `spec.md`, `plan.md`, `tasks.md`, `research.md`, `data-model.md`, contracts, and project constitution docs
- **Evidence Ledger** — Tie documentation claims back to concrete source files and confidence levels
- **Excalidraw Integration** — Generate architecture diagrams, flowcharts, mind maps, timelines
- **Hybrid Knowledge Entries** — Note + diagram pairs with proper embedding
- **Visual Metadata** — `diagram`, `visual_type`, `animation`, `layout` fields
- **Animated Diagram Support** — Sequence ordering for Excalidraw animations

## What's New in v2.2

- **Evidence Research Protocol** — Formal claim registry (`E###`) with confidence grading
- **Claim Reconciliation** — Conflicts between code/docs/tests must be documented before finalizing
- **Validation Checklist** — Brownfield artifacts must pass evidence validation before delivery
- **Brownfield Assertions Safety** — Inferred behavior is clearly labeled and never promoted as observed

## What's New in v2.2.1

- **Human-first output contract** — Response structure now begins with summary, impact, and next actions before evidence details.
- **Readability defaults** — Jargon-reduction, stable headings, and decision-first organization for mixed-audience users.
- **Human usability validation** — Explicit checks for clarity, actionability, and owner/condition on recommended steps.

## What's New in v2.2.2

- **People-first writing defaults** — Topic sentence first, active voice, short sections, and sentence-case headings.
- **Human-facing artifact pattern** — Explicitly includes executive summary, architecture, plans, tasks, and evidence layers.
- **Audience-aware guidance** — Encourages defining audience and writing level before technical detail.

## What's New in v2.2.3

- **Reusable people-review template** — Added a required `## For people` block for non-technical consumption.
- **Artifact section template** — Added consistent section skeleton for Brownfield specs and plans.

## What's New in v2.2.4

- **Copy-paste templates added** — `PROJECT-HOME`, `architecture`, `spec`, `plan`, `tasks`, and `evidence-ledger` templates now included in skill guidance.
- **Human-ready artifact defaults** — Every template includes a person-facing summary + risks + next actions block before technical evidence.

## What's New in v2.2.5

- **Communication modes added** — Explicit Human / Technical / Audit behavior for consistent output.
- **Template mapping matrix** — Enforces minimum required human + technical + evidence sections per artifact.

## What's New in v2.3.0

- **Knowledge vault framing** — Establishes the core principle that a vault is a knowledge system, not a folder tree.
- **Seven operating modes** — Adds Organize Vault, Build Knowledge Graph, Retrieval Optimization, Visual Knowledge, Documentation Builder, Living Documentation, and Codebase Reader.
- **Documentation system guidance** — Adds reusable overview, concept, guide, decision, and runbook templates.
- **Durable metadata contract** — Standardizes required fields for long-term retrieval and maintenance.
- **Output contract** — Requires summary, structure, relationships, and recommendations for every run.

## What It Does

- **Scans** vaults to identify problems (merged notes, inconsistent terms, orphan notes)
- **Splits** large notes into atomic concepts (200-800 words)
- **Adds** RAG metadata (domain, keywords, services, confidence, last_verified)
- **Links** notes with wikilinks between related concepts
- **Applies** templates (incidents, ADRs, runbooks, architecture notes)
- **Marks** stale/deprecated knowledge for lifecycle management
- **Validates** structure with fast checks
- **Reads** brownfield codebases to extract architecture, workflows, contracts, data models, and test strategy
- **Generates** Spec Kit-style documentation grounded in source evidence
- **Maintains** living documentation with stale-claim and open-question tracking

## When to Use

Trigger phrases:
- "organize my notes"
- "make notes AI-friendly"
- "restructure for Claude retrieval"
- "clean up knowledge base"
- "build a second brain"
- "prepare this vault for AI assistants"
- "create living documentation"
- "optimize for AI retrieval"
- "split this note"
- "create diagram"
- "draw architecture"
- "generate Excalidraw"
- "visualize workflow"
- "flowchart"
- "mind map"
- "read this codebase and document it"
- "document this brownfield project"
- "create Spec Kit docs"
- "speckit documentation"
- "generate specs from code"
- "extract architecture from this codebase"
- "create onboarding materials from this codebase"
- "make a plan from the existing code"
- Mentions of "vault", "MOC", "knowledge graph", "Excalidraw", "diagram"

## Core Principles

| # | Principle |
|---|-----------|
| 1 | One concept per note (atomic knowledge) |
| 2 | Consistent terminology (pick canonical term) |
| 3 | Predictable structure (use templates) |
| 4 | Store decisions and tradeoffs (include WHY) |
| 5 | Link like a knowledge graph (wikilinks) |
| 6 | Prefer insight over docs (internal lessons) |
| 7 | Create failure knowledge (document incidents) |
| 8 | Separate stable vs temporary (archive old stuff) |
| 9 | Add metadata (tags, keywords, confidence) |
| 10 | Design for retrieval (searchable titles) |

## RAG Metadata

The skill adds these frontmatter fields:

```yaml
---
title:
type:               # concept, incident, adr, runbook
domain:             # payment, auth, notifications
stack:              # postgres, kafka, redis
services:          # payment-service, api-gateway
keywords:           # search terms
status:            # active, deprecated
confidence:        # high, medium, low
last_verified:      # YYYY-MM-DD
related:           # wiki-links
# v2.0 visual fields
diagram:            # filename.excalidraw
visual_type:        # architecture, flow, timeline, mindmap
animation:          # true, false
layout:             # hierarchy, matrix, freeform
# v2.1 brownfield fields
brownfield:         # true, false
source_paths:       # source files supporting the note
spec_artifact:      # home, constitution, spec, plan, task
evidence_confidence:# high, medium, low
---
```

## Knowledge Priority

| Priority | Type | Value |
|----------|------|-------|
| 1 | Incidents | Highest |
| 2 | Architecture decisions | Highest |
| 3 | Debugging paths | High |
| 4 | Failure patterns | High |
| 5 | Tradeoffs | High |

## Visual Knowledge Priority (v2.0)

| Priority | Type | Value |
|----------|------|-------|
| 1 | Incidents + timeline diagrams | Highest |
| 2 | Architecture + service maps | Highest |
| 3 | ADRs + tradeoff visuals | High |
| 4 | Debugging flows | High |
| 5 | Failure visualizations | High |

## Brownfield Spec Kit-Style Priority (v2.1)

| Priority | Type | Value |
|----------|------|-------|
| 1 | PROJECT-HOME + architecture | Highest |
| 2 | Constitution / engineering rules | Highest |
| 3 | Capability specs | High |
| 4 | Plans and implementation tasks | High |
| 5 | Contracts and data models | High |
| 6 | Evidence ledger and unknowns | High |

## Folder Structure

Recommended vault organization:

```
/vault
├── /Concepts/           # Atomic knowledge
│   ├── /Architecture/
│   ├── /Patterns/
│   └── /Standards/
├── /Diagrams/          # Excalidraw visualizations (v2.0)
│   ├── /Architecture/
│   ├── /Flows/
│   ├── /Incidents/
│   └── /Mindmaps/
├── /Incidents/          # Production failures
├── /Decisions/          # ADRs
├── /Runbooks/           # Operational procedures
├── /Debugging/          # Troubleshooting guides
├── /Glossary/          # Terminology
└── /Archive/           # Deprecated/temporary
```

Brownfield project documentation can also be organized under:

```
/Projects/<Project Name>/
├── PROJECT-HOME.md
├── constitution.md
├── architecture.md
├── glossary.md
├── evidence-ledger.md
├── /specs/
│   └── /<capability-or-feature>/
│       ├── spec.md
│       ├── plan.md
│       ├── tasks.md
│       ├── research.md
│       ├── data-model.md
│       ├── quickstart.md
│       └── /contracts/
├── /Diagrams/
├── /Runbooks/
├── /Decisions/
└── /Archive/
```

## Usage Modes

### Slash Help
Use `/`, `/help`, `/mode`, or `/modes` to ask the skill to show a mode selector:

```text
Obsidian Organizer modes:

1. Knowledge Organization
   Clean up notes, split large files, fix frontmatter, add wikilinks, and improve retrieval metadata.

2. Visual Knowledge Generation
   Create Excalidraw diagrams, architecture maps, flowcharts, timelines, and mind maps.

3. Hybrid Knowledge System
   Combine structured Obsidian notes, linked concepts, metadata, and embedded diagrams.

4. Brownfield Codebase to Spec Kit-Style Docs
   Read an existing repository and generate evidence-backed PROJECT-HOME, constitution, architecture, spec, plan, tasks, contracts, and diagrams.

Reply with 1, 2, 3, or 4, or describe what you want organized.
```

### Quick Mode (Default)
For already-organized vaults - just add what's missing:
- Add missing frontmatter fields
- Create wikilinks where missing
- Mark stale notes

### Full Mode
For scattered notes that need restructuring:
1. Scan and identify problems
2. Split merged notes
3. Create folder structure
4. Apply templates
5. Validate

### One-Off Operations
- "Split this note" → Splits into atomic concepts
- "Add links" → Creates wikilinks
- "Fix frontmatter" → Adds missing fields
- "Create structure" → Sets up folders + templates

### Brownfield Spec Kit Mode
For existing repositories:
1. Scan the codebase read-only
2. Identify architecture, capabilities, contracts, data models, tests, and operational behavior
3. Create an evidence ledger with source paths and confidence levels
4. Generate Spec Kit-style docs: `PROJECT-HOME.md`, `constitution.md`, `architecture.md`, `spec.md`, `plan.md`, `tasks.md`, `research.md`, `data-model.md`, and contracts
5. Add Obsidian wikilinks and retrieval metadata
6. Generate architecture and workflow diagrams where useful
7. Validate that important claims are backed by code evidence

## Knowledge Lifecycle

Notes progress through:

1. **Capture** — Initial note
2. **Refine** — Add context
3. **Link** — Connect to related concepts
4. **Validate** — Verify accuracy
5. **Retrieve** — Use in practice
6. **Archive/Delete** — Mark stale or remove

## Installation

### Option 1: npx (Recommended)

```bash
# Quick install
npx skills add naiplawan/obsidian-organizer
```

### Option 2: Manual

Download the `.skill` file and install via Claude Code settings.

## Related Skills

- [obsidian-markdown](https://github.com/anthropics/claude-code) — For creating new notes with proper syntax
- [obsidian-bases](https://github.com/anthropics/claude-code) — For setting up new vaults from scratch
- [monumentum](https://github.com/anthropics/claude-code) — For turning incidents into visual knowledge entries

## Excalidraw Output Modes (v2.0)

| Trigger | Mode | Format | Usage |
|---------|------|-------|-------|
| `Excalidraw` / `diagram` / `flowchart` | Obsidian | `.md` | Open directly in Obsidian |
| `standard excalidraw` | Standard | `.excalidraw` | Open in excalidraw.com |
| `animate` / `animated diagram` | Animated | `.excalidraw` | Excalidraw animate |

## License

MIT

---

**Philosophy:** This skill organizes notes for people first and AI retrieval second. The key shift is designing for clear human reasoning, then making that clear structure machine-searchable.
