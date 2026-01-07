---
description: Set a state value in .state.json
argument-hint: <key> <value> (e.g., mode greenfield)
---

# Set State

**Mission**: Manage project state via `.state.json`. Single source of truth for all project state.

---

## State Schema

`.state.json` contains all project state:

```json
{
  "mode": "greenfield",
  "app": {
    "name": null,
    "initialized": null,
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

**On context load/reload**, Claude reads this file to understand:
- Current mode (greenfield/enhancer)
- Current phase (0-3)
- All features and their status
- Current DDD position (which feature, which step)

---

## Usage

```
/set-state <key> <value>
```

**Arguments** (from `$ARGUMENTS`):
- First word: key name (supports dot notation: `app.name`)
- Second word: value to set

---

## Process

### Step 1: Parse Arguments

Extract key and value from `$ARGUMENTS`:
- Split by space
- First token = key
- Second token = value

**If no arguments (show current state):**
```
📊 Current State

Mode: {mode}
App: {app.name or "Not set"}
Phase: {app.phase}

Features:
{list features with status}

DDD:
- Feature: {ddd.feature or "None"}
- Step: {ddd.step or "N/A"}
```

### Step 2: Validate Key

**Valid top-level keys:**
- `mode`: Project mode (`greenfield` | `enhancer`)
- `app.name`: Application name
- `app.phase`: Current phase (0-3)

**Note:** `features` and `ddd` are managed by DDD commands, not directly via set-state.

### Step 3: Validate Value

**For `mode`:**
- Valid: `greenfield`, `enhancer`

**For `app.phase`:**
- Valid: `0`, `1`, `2`, `3`

**For `app.name`:**
- Valid: any string

### Step 4: Update State File

Read `.state.json`, update the specified key, write back.

For dot notation keys like `app.name`, update nested value.

### Step 5: Confirm

```
✅ State updated

{key}: {old_value} → {value}
```

---

## State File Details

**Location:** `.state.json` at project root (both modes)

**Default state:**
```json
{
  "mode": "greenfield",
  "app": {
    "name": null,
    "initialized": null,
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

**Feature entry (added by DDD commands):**
```json
{
  "features": {
    "F1": {
      "name": "User Authentication",
      "tier": "free",
      "status": "complete",
      "started": "2024-01-15T10:00:00Z",
      "completed": "2024-01-15T11:00:00Z"
    },
    "F2": {
      "name": "Dashboard",
      "tier": "free",
      "status": "in_progress",
      "started": "2024-01-15T11:30:00Z"
    }
  }
}
```

**DDD tracking (updated by DDD commands):**
```json
{
  "ddd": {
    "feature": "F2",
    "step": 3,
    "workspace": ".ddd_workspaces/F2-dashboard/"
  }
}
```

---

## Examples

**Set mode:**
```
/set-state mode enhancer
```

**Set app name:**
```
/set-state app.name "TaskFlow Pro"
```

**Set phase:**
```
/set-state app.phase 2
```

**Show current state (no args):**
```
/set-state

📊 Current State

Mode: greenfield
App: TaskFlow Pro
Phase: 2

Features:
- F1: User Authentication [complete]
- F2: Dashboard [in_progress]
- F3: Data Export [pending]

DDD:
- Feature: F2
- Step: 3 (Code Breakdown)
```
