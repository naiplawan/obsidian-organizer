---
name: obsidian-organizer
description: "Organize Obsidian notes for AI retrieval. Apply this skill whenever the user mentions organizing, restructuring, or optimizing Obsidian vaults, knowledge bases, or note collections. Use it when users say 'organize my notes', 'make notes AI-friendly', 'restructure for Claude retrieval', 'clean up knowledge base', or when working with MOCs, wikilinks, and vault architecture. This skill transforms scattered notes into atomic, interlinked knowledge optimized for AI assistants, Claude Skills, and RAG systems."
---

# Obsidian Organizer

Transform scattered Obsidian notes into AI-ready knowledge. This skill applies 10 core principles to make notes work well with Claude Skills, RAG systems, and AI assistants.

## Usage Modes

### Quick Mode (Default)
For already-organized vaults that just need enhancement:
1. Add missing frontmatter fields
2. Create wikilinks where missing
3. Add type field to notes

### Full Mode
For scattered notes that need restructuring:
1. Scan and identify problems
2. Split merged notes
3. Create folder structure
4. Apply templates
5. Validate

### One-Off Operations
- "Split this note" → Splits into atomic concepts
- "Add links" → Creates wikilinks between notes
- "Fix frontmatter" → Adds missing fields
- "Create structure" → Sets up folders + templates

---

## Core Philosophy

> **You are no longer organizing notes only for humans.**
> **You are organizing context for AI retrieval.**

AI doesn't care about:
- Beautiful folder trees
- Aesthetic dashboards
- Visual graph views

AI cares about:
- Chunk quality
- Explicit context
- Terminology consistency
- Relationships
- Structured knowledge

---

## Workflow Overview

1. **Quick Scan** — Check what's missing (fast)
2. **Enhance** — Add what's needed (targeted)
3. **Validate** — Verify key checks pass

### Quick Scan (Fast Path)

Instead of comprehensive analysis, focus on what's missing:

```bash
# Fast checks - don't over-analyze
head -5 *.md | grep -c "---"                    # Has frontmatter?
grep -l "^updated:" *.md | wc -l               # Has updated date?
grep -l "\[\[" *.md | wc -l                     # Has wikilinks?
```

**Decision tree:**
- All notes have frontmatter → Skip to links
- Some missing frontmatter → Add only what's missing
- No wikilinks → Add Related sections
- Large files (>800 words) → Flag for potential split

### For Already-Organized Vaults (Skip Full Scan)

If vault already has frontmatter:
1. Check if `updated` field exists on all notes
2. Check if wikilinks exist between related concepts
3. Add what's missing only
4. Report done - don't rebuild what's working

**Time-saving rules:**
- If frontmatter exists, don't regenerate it
- If wikilinks exist, don't add more just for completeness
- If folders exist, use them - don't recreate

### Full Scan (When Needed)

Only do comprehensive scan when:
- Vault has no frontmatter
- No folder structure
- Notes >1500 words with multiple H2s

---

## Step 1: Scan the Vault

Before making changes, understand the current state.

```bash
# List all markdown files
ls -la /path/to/vault
find . -name "*.md" -type f | head -50

# Look for common problems
grep -l "# " *.md                    # Notes with H1 (should use H2+)
grep -l " aliases:" *.md             # Notes missing aliases
grep -l "^date:" *.md               # Notes missing dates
grep -l "\[\[" *.md | wc -l           # Count existing wikilinks
```

**Identify patterns:**
- Large merged notes (>1000 words, multiple topics)
- Inconsistent terminology (auth vs authentication vs login)
- Missing frontmatter (no tags, no dates)
- Orphan notes (no links to/from other notes)
- Temporary context mixed with stable knowledge

---

## Step 2: Analyze Problems

### Problem 1: Merged Notes

Search for notes covering multiple unrelated topics:

```bash
# Find large files
find . -name "*.md" -exec wc -l {} + | sort -rn | head -20
```

**Example of bad:**
```md
# Backend Notes
- Redis
- Kafka
- Docker
- OAuth
- PostgreSQL
```

