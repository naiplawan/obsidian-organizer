---
name: obsidian-organizer
description: "Organize Obsidian notes for AI retrieval and generate Excalidraw visualizations. Apply this skill whenever the user mentions organizing, restructuring, optimizing, visualizing, diagramming, or improving Obsidian vaults, knowledge bases, workflows, architectures, or note collections. Use it when users say 'organize my notes', 'make notes AI-friendly', 'restructure for Claude retrieval', 'clean up knowledge base', 'create diagrams', 'draw architecture', 'generate Excalidraw', 'visualize workflow', 'flowchart', 'mind map', or when working with MOCs, wikilinks, vault architecture, and visual knowledge systems. This skill transforms scattered notes into atomic, interlinked knowledge optimized for AI assistants, Claude Skills, RAG systems, and Excalidraw-based visual retrieval."
metadata:
  version: 2.0.0
  capabilities:
    - obsidian-organization
    - rag-optimization
    - wikilink-generation
    - frontmatter-standardization
    - knowledge-graph-optimization
    - excalidraw-generation
    - architecture-visualization
    - animated-diagrams
---

# Obsidian Organizer + Excalidraw Visual Knowledge System

Transform scattered Obsidian notes into AI-ready, visually connected knowledge systems.

This skill combines:

* Structured Obsidian organization
* AI retrieval optimization
* RAG-friendly metadata
* Excalidraw visualization generation
* Architecture and workflow diagrams
* Visual concept mapping

---

# Core Philosophy

> You are no longer organizing notes only for humans.
> You are organizing structured context for AI retrieval and visual reasoning.

AI systems benefit from:

* Atomic knowledge
* Explicit relationships
* Semantic consistency
* Structured metadata
* Visual representations
* Diagram-based contextual understanding

This skill optimizes both:

1. Text retrieval
2. Visual comprehension

---

# Unified Workflow

## Mode 1 — Knowledge Organization

Used for:

* Vault cleanup
* RAG optimization
* Frontmatter fixes
* Wikilink creation
* Note splitting
* Folder restructuring

## Mode 2 — Visual Knowledge Generation

Used for:

* Architecture diagrams
* Flowcharts
* Mind maps
* Relationship maps
* Timelines
* Animated Excalidraw exports

## Mode 3 — Hybrid Knowledge System (Recommended)

Combines:

1. Structured notes
2. Linked concepts
3. Excalidraw visualizations
4. Embedded diagrams
5. Retrieval metadata

Recommended for:

* Engineering knowledge bases
* Architecture documentation
* Incident management systems
* ADR repositories
* Operational intelligence vaults

---

# Trigger Detection

## Organization Triggers

* organize my notes
* optimize for AI retrieval
* restructure vault
* split this note
* add wikilinks
* fix frontmatter
* clean up knowledge base
* make AI-friendly

## Excalidraw / Visualization Triggers

* Excalidraw
* diagram
* architecture diagram
* flowchart
* mind map
* visualize
* workflow diagram
* flowchart
* mind map
* visualization
* standard excalidraw
* animate
* animated diagram
* Excalidraw animation

---

# Excalidraw Integration

## Output Modes

| Trigger                          | Mode     | Format      | Usage                       |
| -------------------------------- | -------- | ----------- | --------------------------- |
| Excalidraw / diagram / flowchart | Obsidian | .md         | Open directly in Obsidian   |
| standard excalidraw              | Standard | .excalidraw | Open in excalidraw.com      |
| animate / animated diagram       | Animated | .excalidraw | Use with excalidraw-animate |

---

# Diagram Type Selection Guide

| Type         | Use Case                         |
| ------------ | -------------------------------- |
| Flowchart    | Workflows, execution paths       |
| Mind Map     | Idea expansion, concept grouping |
| Hierarchy    | Systems, org structures          |
| Relationship | Dependencies, interactions       |
| Timeline     | Incidents, migrations, history   |
| Matrix       | Prioritization, comparisons      |
| Architecture | Services, infrastructure         |
| Freeform     | Brainstorming                    |

---

# Hybrid Knowledge Design Rules

## Every Major Concept Should Have:

1. Atomic markdown note
2. Metadata-rich frontmatter
3. Wikilinks
4. Related diagram
5. Searchable keywords
6. Stable naming

---

# Visual Knowledge Rules

## Excalidraw Standards

### Text Rules

* Use `fontFamily: 5`
* Minimum readable sizes:

  * Title: 20-28px
  * Body: 16-18px
  * Notes: 14px minimum
* Replace:

  * `"` → `『』`
  * `()` → `「」`

### Layout Rules

* Canvas: 0-1200 x 0-800
* Minimum spacing: 20px
* Padding: 50px minimum
* Avoid overlaps
* Avoid emoji usage

### Color Palette

#### Text Colors

| Purpose  | Color   |
| -------- | ------- |
| Title    | #1e40af |
| Subtitle | #3b82f6 |
| Body     | #374151 |
| Emphasis | #f59e0b |

#### Fill Colors

| Semantic   | Color   |
| ---------- | ------- |
| Primary    | #a5d8ff |
| Success    | #b2f2bb |
| Warning    | #ffd8a8 |
| Processing | #d0bfff |
| Critical   | #ffc9c9 |
| Planning   | #fff3bf |
| Data       | #c3fae8 |
| Analytics  | #eebefa |

---

# Visual Retrieval Optimization

## Diagrams Must:

* Reflect semantic structure
* Use explicit labels
* Show causal relationships
* Surface dependencies
* Match note terminology exactly

## Avoid:

* Ambiguous labels
* Decorative-only diagrams
* Inconsistent naming
* Overcrowded layouts

---

# Excalidraw JSON Requirements

