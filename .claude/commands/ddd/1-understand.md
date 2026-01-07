---
description: DDD Step 1 - Understand and approve feature spec before implementation
argument-hint: [feature-id] (e.g., F1, E-F1) - optional, auto-detects next feature if omitted
---

# DDD Step 1: Understand

**Mission**: Select next feature, create workspace, understand spec, get human approval before building.

**Mode-Aware**: This command adapts to greenfield or enhancer mode by reading `.state.json`.

---

## Mode Detection

Read `.state.json` and set paths accordingly:

| Resource | Greenfield | Enhancer |
|----------|------------|----------|
| State | `.state.json` | `.state.json` |
| Roadmap | `ROADMAP.md` | `.enhancer/ROADMAP.md` |
| Architecture | `ARCHITECTURE.md` | `.enhancer/ARCHITECTURE.md` |
| Workspaces | `.ddd_workspaces/` | `.enhancer/workspaces/` |
| Feature prefix | F | E-F |
| Extra context | - | `.enhancer/DISCOVERY.md` |

**If mode not set:**
```
⚠️ Mode Not Set

Please set mode first: /set-state mode <greenfield|enhancer>
Then run /init to set up project structure.
```

---

**Input** (paths depend on mode):
- `{ROADMAP_PATH}` (ordered feature list with dependencies)
- `{ARCHITECTURE_PATH}` (technical approach)
- `{STATE_PATH}` (what's done/in-progress)
- `{DISCOVERY_PATH}` (enhancer mode only - existing codebase context)

**Output**:
- `{WORKSPACE_PATH}/{feature-id}-{feature-name}/FEATURE_SPEC.md`
- Updated `{STATE_PATH}`
- Human approval to proceed

---

## Process

### Step 0: Load Mode and Paths

```
🔍 Detecting mode...

Mode: {greenfield|enhancer}

Paths:
- State: {STATE_PATH}
- Roadmap: {ROADMAP_PATH}
- Workspaces: {WORKSPACE_PATH}
- Feature prefix: {F|E-F}
```

### Step 1: Determine Next Feature

**If feature-id provided via `$ARGUMENTS`:**
- Use that feature directly
- Display: "Using specified feature: {feature-id}"

**If no argument provided:**
1. Read `.state.json` to check:
   - Is there a feature already in-progress? → Resume it
   - If not, what features are completed?
2. Read `ROADMAP.md` to get ordered feature list
3. Find next pending feature (respecting dependencies)
4. Present selection to user:

```
📋 Next Feature Selection

Based on ROADMAP.md and current progress:

✅ Completed: F1 (User Authentication), F2 (Dashboard)
🔄 In Progress: None
⏳ Next Available: F3 (Data Export)

F3 is next because:
- Dependencies satisfied (requires F1 ✓)
- Next in roadmap priority order

Proceed with F3? [Yes / Pick different / Show all]
```

Wait for user confirmation before proceeding.

### Step 2: Create Workspace

```bash
mkdir -p .ddd_workspaces/{feature-id}-{feature-name}/
```

Example: `.ddd_workspaces/F3-data-export/`

### Step 3: Extract Feature Spec

Read from `ROADMAP.md` and `ARCHITECTURE.md`:
- Feature description
- User story
- Acceptance criteria
- Technical components needed
- Dependencies

Create `FEATURE_SPEC.md` in workspace:

```markdown
# Feature Spec: {Feature ID} - {Feature Name}

## From ROADMAP.md

**ID**: {feature-id}
**Name**: {feature-name}
**Description**: {description}
**User Story**: {user story}
**Tier**: 🆓 Free | 💰 Paid | 🏢 Enterprise

### Acceptance Criteria
- [ ] {criterion 1}
- [ ] {criterion 2}
- [ ] {criterion 3}

### Dependencies
- {F1}: {why needed}
- {F2}: {why needed}

---

## From ARCHITECTURE.md

### Technical Components
- {component 1}: {what's needed}
- {component 2}: {what's needed}

### Data Model Impact
- {entity changes}

### API/Interface Changes
- {endpoint or interface changes}

---

## Implementation Notes

{Any additional context, constraints, or guidance for implementation}

---

**Status**: Pending approval
**Created**: {timestamp}
```

### Step 4: Critical Spec Analysis

Before presenting to user, analyze the spec for issues:

**Analysis Checklist:**

1. **Completeness**
   - Are acceptance criteria specific and testable?
   - Are all dependencies identified?
   - Is technical approach clear?

2. **Consistency**
   - Does spec align with ARCHITECTURE.md patterns?
   - Any conflicts with existing features?

3. **Feasibility**
   - Can this be built with current tech stack?
   - Any blockers or unknowns?

4. **Sizing**
   - Is this right-sized for ~1 hour DDD cycle?
   - Too large? Flag for splitting.
   - Too small? Flag for combining.

5. **Monetization** (MRR is King)
   - Is the tier clearly defined? (Free/Paid/Enterprise)
   - If paid: Does it require feature gating?
   - If paid: Does it have upgrade triggers?
   - Does this feature support revenue goals?

**If issues found:**
```
⚠️ Spec Analysis: Issues Detected

{issue 1}: {description}
  - Impact: {what this affects}
  - Recommendation: {how to resolve}

{issue 2}: ...

---

Options:
1. Address issues now (I'll update the spec)
2. Proceed with known limitations
3. Go back to ROADMAP.md to adjust feature

Which would you prefer?
```

**If no issues:**
```
✅ Spec Analysis: Passed

Checked for:
- Completeness: All criteria defined
- Consistency: Aligns with architecture
- Feasibility: No blockers identified
- Sizing: Appropriate for DDD cycle

Proceeding to summary...
```

### Step 5: Present Executive Summary

Generate concise summary (200-300 words):

```
📋 Feature Summary: {Feature ID} - {Feature Name}

## What We're Building
{2-3 sentences: Plain language description of what this feature does}

## Why It Matters
{2-3 sentences: Value delivered, problems solved}

## Technical Approach
- {Key technical decision 1}
- {Key technical decision 2}
- {Key technical decision 3}

## Scope
- In: {what's included}
- Out: {what's explicitly not included}

## Dependencies
- Requires: {features that must be done first}
- Enables: {future features this unlocks}

---

Questions to consider:
- Does this match your expectations?
- Any concerns about the approach?
- Ready to proceed?
```

### Step 6: Q&A (If Needed)

If user has questions:
- Answer based on spec, ARCHITECTURE.md, ROADMAP.md
- Reference specific sections
- If user requests changes, update FEATURE_SPEC.md
- Document any modifications made

### Step 7: Update State

Once user approves, update `.state.json`:

```json
{
  "ddd": {
    "current_feature": "F3",
    "current_step": "1",
    "workspace": ".ddd_workspaces/F3-data-export/"
  },
  "features": {
    "F3": {
      "status": "in_progress",
      "started": "{timestamp}",
      "steps": {
        "1": { "completed": "{timestamp}" }
      }
    }
  }
}
```

### Step 8: Handoff

```
✅ DDD Step 1 Complete: Feature Understood & Approved

**Feature**: {Feature ID} - {Feature Name}
**Workspace**: .ddd_workspaces/{workspace}/
**Spec**: FEATURE_SPEC.md

Ready for Step 2: Document

Run: /ddd:2
```

---

## Edge Cases

### No ROADMAP.md Found

```
⚠️ Missing ROADMAP.md

DDD requires a roadmap to select features.

This means Phase 2 (Technical Foundation) isn't complete.

Run Phase 2 first to generate:
- ARCHITECTURE.md
- ROADMAP.md

Then return to DDD.
```

### All Features Complete

```
🎉 All Features Complete!

Every feature in ROADMAP.md has been implemented.

Options:
1. Review VISION.md for v2 features
2. Run /daily-summary for progress report
3. Start new app with /app-init
```

### Feature Dependencies Not Met

```
⚠️ Dependencies Not Satisfied

Feature {F5} requires:
- F3: ❌ Not complete
- F4: ❌ Not complete

Available features with satisfied dependencies:
- F3: Ready (no dependencies)
- F4: Ready (requires F1 ✓)

Would you like to:
1. Select F3 instead
2. Select F4 instead
3. Override and attempt F5 anyway (not recommended)
```

### User Wants Different Feature

```
📋 Feature Selection Override

Available features:
- F3: Data Export (next in roadmap) ✓
- F4: Settings Page (dependencies met) ✓
- F5: Admin Panel (missing: F3, F4) ⚠️

Select feature ID to proceed:
```

### Spec Too Large

```
⚠️ Feature Sizing Concern

This feature appears too large for a single DDD cycle:
- {reason 1}
- {reason 2}

Recommended split:
- F3a: {first part}
- F3b: {second part}

Options:
1. Accept split (update ROADMAP.md)
2. Proceed as single feature anyway
3. Discuss alternative breakdown
```

---

## Success Criteria

After Step 1 completion:
- [x] Feature selected (auto or manual)
- [x] Workspace created
- [x] FEATURE_SPEC.md generated
- [x] Spec analysis passed (or issues addressed)
- [x] User understands and approves
- [x] State updated
- [x] Ready for /ddd:2

---

**Step 1 bridges ROADMAP.md to implementation. No coding until spec is understood and approved.**
