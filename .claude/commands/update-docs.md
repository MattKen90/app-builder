---
description: Update VISION.md, ARCHITECTURE.md, and ROADMAP.md based on recent changes
allowed-tools: Read, Edit
---

# Update Docs

Sync canonical documents with reality based on current context knowledge.

## Current State

- State: @.state.json

## Current Docs (read based on mode from state)

**Greenfield:** @VISION.md @ARCHITECTURE.md @ROADMAP.md

**Enhancer:** Read from `.enhancer/` path

## Process

### 1. Identify Drift

Compare docs to what you know from recent work:
- What changed from the original plan?
- What technical decisions were made?
- What features were added/removed/modified?

### 2. Propose Updates

Present changes before applying:

```
📝 Proposed Updates

VISION.md: {changes}
ARCHITECTURE.md: {changes}
ROADMAP.md: {changes}

Approve? [Yes / Modify / Skip]
```

### 3. Apply Updates

On approval:
- Make surgical edits (don't rewrite)
- Preserve document structure
- Update `.state.json` if features changed

### 4. Confirm

```
✅ Docs Updated

- VISION.md: {summary}
- ARCHITECTURE.md: {summary}
- ROADMAP.md: {summary}
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