**Example of good:**
```md
# Redis Cache Invalidation
```

### Problem 2: Inconsistent Terminology

Search for alternate terms:

```bash
grep -r "authentication\|login\|identity" --include="*.md" .
```

Pick ONE canonical term. Add aliases for others.

### Problem 3: Missing Links

```bash
# Find orphan notes (no wikilinks)
for f in *.md; do grep -q "\[\[" "$f" || echo "$f"; done
```

### Problem 4: Poor Titles

```bash
# Find vague titles
grep -l "Interesting Stuff\|Notes\|Thoughts" *.md
```

---

## Step 3: Split Merged Notes

When a note covers multiple concepts, split it into atomic notes.

### Fast Split Pattern

Given a note with multiple H2s (##), extract each H2 section into its own note:

**Input:** Note with ## Authentication, ## Database, ## Caching sections
**Output:** Authentication.md, Database.md, Caching.md + links between them

### Direct Split Template

For each H2 section in the source note:
1. Create new file named after H2 heading
2. Extract content between this H2 and next H2
3. Add frontmatter with tags related to topic
4. Add wikilinks to related concepts

### Example (Before/After)

**Before:** `dev-notes.md` (5 topics)
```md
# Development Notes

## Authentication
We use NextAuth...

## Database
PostgreSQL with Prisma...

## Caching
Redis for sessions...

## Deployment
Docker multi-stage...

## Monitoring
Sentry + Prometheus...
```

**After:** 5 files created

```md
---
title: Authentication
tags: [auth, backend]
type: concept
related: [[Database]], [[Caching]], [[Monitoring]]
---
# Authentication
We use NextAuth...
```

Repeat for each section. Create index note linking them all:

```md
---
title: Development Notes Index
tags: [index, meta]
---
# Development Notes Index

Overview of development infrastructure.

## Concepts
- [[Authentication]] - NextAuth + JWT
- [[Database]] - PostgreSQL + Prisma
- [[Caching]] - Redis patterns
- [[Deployment]] - Docker + K8s
- [[Monitoring]] - Sentry + Prometheus

```md
# NextAuth Setup
tags: [auth, backend]
aliases: [Auth, Authentication]
---

Purpose: User authentication with JWT tokens

## Configuration
\`\`\`ts
// auth.config.ts
providers: [Credentials({...})]
\`\`\`

Related:
- [[JWT Token Refresh]]
- [[Session Management]]
```

### Splitting Guidelines

- One concept per note (200-1000 words ideal)
- Each note should be self-contained
- Use consistent naming: `# Concept Name` not `# Notes`
- Move examples to dedicated files if many exist

---

## Step 4: Apply Structured Templates

### Architecture Note Template

```md
---
title: [Component Name]
tags: [architecture, backend|frontend|mobile]
domain: [payment|auth|notifications]
stack: [postgres, kafka, redis]
created: [YYYY-MM-DD]
updated: [YYYY-MM-DD]
---

# [Component Name]

Purpose: [One sentence what this does]

## Components

| Component | Responsibility |
|-----------|----------------|
| [Name] | [Role] |

## Data Flow

1. [Step 1]
2. [Step 2]
3. [Step 3]

## Failure Modes

- **[Scenario]**: [Impact] → [Mitigation]

## Scaling Concerns

- [Consideration]

## Related

- [[Related Concept 1]]
- [[Related Concept 2]]
```

### Incident Note Template

```md
---
title: [Incident Description]
tags: [incident, resolved]
severity: [critical|high|medium|low]
date: [YYYY-MM-DD]
affected: [system/component]
---

# [Incident Description]

## Symptoms

- [Observable problem]

## Root Cause

[Why it happened]

## Resolution

[How it was fixed]

## Prevention

[How to avoid recurrence]

## Lessons Learned

[What we learned]

## Related

- [[Related Concept]]
```

### Decision Record Template (ADR)

```md
---
title: [Decision Title]
tags: [adr, approved|superseded]
status: [accepted|deprecated|superseded]
date: [YYYY-MM-DD]
---

# [Decision Title]

## Status

[accepted | deprecated | superseded by [[ADR-XXX]]]

## Context

[What prompted this decision]

## Decision

[What we decided]

## Alternatives Considered

| Alternative | Pros | Cons |
|-------------|-----|------|
| [Option A] | [+] | [-] |
| [Option B] | [+] | [-] |

## Consequences

- [Positive outcome]
- [Negative outcome / mitigation]

## Related

- [[Related ADR]]
```

---

## Step 5: Create Wikilinks

### Linking Guidelines

Use wikilinks for internal vault connections:

```md
[[Note Name]]                          Link to note
[[Note Name|Display Text]]             Custom display text
[[Note Name#Heading]]                 Link to heading
[[Note Name#^block-id]]                Link to block
[[#Heading in same note]]             Same-note heading link
```

### Link Types

| Type | Pattern | When |
|------|---------|------|
| Related | `Related:\n- [[Concept]]` | Direct relationship |
| Elaborates | `See [[Concept]] for details` | Builds on another |
| Contrasts | `Unlike [[Concept]], this...` | Difference |
| Depends On | `Requires [[Service]]` | Dependency |

### Linking Strategy

From any note, link to:
- Direct dependencies
- Related patterns
- Opposite/contrasting approaches
- Parent/child concepts

Avoid:
- Too many links (>10 per note confuses retrieval)
- Links to nothing (orphan notes)
- Generic "see also" without specifics

---

## Step 6: Add Frontmatter

### Required Fields

```yaml
---
title: [Clean Title]
tags: [category, subcategory]
created: [YYYY-MM-DD]
updated: [YYYY-MM-DD]
---
```

### Recommended Fields

```yaml
---
title: [Clean Title]
tags:
  - [category]
aliases: [Alternative Name, Another Name]
created: [YYYY-MM-DD]
updated: [YYYY-MM-DD]
type: [concept|incident|adr|runbook|standard]
status: [active|deprecated]
---
```

### Tag Organization

Use flat tags for broad categories, nested for specificity:

```yaml
tags:
  - architecture    # broad
  - architecture/api # specific
```

Common tags:
- `concept` — atomic knowledge
- `incident` — past failures
- `adr` — decisions
- `runbook` — procedures
- `standard` — team conventions
- `pattern` — reusable solutions
- `anti-pattern` — what to avoid

---

## Step 7: Separate Stable vs Temporary

### Recommended Folder Structure

```
/vault
├── /Concepts/           # Atomic knowledge (AI检索 target)
│   ├── /Architecture/
│   ├── /Patterns/
│   └── /Standards/
├── /Incidents/          # Production failures (gold for AI)
├── /Decisions/          # ADRs
├── /Runbooks/           # Operational procedures
├── /Debugging/          # Troubleshooting guides
├── /Projects/           # Project-specific
├── /Glossary/           # Terminology
└── /Archive/           # Temporary/context (deprioritize)
```

### Separation Rules

| Stable (AI优先) | Ephemeral (Archive) |
|----------------|-------------------|
| Architecture | Sprint notes |
| Patterns | Temporary research |
| Standards | Drafts |
| Incidents | Meeting notes |
| Decisions | PoCs |

**Rule:** If note has expiration or becomes outdated, put in `/Archive/` or delete.

---

## Step 8: Validate Structure

After changes, verify the vault is organized.

### Fast Validation (3 checks)

```bash
# 1. Frontmatter check
grep -l "^---" *.md | wc -l    # Should be all

# 2. Link check  
grep -l "\[\[" *.md | wc -l    # Should be most

# 3. Large file check
find . -name "*.md" -exec wc -l {} + | awk '$1 > 1000 {print $2}'
```

### Quality Checklist

- [ ] All notes have frontmatter with tags
- [ ] No notes >1500 words (split if needed)
- [ ] Consistent terminology (one canonical term)
- [ ] All wikilinks resolve
- [ ] No orphan notes
- [ ] Clear titles (searchable names)
- [ ] Stable vs temporary separated
- [ ] Related concepts linked

---

## Principles Summary (Quick Reference)

| # | Principle | Action |
|---|-----------|--------|
| 1 | One concept per note | Split merged notes |
| 2 | Consistent terminology | Pick canonical term, add aliases |
| 3 | Predictable structure | Use templates |
| 4 | Store decisions/tradeoffs | Include WHY in notes |
| 5 | Link like a knowledge graph | Add wikilinks |
| 6 | Prefer insight over docs | Internal lessons, not public docs |
| 7 | Create failure knowledge | Document incidents, bugs |
| 8 | Separate stable vs temporary | Split knowledge from context |
| 9 | Add metadata | Use frontmatter with tags |
| 10 | Design for retrieval | Searchable titles, explicit keywords |

---

## Quick Command Reference

### One-Liner Commands

```bash
# Add updated date to all notes (if missing)
for f in *.md; do sed -i 's/^created:.*/&\nupdated: 2026-05-13/' "$f"; done

# Add type field to notes without it
sed -i 's/^---\n/---\ntype: concept\n/' *.md

# Find large files for splitting
find . -name "*.md" -exec wc -l {} + | sort -rn | head -10

# Count wikilinks per file
for f in *.md; do echo "$(grep -c "\[\[" "$f") $f"; done | sort -rn
```

---

## Example Transformations

### Example 1: Scattered Backend Notes → Structured Concepts

**Before:**
```
backend.md (2500 words, covers auth, DB, caching, deployment)
```

**After:**
```
/Concepts/
├── /Architecture/
│   └── Backend Architecture.md
├── /Architecture/
│   ├── Authentication.md
│   ├── Database Setup.md
│   └── Caching Strategy.md
├── /Patterns/
│   └── Docker Multi-Stage Build.md
├── /Standards/
│   └── API Response Format.md
└── /Decisions/
    └── ADR-001-choose-postgres.md
```

### Example 2: Incident → Incident Note

**Before (slack message):**
```
had a db issue yesterday, deadlock from bad transaction order. fixed by adding retry logic
```

**After:**
```md
---
title: PostgreSQL Deadlock Incident
tags: [incident, database, resolved]
severity: high
date: 2026-01-15
affected: Payment Service
---

# PostgreSQL Deadlock Incident

## Symptoms

- Payment requests hanging
- DB CPU at 20% (not maxed)
-Timeouts after 30s

## Root Cause

Transaction ordering inconsistency between service instances.
Instance A: lock(order) → lock(payment)
Instance B: lock(payment) → lock(order)

## Resolution

Added standardized lock ordering: always acquire locks in alphabetical order.

## Prevention

- Added transaction ordering linter rule
- Documented in [[Database Concurrency Patterns]]
```

---

## Usage

### Trigger Phrases

Use this skill when the user says:
- "organize my notes"
- "make notes AI-friendly"
- "restructure for Claude"
- "clean up knowledge base"
- "optimize for AI retrieval"
- "split this note"
- "add links between these concepts"
- Mentions of "vault", "MOC", "knowledge graph"

### Input

The user should provide:
- Path to the vault/folder
- Any specific problem areas to focus on
- Whether to create new folder structure

### Output

The skill produces:
- Restructured notes with proper frontmatter
- Split notes (if needed)
- Added/modified wikilinks
- New folder structure (if requested
- Summary of changes made

---

## Retrieval Optimization Rules

AI retrieval quality improves when notes contain:

- Explicit nouns instead of pronouns
- Concrete system names
- Error messages verbatim
- Technology names
- Searchable keywords
- Problem + symptom pairs

**Prefer:**
```
PostgreSQL connection pool exhaustion
```

**Over:**
```
database issue
```

**Prefer:**
```
Kubernetes readiness probe timeout
```

**Over:**
```
deployment problem
```

---

## Semantic Density

Good notes maximize:
- Technical specificity
- Causal relationships
- Tradeoffs
- Operational context

**Avoid filler text and narrative storytelling.**

**Bad:**
"We had some issues with the deployment."

**Good:**
"Kubernetes rolling deployment caused 503 spikes due to readiness probe delay exceeding ALB deregistration timeout."

This is one of the biggest hidden factors in RAG quality.

---

## Chunking Rules

Ideal chunk size: **200-800 words**

Split when:
- Multiple unrelated H2 sections
- More than one root concept
- Multiple architectural domains

**Avoid:**
- Giant reference dumps
- Mixed troubleshooting topics
- Long chronological logs

---

## High-Value Knowledge Priority

| Priority | Note Type | Value |
|----------|----------|-------|
| 1 | Incidents | Highest |
| 2 | Architecture decisions | Highest |
| 3 | Debugging paths | High |
| 4 | Failure patterns | High |
| 5 | Tradeoffs | High |
| 6 | Internal conventions | Medium |
| 7 | Copied docs | Low |
| 8 | Tutorials | Low |
| 9 | Meeting summaries | Low |
| 10 | Generic references | Low |

This helps avoid garbage accumulation.

---

## Knowledge Decay Rules

**Archive or update notes when:**
- Technology deprecated
- Architecture replaced
- API changed
- Incident no longer relevant

**Mark stale notes:**
```yaml
status: deprecated
replaced_by: [[New Architecture]]
```

AI systems should deprioritize stale notes. Without this, retrieval quality degrades over time.

---

## RAG Metadata

Add retrieval-centric fields to frontmatter:

```yaml
---
title:
type:
domain:              # e.g., payment, auth, notifications
stack:              # e.g., postgres, kafka, redis
services:            # e.g., payment-service, api-gateway
keywords:            # search terms
status:              # active, deprecated, verified
confidence:          # high, medium, low - how reliable is this info
last_verified:        # YYYY-MM-DD
related:
---
```

**Most important for RAG:** `keywords`, `services`, `confidence`, `last_verified`

---

## Operational Intelligence

Capture in dedicated notes:
- Failure symptoms
- Metrics anomalies
- Error messages verbatim
- Log patterns
- Alert configurations
- Recovery steps
- Escalation paths

These notes are highly valuable for AI troubleshooting.

**Example:**
```md
---
title: Payment Service 503 Errors
keywords: [503, ALB, readiness, timeout]
services: [payment-service, kubernetes]
---

# Payment Service 503 Errors

## Symptoms
- ALB returned 503 during rolling deployment
- Error rate spiked to 15%
- Duration: 2-3 minutes

## Root Cause
readinessProbe.initialDelaySeconds was 10s but app needed 30s cold start.

## Fix
Increased initialDelaySeconds to 35s.
```

---

## Avoid Storing

**Do not store:**
- Raw copied documentation (link instead)
- Temporary AI chats
- Generic tutorials (link instead)
- Low-context snippets
- Duplicated notes
- Vague brainstorming
- Obsolete drafts

This prevents vault entropy.

---

## Naming Conventions

**Prefer:**
- PostgreSQL Connection Pooling
- JWT Refresh Token Flow
- Kubernetes Readiness Probes

**Avoid:**
- DB Stuff
- Auth Notes
- Deployment Ideas

Explicit searchable naming matters more than people think.

---

## Context Window Optimization

Claude Skills perform better when:
- Notes are self-contained
- Assumptions are explicit
- Dependencies are linked
- References are localized

**Avoid requiring AI to traverse 10+ notes to understand one concept.**

---

## Human + AI Co-Design

Notes should be:
- Understandable by humans
- Retrievable by AI
- Maintainable over years

**Do not sacrifice readability purely for embeddings.**

---

## Knowledge Lifecycle

Notes progress through stages:

1. **Capture** — Initial note from incident/research
2. **Refine** — Add context, fix errors
3. **Link** — Connect to related concepts
4. **Validate** — Verify accuracy, update confidence
5. **Retrieve** — Use in practice
6. **Archive/Delete** — Mark stale or remove

**Unmaintained knowledge reduces AI quality.**

---

## Related Skills

- [[obsidian-markdown]] — For creating new notes with proper syntax
- [[obsidian-bases]] — For setting up new vaults from scratch

See [[obsidian-markdown]] for syntax reference (wikilinks, embeds, callouts, properties).