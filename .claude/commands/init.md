---
description: Initialize project structure based on current mode (greenfield or enhancer)
---

# Init

**Mission**: Initialize the project structure based on the current mode. Reads `.state.json` and sets up appropriate directories.

**Prerequisites**: Mode should be set via `/set-state mode <greenfield|enhancer>`

**Output**:
- Greenfield: `.ddd_workspaces/`, `docs/features/`, `playbooks/`
- Enhancer: `.enhancer/` beachhead with subdirectories
- Updated `.state.json` with initialization timestamp

---

## Process

### Step 1: Check Mode

Read `.state.json` file:

```
🔍 Checking mode...
```

**If mode not set or file missing:**
```
⚠️ Mode Not Set

Please set mode first:

/set-state mode greenfield  - Building a new app from scratch
/set-state mode enhancer    - Enhancing an existing app

Then run /init again.
```

### Step 2: Branch by Mode

---

## Greenfield Mode

### Verify Not Already Initialized

```
🔍 Checking existing structure...

- .ddd_workspaces/ exists: {Yes/No}
- app.initialized in .state.json: {Yes/No}
```

**If already initialized:**
```
ℹ️ Already Initialized (Greenfield)

Project structure already exists.

Options:
1. Continue with existing setup
2. Reset (delete and reinitialize)
3. Cancel

Which option?
```

### Create Structure

```bash
mkdir -p .ddd_workspaces
mkdir -p docs/features
mkdir -p playbooks
```

### Update State

Update `.state.json`:

```json
{
  "mode": "greenfield",
  "app": {
    "name": null,
    "initialized": "{timestamp}",
    "phase": 1
  },
  "features": {},
  "ddd": {
    "feature": null,
    "step": null,
    "workspace": null
  }
}
```

### Present Completion

```
✅ Greenfield Project Initialized

Structure created:
├── .state.json           # All project state
├── .ddd_workspaces/      # Feature workspaces
├── docs/features/        # Feature documentation
└── playbooks/            # Deployment automation

Next Steps:
1. Run /phases/1 to define your vision
2. Or invoke vision-architect directly

Ready to begin!
```

---

## Enhancer Mode

### Verify Context

```
🔍 Checking repository...

Current directory: {cwd}

Verifying:
- [ ] Has existing code (not empty)
- [ ] .enhancer/ doesn't already exist
```

**If empty repo:**
```
⚠️ Empty Repository

This repository appears to be empty or nearly empty.
Enhancer mode is for existing apps with code to enhance.

For building from scratch:
/set-state mode greenfield
/init
```

**If .enhancer/ already exists:**
```
ℹ️ Already Initialized (Enhancer)

.enhancer/ beachhead already exists.

Options:
1. Continue with existing setup
2. Reset (archive existing and reinitialize)
3. Cancel

Which option?
```

### Create Beachhead

```bash
mkdir -p .enhancer/workspaces
mkdir -p .enhancer/docs/features
```

### Update State

Update `.state.json`:

```json
{
  "mode": "enhancer",
  "app": {
    "name": null,
    "initialized": "{timestamp}",
    "phase": 0
  },
  "features": {},
  "ddd": {
    "feature": null,
    "step": null,
    "workspace": null
  }
}
```

### Quick Repo Assessment

```
📊 Quick Assessment

Repository: {name}
Path: {path}

Detected:
- Language: {detected or "Unknown"}
- Framework: {detected or "Unknown"}
- Has CLAUDE.md: {Yes/No}
- Has .claude/: {Yes/No}
```

### Present Completion

```
✅ Enhancer Beachhead Initialized

Structure created:
├── .state.json                 # All project state
└── .enhancer/                  # Your beachhead
    ├── workspaces/             # DDD workspaces
    └── docs/features/          # Feature documentation

Next Steps:
1. Run /phases/0 to analyze this codebase
2. Review .enhancer/DISCOVERY.md
3. Continue with /phases/1, /phases/2, /phases/3

Ready to begin discovery?
→ Run: /phases/0
```

---

## Path Reference

Commands use these paths based on mode:

| Resource | Greenfield | Enhancer |
|----------|------------|----------|
| State | `.state.json` | `.state.json` |
| Workspaces | `.ddd_workspaces/` | `.enhancer/workspaces/` |
| Feature docs | `docs/features/` | `.enhancer/docs/features/` |
| Vision | `VISION.md` | `.enhancer/VISION.md` |
| Architecture | `ARCHITECTURE.md` | `.enhancer/ARCHITECTURE.md` |
| Roadmap | `ROADMAP.md` | `.enhancer/ROADMAP.md` |
| Feature IDs | F1, F2, F3 | E-F1, E-F2, E-F3 |

**Note:** State is ALWAYS in `.state.json` at project root, regardless of mode.

---

**Init sets up the foundation. Mode determines the structure.**
