---
description: DDD Step 5 - Final review, documentation finalization, and feature completion
---

# DDD Step 5: Review

**Mission**: Final review, finalize documentation, mark feature complete, clean up workspace.

**Input**:
- All workspace artifacts (FEATURE_SPEC.md, DOCS_DRAFT.md, IMPLEMENTATION_PLAN.md, PROGRESS.md)
- Implemented code
- `ARCHITECTURE.md`, `ROADMAP.md`

**Output**:
- `docs/features/{feature-id}-{feature-name}.md` (final documentation)
- Updated `.state/project.json` (feature marked complete)
- Git commit with final changes
- Clean workspace (optional archive)

---

## Process

### Step 1: Load All Artifacts

Read all workspace files:
- `FEATURE_SPEC.md` (original spec)
- `DOCS_DRAFT.md` (documentation draft)
- `IMPLEMENTATION_PLAN.md` (build plan)
- `PROGRESS.md` (what was built)

Review the implemented code.

### Step 2: Implementation Review

Verify implementation quality:

#### 2A: Acceptance Criteria Check

From FEATURE_SPEC.md:
```
Acceptance Criteria:
- [ ] {criterion 1}: {PASS/FAIL}
- [ ] {criterion 2}: {PASS/FAIL}
- [ ] {criterion 3}: {PASS/FAIL}
```

#### 2B: Documentation Accuracy Check

Compare DOCS_DRAFT.md to actual implementation:
- Do documented features work as described?
- Are examples accurate?
- Any undocumented capabilities added?
- Any documented features not implemented?

```
Documentation vs Implementation:

✅ Matches: {list of accurate docs}
⚠️ Needs update: {list of mismatches}
➕ Undocumented: {new capabilities to add}
```

#### 2C: Code Quality Check

Quick assessment:
- [ ] Follows ARCHITECTURE.md patterns
- [ ] Tests passing
- [ ] No obvious issues
- [ ] Consistent with codebase style

#### 2D: Present Review Summary

```
🔍 Feature Review: {Feature ID} - {Feature Name}

## Acceptance Criteria
✅ {N}/{N} criteria met

## Documentation Accuracy
{Summary of matches/mismatches}

## Code Quality
{Summary assessment}

## Overall Status
{READY / NEEDS WORK}

---

{If NEEDS WORK: List specific issues to address}
{If READY: Proceed to documentation finalization}
```

If issues found, address them before proceeding.

### Step 3: Finalize Documentation

Create the final feature documentation:

#### 3A: Generate Final Doc

Take DOCS_DRAFT.md and:
1. Update based on actual implementation
2. Verify all examples work
3. Add any discovered edge cases
4. Polish language and formatting

#### 3B: Write to Final Location

Create `docs/features/{feature-id}-{feature-name}.md`:

```markdown
# {Feature Name}

{One-sentence description}

## Overview

{Updated overview based on actual implementation}

## Quick Start

{Verified working examples}

## Features

{Actual features as implemented}

## Configuration

{Actual configuration options}

## Examples

{Tested, working examples}

## Troubleshooting

{Issues discovered during implementation}

---

*Feature ID: {feature-id}*
*Implemented: {date}*
```

#### 3C: Verify Final Doc

```
📝 Final Documentation

Created: docs/features/{feature-id}-{feature-name}.md

Verified:
✅ Matches implementation
✅ Examples tested and working
✅ Follows documentation standards
```

### Step 4: Update Project State

#### 4A: Mark Feature Complete

Update `.state/project.json`:

```json
{
  "features": {
    "{feature-id}": {
      "status": "complete",
      "started": "{start timestamp}",
      "completed": "{now}",
      "steps": {
        "1": { "completed": "...", "commit": "..." },
        "2": { "completed": "...", "commit": "..." },
        "3": { "completed": "...", "commit": "..." },
        "4": { "completed": "...", "commit": "..." },
        "5": { "completed": "{now}", "commit": "{commit hash}" }
      }
    }
  },
  "ddd": {
    "current_feature": null,
    "current_step": null,
    "workspace": null
  },
  "metrics": {
    "features_completed": {N+1}
  }
}
```

#### 4B: Calculate Metrics

```
📊 Feature Metrics

Feature: {feature-id}
Total Duration: {end - start}
Steps:
- Understand: {duration}
- Document: {duration}
- Code-Breakdown: {duration}
- Implement: {duration}
- Review: {duration}

Commits: {N} commits
Lines Changed: +{added} -{removed}
```

### Step 5: Final Commit

```bash
git add docs/features/{feature-id}-{feature-name}.md
git add .state/project.json
git add {any other final changes}
git commit -m "[DDD:{feature-id}:5] Complete {feature-name}

- Final documentation created
- All acceptance criteria met
- Feature ready for use

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude Opus 4.5 <noreply@anthropic.com>"
```

