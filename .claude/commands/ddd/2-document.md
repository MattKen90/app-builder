---
description: DDD Step 2 - Create user-facing documentation before implementation
---

# DDD Step 2: Document

**Mission**: Create user-facing documentation for the feature BEFORE building it. Document what we're about to build, not what we built.

**Mode-Aware**: Reads `.mode` file to determine paths.

---

## Mode Detection

| Resource | Greenfield | Enhancer |
|----------|------------|----------|
| Workspaces | `.ddd_workspaces/` | `.enhancer/workspaces/` |
| Architecture | `ARCHITECTURE.md` | `.enhancer/ARCHITECTURE.md` |
| Docs | `docs/features/` | `.enhancer/docs/features/` |

---

**Input** (paths depend on mode):
- `{WORKSPACE_PATH}/{feature}/FEATURE_SPEC.md`
- `{ARCHITECTURE_PATH}` (for technical context)

**Output**:
- `{WORKSPACE_PATH}/{feature}/DOCS_DRAFT.md` (draft documentation)
- Ready for user review and approval

---

## Why Document Before Code?

1. **Forces clarity** - If you can't document it, you don't understand it
2. **User perspective** - Writing docs reveals UX issues before coding
3. **Contract** - Docs become the spec for what implementation must deliver
4. **No "docs debt"** - Documentation is never an afterthought

---

## Process

### Step 1: Load Context

Read:
- `.ddd_workspaces/{feature}/FEATURE_SPEC.md`
- `ARCHITECTURE.md` (relevant sections)
- Existing `docs/features/*.md` (for consistency)

Extract:
- Feature name and purpose
- User-facing functionality
- How users will interact with it
- Any configuration or setup needed

### Step 2: Generate Documentation Draft

Create `.ddd_workspaces/{feature}/DOCS_DRAFT.md`:

```markdown
# {Feature Name}

{One-sentence description of what this feature does.}

## Overview

{2-3 paragraphs explaining:
- What problem this solves
- Who it's for
- High-level how it works}

## Quick Start

{Minimal steps to get the feature working. Copy-paste executable.}

### Prerequisites
- {prerequisite 1}
- {prerequisite 2}

### Basic Usage

```bash
# Example command or code
{example}
```

Expected output:
```
{what user should see}
```

## Features

### {Feature 1}
{Description and usage}

### {Feature 2}
{Description and usage}

## Configuration

{Any configuration options, environment variables, settings}

| Option | Default | Description |
|--------|---------|-------------|
| | | |

## Examples

### Example 1: {Common Use Case}
```
{complete, working example}
```

### Example 2: {Another Use Case}
```
{complete, working example}
```

## Troubleshooting

### {Common Issue 1}
**Symptom**: {what user sees}
**Cause**: {why it happens}
**Solution**: {how to fix}

### {Common Issue 2}
**Symptom**: {what user sees}
**Cause**: {why it happens}
**Solution**: {how to fix}

## API Reference (if applicable)

{Endpoints, functions, or interfaces exposed}

---

**Related Features**: {links to related feature docs}
```

### Step 3: Apply Documentation Standards

Verify against the 6 rules:

**Rule 1: Fresh Context**
- No assumed knowledge
- Explain all concepts used
- Link to dependencies if needed

**Rule 2: Current State Only**
- No version references
- No "previously" or "now"
- Write as if feature always existed

**Rule 3: Complete, Not Fragmented**
- All info about this feature in this doc
- Don't duplicate other docs (link instead)

**Rule 4: Progressive Disclosure**
- Quick Start first
- Details later
- User can stop reading at any point with useful knowledge

**Rule 5: Executable Examples**
- Every example copy-paste works
- Include expected output
- Include prerequisites

**Rule 6: Reflect Reality**
- Document what WILL exist after implementation
- Be specific about behavior

### Step 4: Self-Review Checklist

Before presenting to user, verify:

```
Documentation Quality Check:

[ ] Title clearly states what feature does
[ ] Overview explains problem and solution
[ ] Quick Start gets user running in <5 minutes
[ ] All examples are complete and executable
[ ] Configuration options documented
[ ] Troubleshooting covers likely issues
[ ] No assumed knowledge (fresh context)
[ ] No version references (current state only)
[ ] Consistent with existing docs style
```

### Step 5: Present to User

```
📝 Documentation Draft Complete

Feature: {Feature ID} - {Feature Name}
File: .ddd_workspaces/{feature}/DOCS_DRAFT.md

## Preview

{Show first 50 lines or key sections}

---

## Quality Check

✅ Fresh context (no assumed knowledge)
✅ Executable examples included
✅ Troubleshooting section complete
✅ Consistent with docs style

---

Please review:
1. Does this accurately describe the feature?
2. Are the examples realistic?
3. Anything missing for users?

Options:
- Approve → Proceed to Step 3
- Request changes → I'll revise
- Major concerns → Discuss before proceeding
```

### Step 6: Handle Revisions

If user requests changes:
1. Understand the feedback
2. Update DOCS_DRAFT.md
3. Show diff or revised sections
4. Re-present for approval

Loop until approved.

### Step 7: Update State

```json
{
  "features": {
    "{feature-id}": {
      "steps": {
        "1": { "completed": "..." },
        "2": { "completed": "{timestamp}" }
      }
    }
  },
  "ddd": {
    "current_step": "2"
  }
}
```

### Step 8: Handoff

```
✅ DDD Step 2 Complete: Documentation Draft Approved

**Feature**: {Feature ID} - {Feature Name}
**Documentation**: .ddd_workspaces/{feature}/DOCS_DRAFT.md

The documentation now serves as the contract for implementation.
Step 4 (Implement) must deliver what these docs describe.

Ready for Step 3: Code-Breakdown

Run: /ddd:3
```

---

## Edge Cases

### Missing FEATURE_SPEC.md

```
⚠️ Missing prerequisite: FEATURE_SPEC.md

DDD steps run in order:
✅ Step 1: Understand (FEATURE_SPEC.md exists)
❌ Step 2: Document (current) - Can't find spec

Expected: .ddd_workspaces/{feature}/FEATURE_SPEC.md

Please run: /ddd:1
```

### Feature Has No User-Facing Components

```
ℹ️ Internal Feature Detected

This feature ({feature-name}) appears to be internal infrastructure
with no direct user interaction.

Options:
1. Create technical documentation (for developers)
2. Skip documentation (mark as internal)
3. Identify user-facing aspects I missed

Which approach?
```

If skipping:
- Create minimal DOCS_DRAFT.md noting "Internal feature - no user docs"
- Proceed to Step 3

### Documentation Would Duplicate Existing Docs

```
ℹ️ Overlap Detected

This feature's documentation would overlap with:
- docs/features/F1-user-authentication.md

Options:
1. Reference existing doc (add section there)
2. Create standalone doc with links
3. Merge features (go back to ROADMAP.md)

Recommended: Option 2 (standalone with links)
```

### User Wants Minimal Docs

```
⚠️ Documentation Scope

You've requested minimal documentation.

Minimum viable doc includes:
- One-sentence description
- Quick Start (how to use)
- One example

This is acceptable for simple features.

Proceed with minimal docs? [Yes / Full docs]
```

---

## Documentation Templates by Feature Type

### API Feature
- Endpoints list
- Request/response examples
- Authentication requirements
- Error codes

### UI Feature
- Screenshots/mockups placeholder
- User flow description
- Form fields and validation
- Keyboard shortcuts

### CLI Feature
- Command syntax
- All flags and options
- Exit codes
- Piping/scripting examples

### Data Feature
- Schema/model description
- Import/export formats
- Migration notes
- Backup/restore

---

## Success Criteria

After Step 2 completion:
- [x] DOCS_DRAFT.md created in workspace
- [x] Follows 6 documentation rules
- [x] Examples are executable (will be, after implementation)
- [x] User has reviewed and approved
- [x] State updated
- [x] Ready for /ddd:3

---

**Step 2 creates the user contract. Implementation must deliver what docs promise.**
