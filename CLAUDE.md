# App Builder

Lightweight, Claude Code-first framework for building and enhancing monetizable applications. Zero API costs—subscription only.

## Two Modes

**Greenfield Mode**: Build new apps from scratch. Clone this repo and start building.

**Enhancer Mode**: Enhance existing apps. Install the enhancer beachhead into any repo.

## Prime Directive

**MRR is King.** Everything we build exists to generate Monthly Recurring Revenue. Not apps for apps' sake. Not beautiful code for beauty's sake. Revenue.

## Philosophy

**Revenue-First Development.** Every decision—from vision to deployment—asks: "How does this make money?" Monetization isn't an afterthought; it's the foundation.

**MVP, Fully Monetizable.** Ship fast, iterate fast. Not over-engineered perfection—functional products with clear paths to payment. Stripe-ready from day one.

**Human = Operator.** Minimal involvement. Provides intent, approves direction.

**AI = Driver.** Full ownership of product vision, feature selection, research, and implementation. Always considering revenue implications.

**Spec-Driven Design (SDD).** Human specs what they want, AI expands and builds it—with monetization baked in.

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
│   │   ├── revenue.md           # MRR-first, monetization
│   │   ├── architecture.md      # Factory phases, DDD process
│   │   ├── development.md       # Development rules
│   │   └── python.md            # Python: deterministic only
│   ├── agents/
│   │   ├── vision-architect.md  # Phase 1: Vision synthesis
│   │   ├── tech-architect.md    # Phase 2: Technical foundation
│   │   └── discovery-architect.md # Phase 0: Discovery (enhancer)
│   └── commands/
│       ├── ddd/                 # Greenfield DDD commands
│       │   ├── 1-understand.md
│       │   ├── 2-document.md
│       │   ├── 3-code-breakdown.md
│       │   ├── 4-implement.md
│       │   └── 5-review.md
│       └── enhancer/            # Enhancer mode commands
│           ├── init.md          # Initialize beachhead
│           ├── discovery.md     # Phase 0: Analyze codebase
│           └── ddd/             # Enhancement DDD commands
│               ├── 1-understand.md
│               ├── 2-document.md
│               ├── 3-code-breakdown.md
│               ├── 4-implement.md
│               └── 5-review.md
├── .state/                      # Greenfield state
├── .ddd_workspaces/             # Greenfield workspaces
├── docs/features/               # Greenfield feature docs
└── playbooks/                   # Deployment automation
```

## The Factory

Three phases transform idea → working app:

1. **Vision Synthesis** → `VISION.md` (features, scope)
2. **Technical Foundation** → `ARCHITECTURE.md`, `ROADMAP.md`
3. **Feature Implementation** → Working code via DDD loop

## Quick Start: Greenfield Mode

```
# Phase 1: Vision
Use vision-architect agent to produce VISION.md

# Phase 2: Architecture
Use tech-architect agent to produce ARCHITECTURE.md + ROADMAP.md

# Phase 3: Build (repeat for each feature)
/ddd/1  → Understand (create FEATURE_SPEC.md)
/ddd/2  → Document (create DOCS_DRAFT.md)
/ddd/3  → Code-Breakdown (create IMPLEMENTATION_PLAN.md)
/ddd/4  → Implement (write code, tests)
/ddd/5  → Review (finalize, complete)
```

## Quick Start: Enhancer Mode

Use this when enhancing an EXISTING app (not building from scratch).

```
# In the target repo you want to enhance:

# Step 1: Initialize beachhead
/enhancer/init              → Creates .enhancer/ directory

# Phase 0: Discovery
/enhancer/discovery         → Produces .enhancer/DISCOVERY.md

# Phase 1: Vision (same agents, output to .enhancer/)
Use vision-architect        → .enhancer/VISION.md

# Phase 2: Architecture
Use tech-architect          → .enhancer/ARCHITECTURE.md, ROADMAP.md

# Phase 3: Build (enhancement DDD)
/enhancer/ddd/1  → Understand (E-F1, E-F2... feature IDs)
/enhancer/ddd/2  → Document
/enhancer/ddd/3  → Code-Breakdown (includes integration planning)
/enhancer/ddd/4  → Implement (with regression testing)
/enhancer/ddd/5  → Review
```

### Enhancer Beachhead

When enhancer mode is initialized, everything lives in `.enhancer/`:

```
target-repo/
├── [their existing files]
├── .claude/commands/enhancer/  # Enhancement commands
└── .enhancer/                  # YOUR beachhead
    ├── DISCOVERY.md            # What exists (Phase 0)
    ├── VISION.md               # What to add (Phase 1)
    ├── ARCHITECTURE.md         # How to build (Phase 2)
    ├── ROADMAP.md              # Build order (Phase 2)
    ├── state/project.json      # Progress tracking
    ├── workspaces/             # DDD workspaces
    └── docs/features/          # Enhancement documentation
```

### Key Differences

| Aspect | Greenfield | Enhancer |
|--------|------------|----------|
| Phase 0 | None | Discovery (required) |
| Feature IDs | F1, F2 | E-F1, E-F2 |
| State | `.state/` | `.enhancer/state/` |
| Workspaces | `.ddd_workspaces/` | `.enhancer/workspaces/` |
| Focus | Build new | Integrate with existing |
| Testing | New tests | New + regression tests |

## Rules

See `.claude/rules/` for detailed constraints:
- **revenue.md** - MRR-first, monetization patterns, paywall strategies
- **architecture.md** - Full factory model, phases, document flow
- **development.md** - Agent delegation, zero-BS, regenerate don't patch
- **python.md** - Deterministic only, no LLM API calls
