---
description: Set a state value in .state.json
argument-hint: <key> <value> (e.g., mode greenfield)
---

# Set State

**Mission**: Manage project state via `.state.json`. All commands read from this file.

---

## Usage

```
/set-state <key> <value>
```

**Arguments** (from `$ARGUMENTS`):
- First word: key name
- Second word: value to set

---

## Process

### Step 1: Parse Arguments

Extract key and value from `$ARGUMENTS`:
- Split by space
- First token = key
- Second token = value

**If arguments missing or incomplete:**
```
⚠️ Usage: /set-state <key> <value>

Available keys:
- mode: greenfield | enhancer

Current state:
{show contents of .state.json}

Example: /set-state mode enhancer
```

### Step 2: Validate Key

**Valid keys:**
- `mode`: Project mode (`greenfield` or `enhancer`)

**If invalid key:**
```
⚠️ Unknown key: "{key}"

Available keys:
- mode: greenfield | enhancer
```

### Step 3: Validate Value

**For `mode`:**
- Valid: `greenfield`, `enhancer`
- Invalid: anything else

**If invalid value:**
```
⚠️ Invalid value for {key}: "{value}"

Valid values for mode:
- greenfield: Build new apps from scratch
- enhancer: Enhance existing apps
```

### Step 4: Update State File

Read `.state.json` (create if doesn't exist):

```json
{
  "mode": "greenfield"
}
```

Update the specified key with new value.

Write back to `.state.json`.

### Step 5: Confirm

```
✅ State updated

{key}: {old_value} → {value}

Current state:
{
  "mode": "{value}"
}
```

---

## State File Location

`.state.json` at project root.

**Default state:**
```json
{
  "mode": "greenfield"
}
```

---

## How Other Commands Use State

All mode-aware commands read `.state.json`:

```python
import json

def get_state():
    try:
        with open('.state.json', 'r') as f:
            return json.load(f)
    except FileNotFoundError:
        return {"mode": "greenfield"}

state = get_state()
mode = state.get("mode", "greenfield")
```

---

## Examples

**Set mode to enhancer:**
```
/set-state mode enhancer

✅ State updated
mode: greenfield → enhancer
```

**Invalid key:**
```
/set-state foo bar

⚠️ Unknown key: "foo"

Available keys:
- mode: greenfield | enhancer
```

**Invalid value:**
```
/set-state mode invalid

⚠️ Invalid value for mode: "invalid"

Valid values for mode:
- greenfield: Build new apps from scratch
- enhancer: Enhance existing apps
```

**No arguments (show current state):**
```
/set-state

⚠️ Usage: /set-state <key> <value>

Available keys:
- mode: greenfield | enhancer

Current state:
{
  "mode": "greenfield"
}
```
