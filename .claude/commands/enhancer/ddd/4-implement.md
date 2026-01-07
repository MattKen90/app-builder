---
description: Enhancement DDD Step 4 - Execute implementation with integration checkpoints
---

# Enhancement DDD Step 4: Implement

**Mission**: Build the enhancement following the plan. Integrate with existing code. Verify no regressions.

**Context**: Enhancer version - integration and regression testing are critical.

**Input**:
- `.enhancer/workspaces/{feature}/IMPLEMENTATION_PLAN.md`
- `.enhancer/workspaces/{feature}/FEATURE_SPEC.md`
- `.enhancer/DISCOVERY.md` (patterns to follow)

**Output**:
- Working enhancement code (integrated with existing)
- Tests passing (new + existing)
- `.enhancer/workspaces/{feature}/PROGRESS.md`

---

## Key Differences from Greenfield

| Aspect | Greenfield | Enhancer |
|--------|------------|----------|
| Risk | Build wrong | Break existing |
| Tests | New tests | New + regression tests |
| Patterns | Define | Follow existing |
| Checkpoint | Feature works | Feature works + nothing broken |

---

## Process

### Step 1: Load Context

Read:
- `IMPLEMENTATION_PLAN.md` (phases)
- `FEATURE_SPEC.md` (requirements)
- `.enhancer/DISCOVERY.md` (patterns to follow)

Initialize `.enhancer/workspaces/{feature}/PROGRESS.md`

### Step 2: Execute Phases

**For each phase:**

#### 2A: Pre-Phase Regression Check
```bash
# Run existing tests BEFORE changes
{existing test command}
```

Save baseline: All existing tests passing.

#### 2B: Implement Phase
- Follow patterns from DISCOVERY.md
- Integrate with existing code
- Write new tests alongside code

#### 2C: Post-Phase Verification
```bash
# Run phase tests
{phase test command}

# Run regression tests
{existing test command}
```

**Checkpoint criteria:**
- [ ] Phase deliverables complete
- [ ] New tests passing
- [ ] Existing tests still passing (CRITICAL)
- [ ] Integration verified

#### 2D: Phase Completion
```
📦 Phase {N} Complete

Deliverables: ✅
New Tests: {X} passing
Regression Tests: ✅ All passing

Files modified:
- {file}: {changes}

Files created:
- {file}: {purpose}

Integration verified: ✅

Options:
1. Proceed to Phase {N+1}
2. Review changes
```

### Step 3: Final Integration Verification

After all phases:

```bash
# Full test suite
{all tests command}

# Manual verification
{verification steps}
```

**Final checklist:**
- [ ] All acceptance criteria met
- [ ] All new tests passing
- [ ] All existing tests passing
- [ ] Integration points working
- [ ] No console errors/warnings
- [ ] Performance acceptable

### Step 4: Handoff

```
✅ Enhancement DDD Step 4 Complete

**Feature**: {E-F#} - {Name}
**Phases Completed**: {N}/{N}

Tests:
- New: {X} passing
- Regression: ✅ All passing

Integration: ✅ Verified

Ready for Step 5: Review

Run: /enhancer/ddd/5
```

---

## Critical: Regression Testing

**Every phase must verify existing tests still pass.**

If regression detected:
```
⚠️ Regression Detected

Existing test failing after Phase {N}:
- {test}: {error}

This enhancement broke existing functionality.

Options:
1. Fix the regression (recommended)
2. Review approach - may need redesign
3. Check if test expectation should change

NEVER proceed with broken existing tests.
```

---

## Implementation Guidelines

### Follow Existing Patterns

From DISCOVERY.md:
- Use same component structure
- Follow same naming conventions
- Match error handling approach
- Use same state management

### Integration Best Practices

- Import existing utilities, don't recreate
- Extend existing types, don't shadow
- Add to existing routes/handlers cleanly
- Follow existing file organization

### Testing Strategy

**New tests:**
- Unit tests for new logic
- Integration tests for new flows
- E2E for critical paths

**Regression tests:**
- Run full existing suite after each phase
- Pay attention to integration boundaries
- Test areas that touch existing code

---

## Success Criteria

- [x] All phases implemented
- [x] All new tests passing
- [x] All existing tests passing (no regressions)
- [x] Integration verified
- [x] Follows existing patterns
- [x] PROGRESS.md complete
- [x] Ready for /enhancer/ddd/5
