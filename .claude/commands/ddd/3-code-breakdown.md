---
description: DDD Step 3 - Break down implementation into phases with checkpoints
---

# DDD Step 3: Code-Breakdown

**Mission**: Break the feature into implementation phases. Each phase is a buildable, testable unit with clear deliverables.

**Mode-Aware**: Reads `.state.json` to determine paths. In enhancer mode, phases include integration planning.

---

## Mode Detection

| Resource | Greenfield | Enhancer |
|----------|------------|----------|
| Workspaces | `.ddd_workspaces/` | `.enhancer/workspaces/` |
| Architecture | `ARCHITECTURE.md` | `.enhancer/ARCHITECTURE.md` |
| Extra context | - | `.enhancer/DISCOVERY.md` (integration points) |

---

**Input** (paths depend on mode):
- `{WORKSPACE_PATH}/{feature}/FEATURE_SPEC.md`
- `{WORKSPACE_PATH}/{feature}/DOCS_DRAFT.md`
- `{ARCHITECTURE_PATH}`
- `{DISCOVERY_PATH}` (enhancer mode: existing patterns to follow)

**Output**:
- `{WORKSPACE_PATH}/{feature}/IMPLEMENTATION_PLAN.md`

---

## Why Break Down Before Coding?

1. **Incremental validation** - Test assumptions early, adjust as you learn
2. **Vertical slices** - End-to-end functionality at each phase (not horizontal layers)
3. **Checkpoints** - Know when each phase succeeds before moving on
4. **Reduced risk** - Catch problems early, not at the end

---

## Process

### Step 1: Load Context

Read:
- `FEATURE_SPEC.md` (what to build)
- `DOCS_DRAFT.md` (what users expect)
- `ARCHITECTURE.md` (technical patterns)

Identify:
- Core functionality that must work
- Dependencies between components
- Risk areas (unknowns, complexity)
- Testing requirements

### Step 2: Identify Build Phases

Break feature into 2-4 phases. Each phase should:
- Deliver working functionality (not just "setup")
- Be testable independently
- Build on previous phase
- Take ~15-30 minutes to implement

**Phase Breakdown Patterns:**

**Pattern A: Core → Enhance → Polish**
- Phase 1: Minimal working version
- Phase 2: Full functionality
- Phase 3: Edge cases and polish

**Pattern B: Data → Logic → Interface**
- Phase 1: Data model and storage
- Phase 2: Business logic
- Phase 3: User interface/API

**Pattern C: Happy Path → Errors → Edge Cases**
- Phase 1: Main success scenario
- Phase 2: Error handling
- Phase 3: Edge cases and validation

Choose pattern based on feature type.

### Step 3: Generate Implementation Plan

Create `.ddd_workspaces/{feature}/IMPLEMENTATION_PLAN.md`:

```markdown
# Implementation Plan: {Feature ID} - {Feature Name}

## Overview

**Feature**: {brief description}
**Phases**: {number}
**Approach**: {which pattern and why}

---

## Phase 1: {Phase Name}

### Goal
{One sentence: What this phase achieves}

### Deliverables
- [ ] {Concrete deliverable 1}
- [ ] {Concrete deliverable 2}
- [ ] {Concrete deliverable 3}

### Technical Tasks
1. {Specific task}
2. {Specific task}
3. {Specific task}

### Files to Create/Modify
- `{path/to/file}`: {what changes}
- `{path/to/file}`: {what changes}

### Tests
- [ ] {Test case 1}
- [ ] {Test case 2}

### Checkpoint
**Phase 1 is complete when:**
- {Specific verifiable condition}
- {Specific verifiable condition}

**Validation command:**
```bash
{command to verify phase works}
```

---

## Phase 2: {Phase Name}

### Goal
{One sentence: What this phase achieves}

### Deliverables
- [ ] {Concrete deliverable 1}
- [ ] {Concrete deliverable 2}

### Technical Tasks
1. {Specific task}
2. {Specific task}

### Files to Create/Modify
- `{path/to/file}`: {what changes}

### Tests
- [ ] {Test case 1}
- [ ] {Test case 2}

### Checkpoint
**Phase 2 is complete when:**
- {Specific verifiable condition}
- Phase 1 still works (regression check)

**Validation command:**
```bash
{command to verify phase works}
```

---

## Phase N: {Final Phase}

{Same structure}

---

## Risk Areas

| Risk | Mitigation | Phase |
|------|------------|-------|
| {potential problem} | {how to handle} | {when it appears} |

## Dependencies

- **External**: {libraries, APIs, services needed}
- **Internal**: {other features or code this depends on}

## Success Criteria

Feature is complete when:
- [ ] All phases complete
- [ ] All tests passing
- [ ] Documentation matches implementation
- [ ] No regressions in existing features
```