### Step 6: Workspace Cleanup

Options for workspace:

#### Option A: Archive (Recommended)
```bash
mkdir -p .archive/ddd/{feature-id}-{feature-name}/
mv .ddd_workspaces/{feature-id}-{feature-name}/* .archive/ddd/{feature-id}-{feature-name}/
rmdir .ddd_workspaces/{feature-id}-{feature-name}/
```

#### Option B: Delete
```bash
rm -rf .ddd_workspaces/{feature-id}-{feature-name}/
```

Present choice to user:
```
🗂️ Workspace Cleanup

Options:
1. Archive to .archive/ddd/ (preserves working notes)
2. Delete (clean slate)

Recommended: Archive

Which option?
```

### Step 7: Completion Summary

```
🎉 DDD Cycle Complete!

**Feature**: {Feature ID} - {Feature Name}

## Delivered
- ✅ Working implementation
- ✅ Tests passing
- ✅ Documentation: docs/features/{feature-id}-{feature-name}.md

## Metrics
- Duration: {total time}
- Commits: {N}
- Lines: +{added} -{removed}

## What's Next

{Check ROADMAP.md for next feature}

Next feature in queue: {next feature or "None - all complete!"}

To continue: /ddd:1
```

### Step 8: Push Changes

```bash
git push
```

```
✅ Changes pushed to remote

Feature {feature-id} is now:
- Implemented
- Documented
- Committed
- Pushed

DDD cycle complete. Ready for next feature.
```

---

## Edge Cases

### Implementation Doesn't Match Spec

```
⚠️ Spec Mismatch Detected

Implementation differs from FEATURE_SPEC.md:

| Criterion | Spec | Implementation |
|-----------|------|----------------|
| {criterion} | {expected} | {actual} |

Options:
1. Fix implementation to match spec
2. Update spec (if implementation is correct)
3. Document as known limitation

Which approach?
```

### Documentation Significantly Wrong

```
⚠️ Documentation Overhaul Needed

DOCS_DRAFT.md has significant inaccuracies:
- {issue 1}
- {issue 2}

This requires substantial rewrite, not just edits.

Options:
1. Rewrite documentation now
2. Create minimal accurate docs, improve later
3. Return to Step 2 for full documentation redo

Recommended: Option 1 (do it right)
```

### Tests Failing at Review

```
⚠️ Test Failures at Review

Tests that were passing are now failing:
- {test 1}: {error}
- {test 2}: {error}

This shouldn't happen if Step 4 was complete.

Options:
1. Fix tests now (likely minor issue)
2. Return to Step 4 for debugging
3. Review what changed since Step 4

Starting with Option 1...
```

### Missing Workspace Files

```
⚠️ Incomplete Workspace

Missing artifacts:
- {missing file 1}
- {missing file 2}

This suggests earlier steps weren't completed properly.

Options:
1. Reconstruct from git history
2. Proceed with available artifacts
3. Re-run missing steps

Recommended: Option 1 if possible
```

### User Wants Changes Before Completion

```
ℹ️ Changes Requested

You've requested changes before marking complete:
- {change 1}
- {change 2}

Options:
1. Make changes now (minor)
2. Return to Step 4 (significant changes)
3. Mark complete, create new feature for changes

Which approach?
```

---

## Review Checklist

Before marking complete:

**Implementation:**
- [ ] All acceptance criteria met
- [ ] Tests passing
- [ ] No regressions
- [ ] Follows architecture patterns

**Monetization (MRR is King):**
- [ ] Feature tier implemented correctly (Free/Paid/Enterprise)
- [ ] If paid: Feature gating working
- [ ] If paid: Upgrade prompts in place
- [ ] Stripe integration tested (if applicable)

**Documentation:**
- [ ] Final doc created in docs/features/
- [ ] Matches actual implementation
- [ ] Examples verified working
- [ ] Follows documentation standards

**Project State:**
- [ ] .state/project.json updated
- [ ] Feature marked complete
- [ ] Metrics captured

**Git:**
- [ ] All changes committed
- [ ] Commit messages follow format
- [ ] Changes pushed

**Cleanup:**
- [ ] Workspace archived or deleted
- [ ] No orphaned files

---

## Success Criteria

After Step 5 completion:
- [x] Implementation reviewed and approved
- [x] Final documentation in docs/features/
- [x] All tests passing
- [x] State updated (feature complete)
- [x] Final commit made
- [x] Changes pushed
- [x] Workspace cleaned up
- [x] Ready for next feature

---

**Step 5 closes the loop. Feature is reviewed, documented, committed, and complete. The factory is ready for the next feature.**
