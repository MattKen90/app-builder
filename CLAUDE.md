# App Builder

Lightweight, Claude Code-first framework for building complete applications. Zero API costs—subscription only.

## Philosophy

**Human = Operator.** Minimal involvement. Provides intent, approves direction.

**AI = Driver.** Full ownership of product vision, feature selection, research, and implementation.

**Spec-Driven Design (SDD).** Human specs what they want, AI expands and builds it.

## Core Primitives

- **Slash Commands** (`.claude/commands/`) - DDD workflow automation
- **Agents** (`.claude/agents/`) - Specialized task delegation
- **Rules** (`.claude/rules/`) - Architecture, development, and Python constraints
- **State** (`.state/`) - Project tracking and metrics

## Project Structure

```
app-builder/
├── CLAUDE.md                    # This file
├── .claude/
│   ├── rules/                   # Constraints and architecture
│   │   ├── architecture.md      # Factory phases, DDD process
│   │   ├── development.md       # Development rules
│   │   └── python.md            # Python: deterministic only
│   ├── agents/                  # Subagent definitions
│   │   ├── vision-architect.md  # Phase 1: Vision synthesis
│   │   └── tech-architect.md    # Phase 2: Technical foundation
│   └── commands/ddd/            # DDD slash commands
│       ├── 1-understand.md      # Select feature, create spec
│       ├── 2-document.md        # Document before coding
│       ├── 3-code-breakdown.md  # Break into phases
│       ├── 4-implement.md       # Execute with checkpoints
│       └── 5-review.md          # Finalize and complete
├── .state/
│   └── project.json             # Project state and tracking
├── .ddd_workspaces/             # Active feature workspaces
├── docs/features/               # Final feature documentation
└── playbooks/                   # Deployment automation scripts
```

## The Factory

Three phases transform idea → working app:

1. **Vision Synthesis** → `VISION.md` (features, scope)
2. **Technical Foundation** → `ARCHITECTURE.md`, `ROADMAP.md`
3. **Feature Implementation** → Working code via DDD loop

## Quick Start

```
# Phase 1: Vision
Use vision-architect agent to produce VISION.md

# Phase 2: Architecture
Use tech-architect agent to produce ARCHITECTURE.md + ROADMAP.md

# Phase 3: Build (repeat for each feature)
/ddd:1  → Understand (create FEATURE_SPEC.md)
/ddd:2  → Document (create DOCS_DRAFT.md)
/ddd:3  → Code-Breakdown (create IMPLEMENTATION_PLAN.md)
/ddd:4  → Implement (write code, tests)
/ddd:5  → Review (finalize, complete)
```

## Rules

See `.claude/rules/` for detailed constraints:
- **architecture.md** - Full factory model, phases, document flow
- **development.md** - Agent delegation, zero-BS, regenerate don't patch
- **python.md** - Deterministic only, no LLM API calls
