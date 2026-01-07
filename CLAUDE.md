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

### Step 1: Set Mode

```
/mode greenfield    # Building a new app
/mode enhancer      # Enhancing an existing app
```

### Step 2: Initialize

```
/init               # Sets up structure based on mode
```

### Step 3: Build

**Greenfield:**
```
Phase 1: vision-architect  → VISION.md
Phase 2: tech-architect    → ARCHITECTURE.md, ROADMAP.md
Phase 3: /ddd/1 through /ddd/5 (repeat for each feature)
```

**Enhancer:**
```
Phase 0: /discovery        → .enhancer/DISCOVERY.md
Phase 1: vision-architect  → .enhancer/VISION.md
Phase 2: tech-architect    → .enhancer/ARCHITECTURE.md, ROADMAP.md
Phase 3: /ddd/1 through /ddd/5 (repeat for each enhancement)
```

## Command Reference

| Command | Purpose |
|---------|---------|
| `/mode` | Set or show current mode |
| `/init` | Initialize project structure |
| `/discovery` | Phase 0: Analyze existing codebase (enhancer only) |
| `/ddd/1` | DDD Step 1: Understand |
| `/ddd/2` | DDD Step 2: Document |
| `/ddd/3` | DDD Step 3: Code-Breakdown |
| `/ddd/4` | DDD Step 4: Implement |
| `/ddd/5` | DDD Step 5: Review |

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
