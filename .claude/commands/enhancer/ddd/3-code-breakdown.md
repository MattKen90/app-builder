---
description: Enhancement DDD Step 3 - Break down implementation into phases
---

# Enhancement DDD Step 3: Code-Breakdown

**Mission**: Break the enhancement into implementation phases. Each phase is buildable, testable, and integrates with existing code.

**Context**: Enhancer version - must integrate with existing codebase patterns.

**Input**:
- `.enhancer/workspaces/{feature}/FEATURE_SPEC.md`
- `.enhancer/workspaces/{feature}/DOCS_DRAFT.md`
- `.enhancer/ARCHITECTURE.md`
- `.enhancer/DISCOVERY.md` (existing patterns)

**Output**:
- `.enhancer/workspaces/{feature}/IMPLEMENTATION_PLAN.md`

---

## Key Differences from Greenfield

| Aspect | Greenfield | Enhancer |
|--------|------------|----------|
| Starting point | Blank slate | Existing code |
| Integration | None | Must integrate cleanly |
| Patterns | Define new | Follow existing |
| Risk | Build wrong | Break existing |

---

## Process

### Step 1: Load Context

Read:
- `FEATURE_SPEC.md` (what to build)
- `DOCS_DRAFT.md` (what users expect)
- `.enhancer/ARCHITECTURE.md` (enhancement approach)
- `.enhancer/DISCOVERY.md` (existing patterns to follow)

### Step 2: Identify Integration Points

From DISCOVERY.md, identify:
- Which existing files need modification
- Which existing patterns to follow
- Which existing code to integrate with

```
🔗 Integration Analysis

Files to modify:
- {file}: {what changes}

Files to create:
- {file}: {purpose}

Patterns to follow:
- {pattern from discovery}

Integration risks:
- {potential issues}
```

### Step 3: Generate Implementation Plan

Create `.enhancer/workspaces/{feature}/IMPLEMENTATION_PLAN.md`:

```markdown
# Implementation Plan: {E-F#} - {Feature Name}

## Overview

**Enhancement**: {brief description}
**Phases**: {number}
**Approach**: {pattern - Core→Enhance→Polish, etc.}

## Integration Map

### Existing Files to Modify
| File | Changes | Risk |
|------|---------|------|
| {path} | {what changes} | Low/Medium/High |

### New Files to Create
| File | Purpose |
|------|---------|
| {path} | {purpose} |

### Patterns to Follow
- {pattern}: {from DISCOVERY.md}

---

## Phase 1: {Phase Name}

### Goal
{One sentence}

### Deliverables
- [ ] {deliverable}
- [ ] {deliverable}

### Integration Points
- Modifies: {existing file}
- Follows: {existing pattern}

### Technical Tasks
1. {task}
2. {task}

### Tests
- [ ] {test case}
- [ ] Existing tests still pass (regression)

### Checkpoint
**Phase 1 complete when:**
- {criterion}
- Existing functionality unchanged

**Validation:**
```bash
{test command}
{regression test command}
```

---

## Phase 2: {Phase Name}

{Same structure}

---

## Risk Areas

| Risk | Mitigation | Phase |
|------|------------|-------|
| Breaking existing code | Run regression tests | All |
| {risk} | {mitigation} | {phase} |

## Success Criteria

Enhancement complete when:
- [ ] All phases complete
- [ ] All tests passing
- [ ] Existing tests still passing
- [ ] Integration verified
- [ ] No regressions
```

### Step 4: Validate Plan

Check:
- [ ] Each phase integrates cleanly
- [ ] Regression testing included
- [ ] Existing patterns followed
- [ ] Risk areas identified

### Step 5: Present Plan

```
🗺️ Enhancement Implementation Plan

Feature: {E-F#} - {Name}

## Phases
Phase 1: {name}
- Modifies: {files}
- Deliverables: {list}

Phase 2: {name}
- Modifies: {files}
- Deliverables: {list}

## Integration Risk: {Low/Medium/High}

Plan: .enhancer/workspaces/{feature}/IMPLEMENTATION_PLAN.md

Options:
- Approve → Proceed to Step 4 (Implement)
- Adjust → I'll revise
- Questions → Let's discuss
```

### Step 6: Handoff

```
✅ Enhancement DDD Step 3 Complete

**Feature**: {E-F#} - {Name}
**Phases**: {N} planned
**Plan**: .enhancer/workspaces/{feature}/IMPLEMENTATION_PLAN.md

Ready for Step 4: Implement

Run: /enhancer/ddd/4
```

---

## Success Criteria

- [x] Integration points identified
- [x] IMPLEMENTATION_PLAN.md created
- [x] Phases include integration steps
- [x] Regression testing planned
- [x] Risk areas identified
- [x] Plan approved
- [x] Ready for /enhancer/ddd/4
