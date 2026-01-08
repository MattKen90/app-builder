# Discovery: App Builder

**Discovered**: 2026-01-07
**Status**: Enhancement Ready

---

## Executive Summary

App Builder is a Claude Code framework that inverts traditional development: AI designs and builds, humans approve. It guides users through a 4-phase process (Discovery, Vision, Architecture, Build) to create monetizable applications. The framework is feature-complete for its core workflow but has no apps built with it yet—it's infrastructure awaiting use.

---

## Tech Stack

| Layer | Technology | Version | Notes |
|-------|------------|---------|-------|
| Language | Markdown | N/A | Configuration and documentation |
| Framework | Claude Code | Latest | Slash commands, skills, agents, rules |
| Runtime | Claude AI | Opus/Sonnet | Executes all framework logic |
| State | JSON | N/A | .state.json for persistence |
| Payments | Stripe | N/A | Designed into apps built by framework |
| Hosting | N/A | N/A | Runs in Claude Code sessions |

**Key Insight**: App Builder is NOT a traditional application—it's a meta-framework. It has no backend, no database, no deployment. It's a collection of Claude Code primitives that orchestrate AI-driven app development.

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                     APP BUILDER FRAMEWORK                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  User Input ──→ /phases/N commands ──→ Agent Execution          │
│                       │                        │                │
│                       ▼                        ▼                │
│              .state.json ←───────────→ Document Output          │
│            (state tracking)          (VISION.md, etc.)          │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                     PRIMITIVE LAYERS                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │   Commands   │  │    Rules     │  │   Agents     │          │
│  │  (13 total)  │  │  (4 files)   │  │  (3 files)   │          │
│  └──────────────┘  └──────────────┘  └──────────────┘          │
│         │                 │                 │                   │
│         └─────────────────┼─────────────────┘                   │
│                           ▼                                     │
│                  ┌──────────────┐                               │
│                  │   Skills     │                               │
│                  │ (builder +   │                               │
│                  │  reference)  │                               │
│                  └──────────────┘                               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Directory Structure

```
app-builder/
├── .claude/
│   ├── agents/                    # AI persona definitions
│   │   ├── discovery-architect.md # Phase 0 agent
│   │   ├── vision-architect.md    # Phase 1 agent
│   │   └── tech-architect.md      # Phase 2 agent
│   │
│   ├── commands/                  # Slash commands
│   │   ├── phases/                # Core workflow
│   │   │   ├── 0.md               # Discovery (enhancer)
│   │   │   ├── 1.md               # Vision synthesis
│   │   │   ├── 2.md               # Technical foundation
│   │   │   └── 3.md               # Build orchestrator
│   │   │
│   │   ├── ddd/                   # Document-Driven Design
│   │   │   ├── 1-understand.md    # Spec approval
│   │   │   ├── 2-document.md      # User docs first
│   │   │   ├── 3-code-breakdown.md# Implementation plan
│   │   │   ├── 4-implement.md     # Build phase
│   │   │   └── 5-review.md        # Finalization
│   │   │
│   │   ├── app/                   # App-specific (empty)
│   │   ├── set-state.md           # State management
│   │   ├── update-docs.md         # Doc sync
│   │   ├── create-new-feature.md  # Feature addition
│   │   └── discovery.md           # Discovery command
│   │
│   ├── rules/                     # Behavior rules
│   │   ├── architecture.md        # System design rules
│   │   ├── development.md         # Coding practices
│   │   ├── revenue.md             # MRR-first mindset
│   │   └── python.md              # Python constraints
│   │
│   └── skills/
│       ├── app/                   # App skills (empty)
│       └── claude-code-builder/   # Builder reference
│           ├── SKILL.md           # Entry point
│           └── docs/              # Comprehensive docs
│               ├── hooks/
│               ├── mcp/
│               ├── plugins/
│               ├── skills/
│               ├── slash-commands/
│               └── subagents/
│
├── .state.json                    # State persistence
├── .ddd_workspaces/               # DDD working dirs (empty)
├── .enhancer/                     # Enhancer artifacts
│   └── DISCOVERY.md               # This document
│
├── app/                           # Built app location (empty)
├── docs/features/                 # Feature docs (empty)
├── playbooks/                     # Deployment scripts (empty)
│
├── CLAUDE.md                      # Quick start entry
└── README.md                      # Full documentation
```

