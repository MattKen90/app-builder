---
description: Update VISION.md, ARCHITECTURE.md, and ROADMAP.md based on recent changes
---

# Update Docs

**Mission**: Sync canonical documents with reality. Use current context knowledge to update vision, architecture, and roadmap.

---

## When to Use

Run this command when:
- A feature implementation revealed new insights
- Technical decisions changed during build
- Scope shifted based on what you learned
- Features were added, removed, or modified
- Architecture evolved during implementation

---

## Process

### Step 1: Assess Current Context

Review what you know from recent work:
- What features were just built or modified?
- What technical decisions were made?
- What changed from the original plan?
- What new insights emerged?

```
🔍 Context Assessment

Recent work in context:
- {What was just done}
- {Key decisions made}
- {Surprises or pivots}
```

### Step 2: Read Current Docs

Read the canonical documents based on mode:

**Greenfield:**
- `VISION.md`
- `ARCHITECTURE.md`
- `ROADMAP.md`

**Enhancer:**
- `.enhancer/VISION.md`
- `.enhancer/ARCHITECTURE.md`
- `.enhancer/ROADMAP.md`

### Step 3: Identify Drift

Compare current docs to reality:

```
📊 Drift Analysis

VISION.md:
- [ ] Problem statement still accurate?
- [ ] Features list current?
- [ ] Monetization unchanged?
- [ ] Scope boundaries still valid?

ARCHITECTURE.md:
- [ ] Tech stack as documented?
- [ ] Data model current?
- [ ] API surface accurate?
- [ ] Payments architecture unchanged?

ROADMAP.md:
- [ ] Feature statuses current?
- [ ] Dependencies still accurate?
- [ ] Phase groupings still make sense?
- [ ] Next steps correct?
```

### Step 4: Propose Updates

Present what needs to change:

```
📝 Proposed Updates

VISION.md:
- {Section}: {Current} → {Proposed}

ARCHITECTURE.md:
- {Section}: {Current} → {Proposed}

ROADMAP.md:
- {Feature}: {Old status} → {New status}
- {Dependency}: {Change}

Approve updates? [Yes / Modify / Skip]
```

### Step 5: Apply Updates

On approval, update each document:
- Make surgical edits (don't rewrite entire docs)
- Preserve document structure
- Add notes for significant changes
- Update timestamps if present

### Step 6: Update Feature Status

If features changed, also update `.state.json`:

```json
{
  "features": {
    "F1": { "status": "complete" },
    "F2": { "status": "in_progress" }
  }
}
```

### Step 7: Confirm

```
✅ Docs Updated

Changes made:
- VISION.md: {summary of changes}
- ARCHITECTURE.md: {summary of changes}
- ROADMAP.md: {summary of changes}
- .state.json: {if updated}

Canonical docs now reflect current reality.
```

---

## What to Update

### VISION.md Updates
- Feature list (add/remove/modify)
- Scope changes (in/out adjustments)
- User story refinements
- Acceptance criteria updates
- Monetization tier changes

### ARCHITECTURE.md Updates
- Tech stack changes
- New components added
- Data model evolution
- API surface changes
- Integration patterns discovered

### ROADMAP.md Updates
- Feature status (pending → in_progress → complete)
- Dependency graph changes
- Phase reorganization
- New features discovered during build
- Features split or combined

---

## Examples

**After implementing auth differently than planned:**
```
/update-docs

Context: Just implemented auth with Clerk instead of custom JWT.

ARCHITECTURE.md update:
- Auth: "Custom JWT" → "Clerk"
- Add: Clerk webhook handlers
- Remove: JWT refresh token logic
```

**After feature scope changed:**
```
/update-docs

Context: Dashboard feature grew to include analytics.

VISION.md update:
- F2 Dashboard: Add analytics sub-feature
- Acceptance criteria: Add 3 new criteria

ROADMAP.md update:
- F2: Increase complexity estimate
- F5 Analytics: Mark as "merged into F2"
```

---

## Remember

- **Reality wins** - Docs serve the build, not the other way around
- **Surgical edits** - Don't rewrite, update specific sections
- **Preserve structure** - Keep document formats consistent
- **Note significant changes** - Future context will thank you
- **Update state** - Keep `.state.json` in sync with feature status
