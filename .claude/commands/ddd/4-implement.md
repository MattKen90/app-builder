---
description: DDD Step 4 - Execute implementation plan phase by phase
---

# DDD Step 4: Implement

**Mission**: Build the feature following the implementation plan. Execute phase by phase with checkpoints.

**Mode-Aware**: Reads `.state.json` to determine paths. In enhancer mode, includes regression testing to ensure existing functionality isn't broken.

---

## Mode Detection

| Resource | Greenfield | Enhancer |
|----------|------------|----------|
| Workspaces | `.ddd_workspaces/` | `.enhancer/workspaces/` |
| Architecture | `ARCHITECTURE.md` | `.enhancer/ARCHITECTURE.md` |
| Testing | New tests | New tests + regression tests |
| Patterns | Define new | Follow existing (from DISCOVERY.md) |

---

**Input** (paths depend on mode):
- `{WORKSPACE_PATH}/{feature}/IMPLEMENTATION_PLAN.md`
- `{WORKSPACE_PATH}/{feature}/FEATURE_SPEC.md`
- `{WORKSPACE_PATH}/{feature}/DOCS_DRAFT.md`
- `{ARCHITECTURE_PATH}`

**Output**:
- Working code (in appropriate project locations)
- Tests (passing)
- `{WORKSPACE_PATH}/{feature}/PROGRESS.md`

**Enhancer Mode Critical**: Run existing test suite before AND after each phase to catch regressions.

---

## Process

### Step 1: Load Context

Read:
- `IMPLEMENTATION_PLAN.md` (phases and deliverables)
- `FEATURE_SPEC.md` (requirements and acceptance criteria)
- `DOCS_DRAFT.md` (what implementation must deliver)
- `ARCHITECTURE.md` (patterns to follow)

Initialize `PROGRESS.md`:

```markdown
# Implementation Progress: {Feature ID} - {Feature Name}

**Started**: {timestamp}
**Status**: In Progress

---

## Phases Overview

| Phase | Name | Status |
|-------|------|--------|
| 1 | {name} | 🔄 In Progress |
| 2 | {name} | ⏳ Pending |
| 3 | {name} | ⏳ Pending |

---

## Phase 1: {Name}

**Started**: {timestamp}
**Goal**: {goal from plan}

### Deliverables
- [ ] {deliverable 1}
- [ ] {deliverable 2}

### Progress Log
{Will be updated as work progresses}

---
```

### Step 2: Execute Phases

**For each phase in IMPLEMENTATION_PLAN.md:**

#### 2A: Announce Phase Start

```
🔨 Starting Phase {N}: {Phase Name}

Goal: {phase goal}

Deliverables:
- {deliverable 1}
- {deliverable 2}

Beginning implementation...
```

#### 2B: Build Phase Deliverables

For each deliverable:
1. Write the code following ARCHITECTURE.md patterns
2. Follow project conventions
3. Keep it simple (ruthless simplicity)
4. Update PROGRESS.md as you work

**Implementation Principles:**
- **Zero-BS**: Working code, no stubs, no TODOs
- **Test as you go**: Write tests alongside code
- **Small commits**: Commit after each significant piece
- **Follow patterns**: Use existing code as reference

#### 2C: Run Phase Tests

Execute tests for this phase:

```bash
# Run relevant tests
{test command from IMPLEMENTATION_PLAN.md}
```

**If tests pass:**
- Update PROGRESS.md with results
- Mark deliverables complete
- Proceed to checkpoint

**If tests fail:**
1. Analyze failure
2. Fix the issue
3. Re-run tests
4. Repeat until passing

```
⚠️ Test Failure

Failed test: {test name}
Error: {error message}

Analyzing and fixing...

{Show fix}

Re-running tests...

✅ Tests now passing
```

#### 2D: Phase Checkpoint

Run the validation command from IMPLEMENTATION_PLAN.md:

```bash
{validation command}
```

Verify checkpoint criteria:
- [ ] {criterion 1} - {pass/fail}
- [ ] {criterion 2} - {pass/fail}
- [ ] Previous phases still work - {pass/fail}

#### 2E: Present Phase Completion

```
📦 Phase {N} Complete: {Phase Name}

Deliverables:
✅ {deliverable 1}
✅ {deliverable 2}

Tests: {X} passed
Checkpoint: ✅ All criteria met

---

Files created/modified:
- {file 1}: {what changed}
- {file 2}: {what changed}

---

Options:
1. Proceed to Phase {N+1}
2. Review code before continuing
3. Adjust next phase based on learnings
```

#### 2F: User Decision

Wait for user input:
- **Proceed**: Continue to next phase
- **Review**: Show code changes, discuss
- **Adjust**: Update IMPLEMENTATION_PLAN.md if learnings require it

#### 2G: Update Progress

```markdown
## Phase {N}: {Name} - ✅ Complete

**Completed**: {timestamp}

### Deliverables
- [x] {deliverable 1}
- [x] {deliverable 2}

### Files Changed
- `{path}`: {description}

### Tests
- {X} tests passing

### Learnings
{Any insights that affect future phases}

---
```

#### 2H: Commit Phase

```bash
git add {relevant files}
git commit -m "[DDD:{feature-id}:{phase}] {phase description}"
```

Commit message format enables velocity tracking.

### Step 3: Repeat for All Phases

Loop through all phases until complete.

### Step 4: Final Integration

After all phases:

#### 4A: Run Full Test Suite

```bash
# Run all tests
{project test command}
```

