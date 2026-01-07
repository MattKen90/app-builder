---
description: Enhancement DDD Step 1 - Understand and approve enhancement feature spec
argument-hint: [feature-id] (e.g., E-F1, E-F2) - optional, auto-detects next feature if omitted
---

# Enhancement DDD Step 1: Understand

**Mission**: Select next enhancement feature, create workspace, understand spec, get approval.

**Context**: This is the ENHANCER version. All paths use `.enhancer/` beachhead.

**Input**:
- `.enhancer/ROADMAP.md` (ordered enhancement list)
- `.enhancer/ARCHITECTURE.md` (technical approach)
- `.enhancer/DISCOVERY.md` (what exists)
- `.enhancer/state/project.json` (progress)

**Output**:
- `.enhancer/workspaces/{feature}/FEATURE_SPEC.md`
- Updated `.enhancer/state/project.json`

---

## Key Differences from Greenfield

| Aspect | Greenfield | Enhancer |
|--------|------------|----------|
| Feature IDs | F1, F2, F3 | E-F1, E-F2, E-F3 |
| Roadmap | `ROADMAP.md` | `.enhancer/ROADMAP.md` |
| State | `.state/project.json` | `.enhancer/state/project.json` |
| Workspaces | `.ddd_workspaces/` | `.enhancer/workspaces/` |
| Context | VISION.md | DISCOVERY.md + VISION.md |

---

## Process

### Step 1: Verify Enhancement Context

```
🔍 Checking enhancement setup...

- .enhancer/ exists: ✓
- DISCOVERY.md exists: ✓
- VISION.md exists: ✓
- ARCHITECTURE.md exists: ✓
- ROADMAP.md exists: ✓

Enhancement context loaded.
```

**If missing prerequisites:**
```
⚠️ Missing Prerequisites

Enhancement phases must complete in order:
- Phase 0 (Discovery): {status}
- Phase 1 (Vision): {status}
- Phase 2 (Architecture): {status}

Please complete missing phases first.
```

### Step 2: Determine Next Feature

Read `.enhancer/state/project.json` and `.enhancer/ROADMAP.md`:

```
📋 Next Enhancement Feature

Based on ROADMAP.md and current progress:

✅ Completed: E-F1 (Stripe Integration)
🔄 In Progress: None
⏳ Next Available: E-F2 (Subscription Tiers)

E-F2 is next because:
- Dependencies satisfied (E-F1 ✓)
- Next in roadmap priority

Proceed with E-F2? [Yes / Pick different / Show all]
```

### Step 3: Create Workspace

```bash
mkdir -p .enhancer/workspaces/{E-F#}-{feature-name}/
```

### Step 4: Extract Feature Spec

Create `.enhancer/workspaces/{feature}/FEATURE_SPEC.md`:

```markdown
# Enhancement Feature Spec: {E-F#} - {Feature Name}

## Enhancement Context

**Enhancing**: {App name from DISCOVERY.md}
**Existing State**: {Relevant context from DISCOVERY.md}

---

## From ROADMAP.md

**ID**: {E-F#}
**Name**: {feature-name}
**Description**: {description}
**User Story**: {user story}
**Tier**: 🆓 Free | 💰 Paid | 🏢 Enterprise

### Acceptance Criteria
- [ ] {criterion 1}
- [ ] {criterion 2}

### Dependencies
- {E-F1}: {why needed}

---

## From ARCHITECTURE.md

### Technical Components
- {component}: {what's needed}

### Integration Points
- {Where this connects to existing code}

---

## From DISCOVERY.md

### Existing Patterns to Follow
- {Pattern}: {How to apply}

### Existing Code to Integrate With
- {File/Module}: {How enhancement connects}

---

## Implementation Notes

{Additional context for building this enhancement}

---

**Status**: Pending approval
**Created**: {timestamp}
```

### Step 5: Critical Spec Analysis

**Analysis Checklist:**

1. **Completeness**
   - Acceptance criteria specific and testable?
   - Dependencies identified?

2. **Consistency**
   - Aligns with existing codebase patterns (from DISCOVERY.md)?
   - Follows ARCHITECTURE.md approach?

3. **Integration**
   - Clear integration points with existing code?
   - Won't break existing functionality?

4. **Monetization**
   - Tier clearly defined?
   - Feature gating required?

### Step 6: Present for Approval

```
📋 Enhancement Feature Spec: E-F2

## Summary
{Brief description}

## Tier: 💰 Paid

## Acceptance Criteria
- [ ] {criterion 1}
- [ ] {criterion 2}

## Integration Points
- Connects to: {existing code}
- Follows pattern: {pattern from discovery}

---

Spec written to: .enhancer/workspaces/E-F2-{name}/FEATURE_SPEC.md

Options:
- Approve → Proceed to Step 2 (Document)
- Revise → I'll update the spec
- Questions → Let's discuss

Ready to proceed?
```

### Step 7: Update State

```json
{
  "features": {
    "E-F2": {
      "status": "in_progress",
      "started": "{timestamp}",
      "steps": {
        "1": { "completed": "{timestamp}" }
      }
    }
  },
  "ddd": {
    "current_feature": "E-F2",
    "current_step": "1",
    "workspace": ".enhancer/workspaces/E-F2-{name}/"
  }
}
```

### Step 8: Handoff

```
✅ Enhancement DDD Step 1 Complete

**Feature**: E-F2 - {Name}
**Workspace**: .enhancer/workspaces/E-F2-{name}/
**Spec**: FEATURE_SPEC.md

Ready for Step 2: Document

Run: /enhancer/ddd/2
```

---

## Success Criteria

- [x] Enhancement context verified
- [x] Next feature selected
- [x] Workspace created in .enhancer/workspaces/
- [x] FEATURE_SPEC.md includes integration context
- [x] Spec approved
- [x] State updated
- [x] Ready for /enhancer/ddd/2