### Step 4: Validate Plan Quality

Check the plan against these criteria:

**Vertical Slices:**
- Does each phase deliver working functionality?
- ❌ Bad: "Phase 1: Set up database schema"
- ✅ Good: "Phase 1: User can create and save one record"

**Testability:**
- Is there a concrete way to verify each phase?
- Can you run a command and see it works?

**Incremental:**
- Does Phase 2 build on Phase 1?
- Could you stop after Phase 1 and have something useful?

**Right-Sized:**
- Is each phase ~15-30 minutes of work?
- If longer, break it down further

### Step 5: Present to User

```
🗺️ Implementation Plan Complete

Feature: {Feature ID} - {Feature Name}

## Build Phases

Phase 1: {name} (~{time})
  - {key deliverable}
  - {key deliverable}

Phase 2: {name} (~{time})
  - {key deliverable}
  - {key deliverable}

Phase 3: {name} (~{time})
  - {key deliverable}

---

## Plan Quality

✅ Vertical slices (each phase delivers working functionality)
✅ Testable (concrete validation at each checkpoint)
✅ Incremental (phases build on each other)
✅ Right-sized (15-30 min per phase)

---

Full plan: .ddd_workspaces/{feature}/IMPLEMENTATION_PLAN.md

Options:
- Approve → Proceed to Step 4 (Implement)
- Adjust phases → I'll revise
- Questions → Let's discuss

Ready to build?
```

### Step 6: Handle Revisions

If user wants changes:
- Adjust phase boundaries
- Add/remove deliverables
- Reorder based on risk
- Update IMPLEMENTATION_PLAN.md
- Re-present

### Step 7: Update State

```json
{
  "features": {
    "{feature-id}": {
      "steps": {
        "1": { "completed": "..." },
        "2": { "completed": "..." },
        "3": { "completed": "{timestamp}" }
      }
    }
  },
  "ddd": {
    "current_step": "3"
  }
}
```

### Step 8: Handoff

```
✅ DDD Step 3 Complete: Implementation Plan Approved

**Feature**: {Feature ID} - {Feature Name}
**Phases**: {N} phases planned
**Plan**: .ddd_workspaces/{feature}/IMPLEMENTATION_PLAN.md

Ready for Step 4: Implement

Run: /ddd:4
```

---

## Edge Cases

### Missing Prerequisites

```
⚠️ Missing prerequisite

DDD steps run in order:
✅ Step 1: Understand (FEATURE_SPEC.md exists)
✅ Step 2: Document (DOCS_DRAFT.md exists)
❌ Step 3: Code-Breakdown (current)

Missing: {which file}

Please run: /ddd:{previous step}
```

### Feature Too Simple for Phases

```
ℹ️ Simple Feature Detected

This feature is straightforward enough for single-phase implementation:
- {why it's simple}

Recommended: Single phase with all deliverables

Proceed with 1-phase plan? [Yes / Break down anyway]
```

### Feature Too Complex

```
⚠️ Complexity Warning

This feature may be too large:
- {N} potential phases identified
- Multiple independent subsystems
- High risk areas

Options:
1. Proceed with {N} phases (longer DDD cycle)
2. Split into multiple features (return to ROADMAP.md)
3. Identify MVP subset for this cycle

Recommended: Option 2 if possible
```

### Dependencies Block Phases

```
⚠️ Dependency Issue

Phase 2 requires {dependency} which doesn't exist yet.

Options:
1. Add dependency creation to Phase 1
2. Create stub/mock for now, real implementation later
3. Reorder phases

Recommended: {best option for this case}
```

---

## Implementation Philosophy

**Build → Test → Learn → Adjust**

Each phase is a learning opportunity. If Phase 1 reveals something unexpected:
- Adjust Phase 2 plan
- Update IMPLEMENTATION_PLAN.md
- Note what was learned

Plans serve learning, not rigidity.

**Ruthless Simplicity**

For each phase ask:
- What's the simplest thing that could work?
- What can I defer to a later phase?
- What might I not need at all?

80/20: High value, low effort first.

---

## Success Criteria

After Step 3 completion:
- [x] IMPLEMENTATION_PLAN.md created
- [x] 2-4 phases defined
- [x] Each phase has concrete deliverables
- [x] Each phase has validation checkpoint
- [x] Plan is vertical slices, not horizontal layers
- [x] User has approved
- [x] State updated
- [x] Ready for /ddd:4

---

**Step 3 turns spec into actionable build plan. Each phase is a checkpoint, not just a task list.**
