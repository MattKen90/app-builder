# App Builder

Framework for building monetizable apps with Claude Code. MRR is King.

## Quick Start

```
/set-state mode greenfield    # or: /set-state mode enhancer
/phases/1                     # Vision
/phases/2                     # Architecture
/phases/3                     # Build
```

Enhancer mode: Run `/phases/0` first to analyze existing codebase.

## Commands

| Command | Purpose |
|---------|---------|
| `/set-state mode <mode>` | Set greenfield or enhancer |
| `/set-state target <path>` | Set target app (enhancer) |
| `/phases/0` | Discovery (enhancer only) |
| `/phases/1` | Vision |
| `/phases/2` | Technical Foundation |
| `/phases/3` | Build (DDD cycle) |
| `/ddd/1` - `/ddd/5` | DDD steps (direct access) |

## On Context Load

Read `.state.json` to understand current state:
- Mode (greenfield/enhancer)
- Current phase
- Features and their status
- Current DDD position
