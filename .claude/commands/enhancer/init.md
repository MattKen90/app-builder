---
description: Initialize the App Enhancer beachhead in the current repository
---

# Enhancer Init

**Mission**: Set up the enhancer beachhead in the current repository. Creates `.enhancer/` directory structure and initializes state.

**Prerequisites**:
- You are in a repository you want to enhance (not app-builder itself)
- The repo has existing code to enhance

**Output**:
- `.enhancer/` beachhead directory structure
- `.enhancer/state/project.json` initialized
- Ready for `/enhancer/discovery`

---

## Process

### Step 1: Verify Context

Check that we're in a suitable repo:

```
🔍 Checking repository...

Current directory: {cwd}

Verifying:
- [ ] Not the app-builder repo itself
- [ ] Has existing code (not empty)
- [ ] .enhancer/ doesn't already exist (or confirm overwrite)
```

**If in app-builder repo:**
```
⚠️ Cannot Initialize Here

You're in the app-builder repo itself. The enhancer is meant to be
used on OTHER repositories.

To enhance an existing app:
1. Navigate to that repo
2. Run /enhancer/init from there

Or for greenfield development, use /ddd/1 directly.
```

**If .enhancer/ already exists:**
```
⚠️ Enhancer Already Initialized

.enhancer/ directory already exists in this repo.

Options:
1. Continue with existing setup → Run /enhancer/discovery
2. Reset and start fresh → Confirm to delete and reinitialize
3. Cancel

Which option?
```

### Step 2: Create Beachhead Structure

```bash
mkdir -p .enhancer/{state,workspaces,docs/features}
```

Creates:
```
.enhancer/
├── state/
│   └── project.json      # Will be created
├── workspaces/           # DDD workspaces go here
└── docs/
    └── features/         # Feature documentation
```

### Step 3: Initialize State

Create `.enhancer/state/project.json`:

```json
{
  "enhancer": {
    "initialized": "{timestamp}",
    "target_repo": "{repo_name}",
    "phase": "0"
  },
  "discovery": {
    "status": "pending",
    "completed": null
  },
  "features": {},
  "ddd": {
    "current_feature": null,
    "current_step": null,
    "workspace": null
  },
  "metrics": {
    "features_completed": 0,
    "enhancements_shipped": 0
  }
}
```

### Step 4: Quick Repo Assessment

Do a quick scan to give the user context:

```
📊 Quick Assessment

Repository: {name}
Path: {path}

Detected:
- Language: {detected or "Unknown"}
- Framework: {detected or "Unknown"}
- Has CLAUDE.md: {Yes/No}
- Has .claude/: {Yes/No}
- Has package.json/requirements.txt/etc: {Yes/No}

Existing Claude Code setup:
- Commands: {count or "None"}
- Rules: {count or "None"}
- Agents: {count or "None"}
```

### Step 5: Present Completion

```
✅ Enhancer Initialized

Beachhead created at: .enhancer/

Structure:
.enhancer/
├── state/project.json    # Tracking state
├── workspaces/           # DDD workspaces
└── docs/features/        # Feature documentation

Next Steps:
1. Run /enhancer/discovery to analyze this codebase (Phase 0)
2. Review .enhancer/DISCOVERY.md when complete
3. Run /enhancer/vision to define enhancements (Phase 1)

Ready to begin discovery?
→ Run: /enhancer/discovery
```

### Step 6: Update State

```json
{
  "enhancer": {
    "initialized": "{timestamp}",
    "phase": "0"
  },
  "discovery": {
    "status": "ready"
  }
}
```

---

## What Init Does NOT Do

- Does NOT modify existing CLAUDE.md
- Does NOT add files outside .enhancer/ (except this is run as a command)
- Does NOT run discovery automatically (user should trigger that)
- Does NOT install commands into .claude/commands/enhancer/ (those come from app-builder)

---

## Edge Cases

### Empty Repository

```
⚠️ Empty Repository

This repository appears to be empty or nearly empty.
Enhancement mode is for existing apps with code to enhance.

For building from scratch, use greenfield mode:
1. Clone or copy app-builder structure
2. Use /ddd/1 directly

Continue anyway? [Yes / No]
```

### Already Has .enhancer/ with Work

```
⚠️ Existing Enhancement Work Detected

.enhancer/ exists with:
- DISCOVERY.md: {Exists/Missing}
- VISION.md: {Exists/Missing}
- Features in progress: {count}

Options:
1. Resume existing work → Don't reinitialize
2. Archive and start fresh → Move to .enhancer-backup-{timestamp}/
3. Delete and start fresh → Remove all enhancement work
4. Cancel

Which option?
```

---

## Success Criteria

Init is complete when:
- [x] .enhancer/ directory exists
- [x] .enhancer/state/project.json initialized
- [x] .enhancer/workspaces/ exists
- [x] .enhancer/docs/features/ exists
- [x] User informed of next steps
- [x] Ready for /enhancer/discovery

---

**Init creates the beachhead. Discovery maps the territory. Then we enhance.**