Ensure no regressions.

#### 4B: Validate Against Acceptance Criteria

From FEATURE_SPEC.md:
- [ ] {criterion 1} - {status}
- [ ] {criterion 2} - {status}
- [ ] {criterion 3} - {status}

#### 4C: Validate Against Documentation

From DOCS_DRAFT.md:
- Does implementation match what docs describe?
- Are all documented features working?
- Do examples actually work?

### Step 5: Update State

```json
{
  "features": {
    "{feature-id}": {
      "steps": {
        "1": { "completed": "..." },
        "2": { "completed": "..." },
        "3": { "completed": "..." },
        "4": { "completed": "{timestamp}" }
      }
    }
  },
  "ddd": {
    "current_step": "4"
  }
}
```

### Step 6: Handoff

```
✅ DDD Step 4 Complete: Implementation Done

**Feature**: {Feature ID} - {Feature Name}
**Phases Completed**: {N}/{N}
**Tests**: All passing
**Acceptance Criteria**: All met

Files created/modified:
- {summary of changes}

Progress log: .ddd_workspaces/{feature}/PROGRESS.md

Ready for Step 5: Review

Run: /ddd:5
```

---

## Edge Cases

### Missing Prerequisites

```
⚠️ Missing prerequisite: IMPLEMENTATION_PLAN.md

DDD steps run in order:
✅ Step 1: Understand
✅ Step 2: Document
❌ Step 3: Code-Breakdown (IMPLEMENTATION_PLAN.md missing)
⏹️ Step 4: Implement (current)

Please run: /ddd:3
```

### Tests Fail Repeatedly

```
⚠️ Persistent Test Failures

Tests failing after {N} attempts:
- {test 1}: {error}
- {test 2}: {error}

Analysis:
{What might be wrong}

Options:
1. Debug deeper (show full error context)
2. Review implementation approach
3. Check if spec/tests are wrong
4. Ask user for guidance

Recommended: Option {N}
```

### Phase Takes Too Long

If a phase exceeds expected time:

```
ℹ️ Phase Duration Notice

Phase {N} is taking longer than expected.

Possible reasons:
- Unexpected complexity
- Missing dependencies
- Scope creep

Options:
1. Continue (it's close to done)
2. Split remaining work into new phase
3. Pause and reassess approach

Current progress: {what's done so far}
```

### Learnings Require Plan Changes

```
💡 Implementation Learning

During Phase {N}, discovered:
{What was learned}

Impact on remaining phases:
- Phase {M}: {how it changes}
- Phase {O}: {how it changes}

Options:
1. Update IMPLEMENTATION_PLAN.md and continue
2. Pause and discuss implications
3. Continue with current plan (minor impact)

Recommended: Option {N}
```

### Dependency Issues

```
⚠️ Dependency Issue

Phase {N} requires {dependency} which:
- Doesn't exist
- Isn't working as expected
- Has different interface than assumed

Options:
1. Create/fix dependency first
2. Mock dependency, continue, fix later
3. Redesign approach to avoid dependency

Recommended: {best option}
```

### Acceptance Criteria Unclear

```
❓ Acceptance Criteria Ambiguity

Criterion: "{criterion}"

This is unclear or untestable:
- {Why it's ambiguous}

Options:
1. Interpret as: {interpretation} and proceed
2. Ask user for clarification
3. Skip for now, address in Review step

Which approach?
```

---

## Implementation Guidelines

### Code Quality

- Follow ARCHITECTURE.md patterns
- Match existing code style
- Write clear, readable code
- Comment only when logic isn't self-evident
- Handle errors appropriately

### Testing Strategy

**When to Write Tests:**
- Write tests DURING implementation, not after
- Each phase deliverable should have corresponding tests
- Tests are part of the deliverable, not separate work

**What to Test:**

| Layer | What | How |
|-------|------|-----|
| Unit | Individual functions, components | Fast, isolated, mock dependencies |
| Integration | Components working together | Test real interactions |
| E2E (if applicable) | Full user flows | Simulate actual usage |

**Coverage Expectations:**
- Unit tests: Every function with logic (not just getters/setters)
- Integration: Key user flows and data paths
- E2E: Critical happy paths only (expensive to maintain)

**Testing Principles:**
- Test behavior, not implementation details
- Happy path first, then error cases, then edge cases
- Tests must be fast and reliable (no flaky tests)
- If you can't test it, the code might need refactoring

**Per Phase:**
1. Write tests for phase deliverables
2. Run tests - must pass before checkpoint
3. Run ALL tests (regression) before moving to next phase

**Test Commands** (define in IMPLEMENTATION_PLAN.md):
```bash
# Phase tests
{test command for this phase}

# Full test suite
{command to run all tests}
```

### Commit Strategy

- Commit after each phase
- Use format: `[DDD:{feature-id}:{phase}] {description}`
- Include all related changes in one commit
- Don't commit broken code

### Progress Tracking

- Update PROGRESS.md after each significant step
- Log learnings as they happen
- Note any deviations from plan
- Track time per phase (for velocity)

---

## Success Criteria

After Step 4 completion:
- [x] All phases implemented
- [x] All tests passing
- [x] All acceptance criteria met
- [x] Implementation matches documentation
- [x] Code committed with proper messages
- [x] PROGRESS.md complete
- [x] No regressions in existing features
- [x] State updated
- [x] Ready for /ddd:5

---

**Step 4 is where the code happens. Phase by phase, checkpoint by checkpoint, until the feature works.**