### Key Files

| File | Purpose |
|------|---------|
| `.state.json` | Single source of truth for project state |
| `CLAUDE.md` | Entry point, loaded on context start |
| `.claude/rules/architecture.md` | Core architecture principles |
| `.claude/rules/revenue.md` | MRR-first philosophy |
| `.claude/agents/*.md` | Agent definitions with modes |

---

## Existing Claude Code Setup

### CLAUDE.md Summary

Quick start guide pointing to:
- Mode setting: `/set-state mode greenfield|enhancer`
- Phase commands: `/phases/0-3`
- DDD commands: `/ddd/1-5`
- State file: `.state.json`

### Existing Commands

| Command | Purpose |
|---------|---------|
| `/set-state` | Manage project state |
| `/phases/0` | Discovery (enhancer only) |
| `/phases/1` | Vision synthesis |
| `/phases/2` | Technical foundation |
| `/phases/3` | Build orchestrator |
| `/ddd/1` | Understand feature spec |
| `/ddd/2` | Document before building |
| `/ddd/3` | Code breakdown |
| `/ddd/4` | Implementation |
| `/ddd/5` | Review and finalize |
| `/update-docs` | Sync documentation |
| `/create-new-feature` | Add new feature |
| `/discovery` | Run discovery analysis |

### Existing Rules

| Rule | Purpose |
|------|---------|
| `architecture.md` | System design, DDD process, factory model |
| `development.md` | Coding practices, agent delegation |
| `revenue.md` | MRR-first, Stripe default, paywall patterns |
| `python.md` | Deterministic-only Python (no LLM APIs) |

### Existing Agents

| Agent | Purpose |
|-------|---------|
| `discovery-architect` | Phase 0 - Maps existing codebases |
| `vision-architect` | Phase 1 - Extracts and expands vision |
| `tech-architect` | Phase 2 - Designs architecture and roadmap |

**Conflicts to Avoid**: None identified. App primitives go in `/app/` subdirectories.

---

## Data Model

### State Entity

The only persistent data is `.state.json`:

```json
{
  "mode": "greenfield|enhancer",
  "target": "path|null",
  "app": {
    "name": "string",
    "initialized": "timestamp",
    "phase": 0-3
  },
  "features": {
    "F1": {
      "name": "string",
      "tier": "free|paid|enterprise",
      "status": "pending|in_progress|complete",
      "started": "timestamp",
      "completed": "timestamp"
    }
  },
  "ddd": {
    "feature": "F1",
    "step": 1-5,
    "workspace": "path",
    "last_action": "string",
    "last_checkpoint": "timestamp"
  }
}
```

### Document Artifacts

| Phase | Output | Location |
|-------|--------|----------|
| 0 | DISCOVERY.md | `.enhancer/` |
| 1 | VISION.md | Root or `.enhancer/` |
| 2 | ARCHITECTURE.md, ROADMAP.md | Root or `.enhancer/` |
| 3 | Feature code, docs | `app/`, `docs/features/` |

---

## API Surface

**N/A** - App Builder has no API. It's a Claude Code primitive collection that executes within Claude sessions.

### Interface Pattern

- **Input**: User messages, slash commands
- **Processing**: Claude Code executes commands, invokes agents
- **Output**: Documents (Markdown), code (in `app/`), state updates

---

## Monetization Assessment

### Current State

