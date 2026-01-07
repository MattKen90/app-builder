---
description: Set the App Builder mode (greenfield or enhancer)
argument-hint: <greenfield|enhancer>
---

# Mode

**Mission**: Set the operating mode for this project. All other commands read this mode and adapt accordingly.

**Modes**:
- `greenfield` - Building a new app from scratch
- `enhancer` - Enhancing an existing app

**Output**: `.mode` file at project root

---

## Usage

```
/mode greenfield    # Set to greenfield mode
/mode enhancer      # Set to enhancer mode
/mode               # Show current mode
```

---

## Process

### If No Argument: Show Current Mode

Read `.mode` file and display:

```
📋 Current Mode

Mode: {greenfield|enhancer|not set}
Mode file: .mode

{If greenfield}:
- State: .state/
- Workspaces: .ddd_workspaces/
- Feature IDs: F1, F2, F3...

{If enhancer}:
- State: .enhancer/state/
- Workspaces: .enhancer/workspaces/
- Feature IDs: E-F1, E-F2, E-F3...
- Beachhead: .enhancer/

To change mode: /mode <greenfield|enhancer>
```

### If Argument Provided: Set Mode

#### Validate Argument

```
{if argument is not "greenfield" or "enhancer"}:

⚠️ Invalid Mode

Valid modes:
- greenfield : Build new apps from scratch
- enhancer   : Enhance existing apps

Usage: /mode <greenfield|enhancer>
```

#### Set Mode

Write to `.mode`:

```
{mode}
```

That's it. Just the mode name, nothing else.

#### Confirm

```
✅ Mode Set: {mode}

Mode file: .mode

{If greenfield}:
Next steps:
1. Run /init to initialize project structure
2. Use vision-architect for Phase 1
3. Use tech-architect for Phase 2
4. Run /ddd/1 to start building features

{If enhancer}:
Next steps:
1. Run /init to create .enhancer/ beachhead
2. Run /discovery for Phase 0 (analyze codebase)
3. Use vision-architect for Phase 1 (output to .enhancer/)
4. Use tech-architect for Phase 2 (output to .enhancer/)
5. Run /ddd/1 to start building enhancements
```

---

## Mode Switching

If switching modes when work exists:

```
⚠️ Mode Switch Warning

Current mode: {current}
Requested mode: {new}

Existing work detected:
- {.state/ exists / .enhancer/ exists}
- {N} features in progress

Switching modes will NOT delete existing work, but commands
will now use {new mode} paths.

Continue? [Yes / No]
```

---

## How Commands Use Mode

Every command reads `.mode` to determine:

| Aspect | Greenfield | Enhancer |
|--------|------------|----------|
| State path | `.state/` | `.enhancer/state/` |
| Workspaces | `.ddd_workspaces/` | `.enhancer/workspaces/` |
| Docs | `docs/features/` | `.enhancer/docs/features/` |
| Feature prefix | F | E-F |
| Vision output | `VISION.md` | `.enhancer/VISION.md` |
| Architecture output | `ARCHITECTURE.md` | `.enhancer/ARCHITECTURE.md` |
| Phase 0 | Skipped | Required |

---

## Default Behavior

If `.mode` file doesn't exist:
- Commands will prompt to set mode first
- Or assume greenfield for backwards compatibility

```
ℹ️ Mode Not Set

No .mode file found. Please set mode first:

/mode greenfield  - Building a new app from scratch
/mode enhancer    - Enhancing an existing app

Which mode?
```

---

**Mode is the foundation. Set it first, everything else follows.**