## Required Structure

```json
{
  "type": "excalidraw",
  "version": 2,
  "source": "https://github.com/zsviczian/obsidian-excalidraw-plugin",
  "elements": [],
  "appState": {
    "gridSize": null,
    "viewBackgroundColor": "#ffffff"
  },
  "files": {}
}
```

## Required Element Fields

```json
{
  "id": "unique-id",
  "type": "rectangle",
  "x": 100,
  "y": 100,
  "width": 200,
  "height": 50,
  "angle": 0,
  "strokeColor": "#1e1e1e",
  "backgroundColor": "transparent",
  "fillStyle": "solid",
  "strokeWidth": 2,
  "strokeStyle": "solid",
  "roughness": 1,
  "opacity": 100,
  "groupIds": [],
  "roundness": {"type": 3},
  "seed": 123456,
  "version": 1,
  "isDeleted": false,
  "boundElements": null,
  "updated": 1,
  "link": null,
  "locked": false
}
```

---

# Diagram Embedding Strategy

## Recommended Pattern

Each major concept note should embed diagrams.

Example:

```md
---
title: Authentication Architecture
tags: [architecture, auth]
type: concept
---

# Authentication Architecture

![[authentication-flow.excalidraw]]

## Overview

JWT-based authentication flow.

## Related

- [[Session Management]]
- [[JWT Refresh Flow]]
```

---

# Organizational Workflow

## Step 1 — Quick Scan

Check:

* Frontmatter
* Wikilinks
* Large files
* Missing metadata
* Existing diagrams

## Step 2 — Structural Optimization

* Split large notes
* Normalize terminology
* Add metadata
* Create links

## Step 3 — Visual Extraction

Generate diagrams for:

* Architecture
* Incident timelines
* Data flow
* Service dependencies
* Debugging flows
* Operational procedures

## Step 4 — Diagram Linking

Connect:

* Notes ↔ diagrams
* Concepts ↔ architecture
* Incidents ↔ timelines
* ADRs ↔ tradeoff visuals

## Step 5 — Validation

Verify:

* Links resolve
* Diagrams open correctly
* Naming consistency
* Retrieval metadata quality

---

# Recommended Vault Structure

```text
/vault
├── /Concepts
│   ├── /Architecture
│   ├── /Patterns
│   └── /Standards
├── /Diagrams
│   ├── /Architecture
│   ├── /Flows
│   ├── /Incidents
│   └── /Mindmaps
├── /Incidents
├── /Decisions
├── /Runbooks
├── /Projects
├── /Glossary
└── /Archive
```

---

# Visual Incident Intelligence

High-value incidents should include:

1. Incident note
2. Timeline diagram
3. Failure flow visualization
4. Recovery sequence
5. Dependency graph

Example:

```md
# PostgreSQL Deadlock Incident

![[postgres-deadlock-timeline.excalidraw]]

## Symptoms

- Transaction timeout
- CPU spike
- Retry storm

## Root Cause

Inconsistent lock acquisition ordering.
```

---

# Animated Diagram Support

## Animation Order Strategy

Recommended sequence:

1. Title
2. Main containers
3. Relationships
4. Supporting labels
5. Detailed annotations

Example:

```json
"customData": {
  "animate": {
    "order": 1,
    "duration": 500
  }
}
```

---

# Retrieval Optimization Rules

## Prefer Explicit Technical Terms

Prefer:

* PostgreSQL Connection Pool Exhaustion
* Kubernetes Readiness Probe Timeout
* JWT Refresh Token Rotation

Avoid:

* DB issue
* deployment problem
* auth stuff

---

# Metadata Standards

```yaml
---
title:
type:
domain:
stack:
services:
keywords:
status:
confidence:
last_verified:
related:
diagram:
visual_type:
---
```

## New Visual Metadata Fields

| Field       | Purpose                        |
| ----------- | ------------------------------ |
| diagram     | Related Excalidraw file        |
| visual_type | architecture / flow / timeline |
| animation   | true/false                     |
| layout      | hierarchy / matrix / freeform  |

---

# Knowledge Graph + Visual Graph

The vault should function as:

1. Semantic graph
2. Visual graph
3. Retrieval graph
4. Operational intelligence system

Diagrams should reinforce retrieval structure.

---

# Common Mistakes

## Organization Mistakes

* Giant mixed-topic notes
* Missing metadata
* Broken wikilinks
* Generic titles
* Stale knowledge

## Excalidraw Mistakes

* Tiny unreadable text
* Overlapping elements
* Low contrast colors
* Missing padding
* Decorative diagrams without semantics

---

# Output Requirements

## For Organization Tasks

Provide:

* Files modified
* Metadata added
* Notes split
* Links created
* Structure changes

## For Diagram Tasks

Provide:

* Diagram type selected
* File path
* Output format
* Embedding instructions
* Animation details if applicable

---

# Example Hybrid Output

```text
Generated:
- Authentication.md
- JWT Refresh Flow.md
- authentication-architecture.excalidraw
- auth-dependency-map.excalidraw

Changes:
- Added frontmatter
- Added wikilinks
- Split monolithic backend.md
- Created architecture visualization
- Added retrieval metadata
```

---

# High-Value Knowledge Priority

| Priority | Type                   |
| -------- | ---------------------- |
| 1        | Incidents              |
| 2        | Architecture diagrams  |
| 3        | ADRs                   |
| 4        | Debugging flows        |
| 5        | Failure visualizations |
| 6        | Operational runbooks   |
| 7        | Generic references     |

---

# Final Principle

> Great AI knowledge systems are both semantically structured and visually navigable.

Text explains.

Diagrams compress complexity.

Together they create high-quality retrieval systems for humans and AI.
