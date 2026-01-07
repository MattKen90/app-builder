---
description: Enhancement DDD Step 2 - Document the enhancement before coding
---

# Enhancement DDD Step 2: Document

**Mission**: Write documentation for the enhancement BEFORE coding. Document what we're about to build.

**Context**: Enhancer version - all paths use `.enhancer/` beachhead.

**Input**:
- `.enhancer/workspaces/{feature}/FEATURE_SPEC.md`
- `.enhancer/DISCOVERY.md` (existing patterns)

**Output**:
- `.enhancer/workspaces/{feature}/DOCS_DRAFT.md`

---

## Key Differences from Greenfield

| Aspect | Greenfield | Enhancer |
|--------|------------|----------|
| Workspace | `.ddd_workspaces/` | `.enhancer/workspaces/` |
| Context | Fresh docs | Integrate with existing docs |
| Patterns | Define new | Follow existing (from DISCOVERY.md) |

---

## Process

### Step 1: Load Context

Read:
- `FEATURE_SPEC.md` (what we're building)
- `.enhancer/DISCOVERY.md` (existing patterns and docs)

### Step 2: Write DOCS_DRAFT.md

Create `.enhancer/workspaces/{feature}/DOCS_DRAFT.md`:

```markdown
# {Enhancement Feature Name}

{One sentence: What this enhancement adds}

## Overview

{What this enhancement does, how it integrates with existing functionality}

## Integration

**Connects to**: {Existing code/features this enhances}
**Follows patterns from**: {Patterns identified in DISCOVERY.md}

## Quick Start

{How to use this enhancement}

## Features

### {Sub-feature 1}
{Description and usage}

### {Sub-feature 2}
{Description and usage}

## Configuration

{Any configuration options}

## Examples

{Working examples}

## Troubleshooting

{Common issues}

---

*Enhancement ID: {E-F#}*
```

### Step 3: Integration Check

Verify documentation:
- References existing features correctly?
- Follows existing documentation style?
- Examples use existing patterns?

### Step 4: Handoff

```
✅ Enhancement DDD Step 2 Complete

**Feature**: {E-F#} - {Name}
**Draft**: .enhancer/workspaces/{feature}/DOCS_DRAFT.md

Ready for Step 3: Code-Breakdown

Run: /enhancer/ddd/3
```

---

## Success Criteria

- [x] FEATURE_SPEC.md loaded
- [x] DISCOVERY.md patterns referenced
- [x] DOCS_DRAFT.md created
- [x] Integrates with existing documentation style
- [x] State updated
- [x] Ready for /enhancer/ddd/3
