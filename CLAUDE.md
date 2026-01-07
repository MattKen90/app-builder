# App Builder

Lightweight, Claude Code-first framework for building and enhancing monetizable applications. Zero API costs—subscription only.

## Two Modes

**Greenfield Mode**: Build new apps from scratch.

**Enhancer Mode**: Enhance existing apps with a segregated beachhead.

All commands are mode-aware—set the mode once, and everything adapts.

## Prime Directive

**MRR is King.** Everything we build exists to generate Monthly Recurring Revenue. Not apps for apps' sake. Not beautiful code for beauty's sake. Revenue.

## Philosophy

**Revenue-First Development.** Every decision—from vision to deployment—asks: "How does this make money?" Monetization isn't an afterthought; it's the foundation.

**MVP, Fully Monetizable.** Ship fast, iterate fast. Not over-engineered perfection—functional products with clear paths to payment. Stripe-ready from day one.

**Human = Operator.** Minimal involvement. Provides intent, approves direction.

**AI = Driver.** Full ownership of product vision, feature selection, research, and implementation. Always considering revenue implications.

## Project Structure

```
app-builder/
├── CLAUDE.md                    # This file
├── .mode                        # Current mode (greenfield/enhancer)
├── .claude/
│   ├── rules/                   # Shared rules (both modes)
│   │   ├── revenue.md
│   │   ├── architecture.md
│   │   ├── development.md
│   │   └── python.md
│   ├── agents/                  # Shared agents
│   │   ├── vision-architect.md  # Phase 1
│   │   ├── tech-architect.md    # Phase 2
│   │   └── discovery-architect.md # Phase 0 (enhancer only)
│   └── commands/                # Smart commands (mode-aware)
│       ├── mode.md              # /mode - set greenfield or enhancer
│       ├── init.md              # /init - initialize based on mode
│       ├── discovery.md         # /discovery - Phase 0 (enhancer only)
│       ├── phases/              # Guided phase walkthroughs
│       │   ├── 0.md             # /phases/0 - Discovery (enhancer only)
│       │   ├── 1.md             # /phases/1 - Vision
│       │   ├── 2.md             # /phases/2 - Technical Foundation
│       │   └── 3.md             # /phases/3 - Build (DDD cycle)
│       └── ddd/                 # Single DDD set (adapts to mode)
│           ├── 1-understand.md
│           ├── 2-document.md
│           ├── 3-code-breakdown.md
│           ├── 4-implement.md
│           └── 5-review.md
├── .state/                      # Greenfield state
├── .ddd_workspaces/             # Greenfield workspaces
├── docs/features/               # Greenfield feature docs
└── playbooks/                   # Deployment automation
```

## Quick Start

### Option A: Guided Walkthrough (Recommended)

Just run the phases in order:

```
/mode greenfield    # or /mode enhancer
/init
/phases/0           # Enhancer only - Discovery
/phases/1           # Vision
/phases/2           # Technical Foundation
/phases/3           # Build (DDD cycle)
```

Each phase command invokes the right agent and guides you through.

### Option B: Direct Commands

For experienced users:

```
/mode greenfield    # Set mode
/init               # Initialize structure
```

Then invoke agents directly or run DDD commands.

### What Each Phase Does

| Phase | Greenfield | Enhancer |
|-------|------------|----------|
| 0 | Skipped | Analyze existing codebase → DISCOVERY.md |
| 1 | Define vision → VISION.md | Define enhancements → VISION.md |
| 2 | Design architecture → ARCHITECTURE.md, ROADMAP.md | Design integration → same |
| 3 | Build features via DDD | Build enhancements via DDD |

## Command Reference

### Setup Commands

| Command | Purpose |
|---------|---------|
| `/mode` | Set or show current mode (greenfield/enhancer) |
| `/init` | Initialize project structure based on mode |

### Phase Commands (Guided Walkthrough)

| Command | Purpose |
|---------|---------|
| `/phases/0` | Discovery - Analyze existing codebase (enhancer only) |
| `/phases/1` | Vision - Define what to build |
| `/phases/2` | Technical Foundation - Design architecture |
| `/phases/3` | Build - Start/resume DDD cycle |

### DDD Commands (Direct Access)

| Command | Purpose |
|---------|---------|
| `/ddd/1` | DDD Step 1: Understand & approve spec |
| `/ddd/2` | DDD Step 2: Document before building |
| `/ddd/3` | DDD Step 3: Break into implementation phases |
| `/ddd/4` | DDD Step 4: Build phase by phase |
| `/ddd/5` | DDD Step 5: Review & complete |

### Legacy Commands

| Command | Purpose |
|---------|---------|
| `/discovery` | Same as `/phases/0` (enhancer only) |

## Mode Differences

| Aspect | Greenfield | Enhancer |
|--------|------------|----------|
| Phase 0 | Skipped | Required (/discovery) |
| Feature IDs | F1, F2, F3 | E-F1, E-F2, E-F3 |
| State | `.state/` | `.enhancer/state/` |
| Workspaces | `.ddd_workspaces/` | `.enhancer/workspaces/` |
| Vision | `VISION.md` | `.enhancer/VISION.md` |
| Testing | New tests | New + regression tests |

## Enhancer Beachhead

When in enhancer mode, all your work lives in `.enhancer/`:

```
target-repo/
├── [their existing files]       # Untouched
├── .mode                        # "enhancer"
└── .enhancer/                   # Your beachhead
    ├── DISCOVERY.md             # Phase 0 output
    ├── VISION.md                # Phase 1 output
    ├── ARCHITECTURE.md          # Phase 2 output
    ├── ROADMAP.md               # Phase 2 output
    ├── state/project.json
    ├── workspaces/
    └── docs/features/
```

## Rules

See `.claude/rules/` for detailed constraints:
- **revenue.md** - MRR-first, monetization patterns, paywall strategies
- **architecture.md** - Full factory model, phases, document flow
- **development.md** - Agent delegation, zero-BS, regenerate don't patch
- **python.md** - Deterministic only, no LLM API calls
