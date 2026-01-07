---
description: Initialize project structure based on current mode (greenfield or enhancer)
---

# Init

**Mission**: Initialize the project structure based on the current mode. Reads `.state.json` and sets up appropriate directories and state.

**Prerequisites**: Mode should be set via `/set-state mode <greenfield|enhancer>`

**Output**:
- Greenfield: `.state/`, `.ddd_workspaces/`, `docs/features/`
- Enhancer: `.enhancer/` beachhead with all subdirectories

---

## Process

### Step 1: Check Mode

Read `.state.json` file:

```
🔍 Checking mode...
```

**If mode not set:**
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

- .state/ exists: {Yes/No}
- .ddd_workspaces/ exists: {Yes/No}
```

**If already initialized:**
```
ℹ️ Already Initialized (Greenfield)

Project structure already exists:
- .state/project.json
- .ddd_workspaces/
- docs/features/

Options:
1. Continue with existing setup
2. Reset (delete and reinitialize)
3. Cancel

Which option?
```

### Create Structure

```bash
mkdir -p .state
mkdir -p .ddd_workspaces
mkdir -p docs/features
mkdir -p playbooks
```

### Initialize State

Create `.state/project.json`:

```json
{
  "mode": "greenfield",
  "app": {
    "name": null,
    "started": "{timestamp}",
    "phase": "1"
  },
  "features": {},
  "ddd": {
    "current_feature": null,
    "current_step": null,
    "workspace": null
  },
  "metrics": {
    "features_completed": 0,
    "apps_completed": 0
  }
}
```

### Present Completion

```
✅ Greenfield Project Initialized

Structure created:
├── .state.json           # Project state (mode: greenfield)
├── .state/
│   └── project.json      # Project tracking
├── .ddd_workspaces/      # Feature workspaces
├── docs/features/        # Feature documentation
└── playbooks/            # Deployment automation

Next Steps:
1. Phase 1: Use vision-architect to produce VISION.md
2. Phase 2: Use tech-architect to produce ARCHITECTURE.md + ROADMAP.md
3. Phase 3: Run /ddd/1 to start building features

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
mkdir -p .enhancer/state
mkdir -p .enhancer/workspaces
mkdir -p .enhancer/docs/features
```

### Initialize State

Create `.enhancer/state/project.json`:

```json
{
  "mode": "enhancer",
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
├── .state.json                 # Project state (mode: enhancer)
└── .enhancer/                  # Your beachhead
    ├── state/project.json      # Project tracking
    ├── workspaces/             # DDD workspaces
    └── docs/features/          # Feature documentation

Next Steps:
1. Phase 0: Run /discovery to analyze this codebase
2. Review .enhancer/DISCOVERY.md
3. Phase 1: Use vision-architect for enhancement vision
4. Phase 2: Use tech-architect for architecture
5. Phase 3: Run /ddd/1 to start building enhancements

Ready to begin discovery?
→ Run: /discovery
```

---

## Path Reference

Commands use these paths based on mode:

| Resource | Greenfield | Enhancer |
|----------|------------|----------|
| State | `.state/project.json` | `.enhancer/state/project.json` |
| Workspaces | `.ddd_workspaces/` | `.enhancer/workspaces/` |
| Feature docs | `docs/features/` | `.enhancer/docs/features/` |
| Vision | `VISION.md` | `.enhancer/VISION.md` |
| Architecture | `ARCHITECTURE.md` | `.enhancer/ARCHITECTURE.md` |
| Roadmap | `ROADMAP.md` | `.enhancer/ROADMAP.md` |
| Feature IDs | F1, F2, F3 | E-F1, E-F2, E-F3 |

---

**Init sets up the foundation. Mode determines the structure.**
