---
description: Add a new feature with rigorous spec clarification (mini Phase 1+2 cycle)
allowed-tools: Read, Edit, Write, WebSearch
argument-hint: [feature description]
---

# Create New Feature

Add a new feature through rigorous specification. This is a mini Phase 1 + Phase 2 cycle.

**Why rigorous?** A new feature can throw off the entire balance of the application. It must be properly vetted.

## Context

- State: @.state.json
- Vision: @VISION.md
- Architecture: @ARCHITECTURE.md
- Roadmap: @ROADMAP.md

## Feature Request

```
$ARGUMENTS
```

---

## Process

### Phase A: Vision Review (vision-architect lens)

#### 1. Alignment Check

Does this feature align with the existing vision?

```
🔍 Alignment Analysis

App Vision: {summary from VISION.md}
Proposed Feature: {from arguments}

Alignment: [Strong / Partial / Weak / Conflict]
Reasoning: {why}
```

#### 2. Extract & Clarify (3 rounds)

**Round 1: Problem & Value**
- What problem does this feature solve?
- Who specifically needs this?
- How urgent is this need?
- What happens if we don't build it?

**Round 2: Scope & Boundaries**
- What exactly is in scope?
- What is explicitly OUT of scope?
- What's the minimum viable version?
- What's the gold-plated version?

**Round 3: Monetization & Priority**
- Is this Free, Paid, or Enterprise?
- Does this drive new revenue or retention?
- Where does this rank against existing roadmap?
- Does this cannibalize or enhance existing features?

**Summarize after each round. Get confirmation.**

#### 3. Impact Assessment

```
📊 Impact on Existing App

Features Affected:
- {F1}: {how affected}
- {F2}: {how affected}

Scope Changes:
- In: {what's now in scope}
- Out: {what moves out}

Monetization Impact:
- {pricing/tier changes if any}
```

---

### Phase B: Technical Review (tech-architect lens)

#### 4. Architecture Fit

```
🏗️ Architecture Analysis

Current Stack: {from ARCHITECTURE.md}

New Feature Requires:
- Components: {new components needed}
- Data Model: {schema changes}
- API: {new endpoints}
- Dependencies: {new dependencies}

Fits Existing Patterns: [Yes / Partial / No]
Breaking Changes: [None / Minor / Major]
```

#### 5. Dependency Analysis

```
📦 Dependencies

This feature requires:
- {existing features it depends on}

This feature enables:
- {future features it unlocks}

Conflicts with:
- {any conflicting features}
```

#### 6. Sizing & Sequencing

```
⏱️ Sizing

Complexity: [Small / Medium / Large]
DDD Cycles: {estimated number}
Should Split: [Yes / No]

If splitting:
- {Feature-A}: {scope}
- {Feature-B}: {scope}
```

---

### Phase C: Approval & Integration

#### 7. Feature Spec

Create complete feature specification:

```markdown
## Feature: {ID} - {Name}

### From Vision Review
- Problem: {statement}
- Value: {proposition}
- Tier: {Free/Paid/Enterprise}
- Priority: {High/Medium/Low}

### From Technical Review
- Components: {list}
- Data Model: {changes}
- API: {endpoints}
- Dependencies: {features}

### Acceptance Criteria
- [ ] {criterion 1}
- [ ] {criterion 2}
- [ ] {criterion 3}

### Out of Scope
- {explicit exclusions}
```

#### 8. Seek Approval

```
📋 New Feature Proposal

{Feature ID} - {Feature Name}

Summary: {2-3 sentences}

Impact:
- Affects: {existing features}
- Requires: {dependencies}
- Enables: {future features}

Tier: {Free/Paid/Enterprise}
Complexity: {Small/Medium/Large}

Approve this feature? [Yes / Modify / Reject]
```

#### 9. Update Canonical Docs

On approval, update:

**VISION.md:**
- Add feature to appropriate section
- Update scope if needed
- Note monetization tier

**ARCHITECTURE.md:**
- Add components
- Update data model
- Document API changes

**ROADMAP.md:**
- Add feature with dependencies
- Sequence into appropriate phase
- Update dependency graph

**.state.json:**
- Add feature with status: pending

---

## Rejection Handling

If feature is rejected or needs major changes:

```
❌ Feature Not Added

Reason: {why rejected or needs rework}

Options:
1. Revise and resubmit with: {specific changes}
2. Defer to future version
3. Abandon

Which option?
```

---

## Remember

- **Existing vision first** - New feature serves the app, not the other way around
- **Three rounds minimum** - Don't skip clarification
- **Impact assessment required** - Understand what changes
- **Get explicit approval** - No silent additions
- **Update all docs** - Keep canonical docs in sync
- **MRR lens** - Every feature needs a monetization answer