- **Payment Provider**: N/A (App Builder itself doesn't process payments)
- **Pricing Model**: N/A (Framework is free to use)
- **MRR Infrastructure**: N/A (Not applicable to the framework)

### What Exists

App Builder is designed to BUILD monetizable apps, not BE a monetizable app:

- [x] Revenue rules enforcing MRR-first thinking
- [x] Stripe integration patterns in architecture docs
- [x] Feature tier system (Free/Paid/Enterprise)
- [x] Paywall guidance in revenue rules
- [ ] No revenue from App Builder itself

### Key Insight

**App Builder is infrastructure, not product.** It's a tool for building revenue-generating apps, but the framework itself has no monetization. This is intentional—it's like a hammer that builds houses but isn't itself a house.

---

## Code Patterns to Follow

### Command Pattern

Commands are Markdown files with YAML frontmatter:
```yaml
---
description: What this command does
argument-hint: Expected arguments
---
```

Body contains instructions for Claude to execute.

### Agent Pattern

Agents are Markdown files with extensive YAML frontmatter:
```yaml
---
name: agent-name
description: What the agent does
model: inherit
---
```

Body defines persona, operating modes, and mandatory outputs.

### Rule Pattern

Rules are Markdown files that shape Claude's behavior. Can have path filters:
```yaml
---
paths: **/*.py
---
```

### State Management Pattern

All state goes in `.state.json`. Commands read/write via:
1. Read current state
2. Validate changes
3. Update specific keys
4. Write back full state

### Document-Driven Design

Every phase produces canonical documents. Work that isn't in a document doesn't exist. Agents are ephemeral, documents persist.

---

## Enhancement Opportunities

### Quick Wins (Low effort, high impact)

1. **Example App Template**: Add a working example in `app/` showing the output of a complete DDD cycle. Users currently see an empty folder.

2. **State Visualization**: Add `/show-state` command that renders `.state.json` as a visual progress dashboard.

3. **Checkpoint/Resume Messaging**: Improve `last_action` field usage to give better context on session resume.

### Revenue Gaps (MRR opportunities for the framework itself)

1. **Premium Agents**: Offer specialized agents (e.g., "mobile-architect", "saas-architect") as paid add-ons.

2. **Template Marketplace**: Pre-built VISION.md + ARCHITECTURE.md templates for common app types (SaaS, mobile, CLI tool).

3. **Deployment Automation**: Playbooks are empty—filling them could be a premium feature.

### Technical Debt

1. **Empty Directories**: `app/`, `playbooks/`, `docs/features/`, `.ddd_workspaces/` are all empty with only `.gitkeep`. No examples for users to reference.

2. **Circular Self-Reference**: This discovery is targeting App Builder itself, which is unusual. Normally this would analyze an external app.

3. **Missing Phase 3 Agent**: Phases 0-2 have dedicated agents. Phase 3 (Build) relies on DDD commands but has no orchestrating agent.

4. **No Testing Framework**: No guidance on how to test apps built with App Builder.

---

## Constraints & Considerations

### Must Preserve

| Constraint | Reason |
|------------|--------|
| MRR-first philosophy | Core differentiator |
| Document-driven approach | Handles context compaction |
| State in .state.json | Single source of truth |
| Claude Code primitives only | No external dependencies |
| Phase sequence (0→1→2→3) | Logical progression |

### Integration Points

- **Claude Code**: Framework runs entirely within Claude Code
- **Stripe**: Apps built by framework integrate with Stripe
- **Target App**: Enhancer mode operates on external codebases

### Risk Areas

1. **Self-Enhancement Paradox**: Enhancing App Builder with App Builder is meta. Changes to core commands/rules could break the enhancement process.

2. **State Schema Changes**: Any changes to `.state.json` schema need backward compatibility.

3. **Agent Instruction Drift**: Changes to agent prompts could subtly alter behavior in hard-to-test ways.

---

## Ready for Phase 1

Discovery complete. This document provides the foundation for:

- **Phase 1 (Vision)**: Define WHAT enhancements to build
- **Phase 2 (Architecture)**: Design HOW to build them
- **Phase 3 (Build)**: Implement via DDD

Next: Run `/phases/1` to begin Vision synthesis

---

## Appendix: File Inventory

| Path | Lines | Purpose |
|------|-------|---------|
| `.claude/agents/discovery-architect.md` | 425 | Phase 0 agent |
| `.claude/agents/vision-architect.md` | 532 | Phase 1 agent |
| `.claude/agents/tech-architect.md` | 501 | Phase 2 agent |
| `.claude/rules/architecture.md` | 410 | Core architecture |
| `.claude/rules/revenue.md` | 259 | MRR philosophy |
| `.claude/rules/development.md` | 37 | Dev practices |
| `.claude/rules/python.md` | 34 | Python rules |
| `.claude/commands/ddd/1-understand.md` | 489 | DDD step 1 |
| `README.md` | 270 | User documentation |
| `CLAUDE.md` | 24 | Entry point |

Total: ~3000 lines of framework definition.
