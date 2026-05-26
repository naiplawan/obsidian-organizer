# Obsidian Organizer

**Version 2.0** — Now with Excalidraw visualization support

A Claude Skill for organizing Obsidian vaults specifically for AI retrieval, RAG systems, and Excalidraw visual knowledge systems.

> Transform scattered notes into atomic, interlinked knowledge optimized for AI assistants and visual reasoning.

## What's New in v2.0

- **Excalidraw Integration** — Generate architecture diagrams, flowcharts, mind maps, timelines
- **Hybrid Knowledge Entries** — Note + diagram pairs with proper embedding
- **Visual Metadata** — `diagram`, `visual_type`, `animation`, `layout` fields
- **Animated Diagram Support** — Sequence ordering for Excalidraw animations

## What It Does

- **Scans** vaults to identify problems (merged notes, inconsistent terms, orphan notes)
- **Splits** large notes into atomic concepts (200-800 words)
- **Adds** RAG metadata (domain, keywords, services, confidence, last_verified)
- **Links** notes with wikilinks between related concepts
- **Applies** templates (incidents, ADRs, runbooks, architecture notes)
- **Marks** stale/deprecated knowledge for lifecycle management
- **Validates** structure with fast checks

## When to Use

Trigger phrases:
- "organize my notes"
- "make notes AI-friendly"
- "restructure for Claude retrieval"
- "clean up knowledge base"
- "optimize for AI retrieval"
- "split this note"
- "create diagram"
- "draw architecture"
- "generate Excalidraw"
- "visualize workflow"
- "flowchart"
- "mind map"
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

## Usage Modes

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
npx -y @anthropic-ai/claude-code skill add obsidian-organizer

# Or first install CLI globally
npm install -g claude-code
claude skill add obsidian-organizer
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

**Philosophy:** This skill organizes notes not for human browsing, but for AI retrieval. The key shift is designing for semantic search and machine reasoning rather than visual aesthetics.