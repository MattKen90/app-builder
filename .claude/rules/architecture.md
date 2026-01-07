# App Builder Architecture

## First Principles

**MRR is King.** Everything exists to generate Monthly Recurring Revenue.

**Human = Operator.** Minimal involvement. Provides intent, approves direction.

**AI = Driver.** Full ownership of product vision, feature selection, research, and implementation.

**Spec-Driven Design (SDD).** Human specs what they want, AI expands and builds it.

## The Inversion

Traditional: Human designs, AI assists.

App Builder: **AI designs, human approves.**

The human's role is to say "yes" or "not quite" — not to architect.

---

## Two Modes

**Greenfield Mode:** Build new apps from scratch.

**Enhancer Mode:** Enhance existing apps with a segregated beachhead.

All commands read `.state.json` and adapt behavior accordingly.

---

## Project Structure

Clear separation between App Builder infrastructure and the app being built.

```
project-root/
├── .claude/
│   ├── commands/
│   │   ├── phases/             # Builder commands (root = builder)
│   │   ├── ddd/
│   │   ├── init.md
│   │   ├── set-state.md
│   │   └── app/                # App commands (/app/...)
│   ├── skills/
│   │   ├── claude-code-builder/  # Builder skills
│   │   └── app/                # App skills
│   └── rules/
│       ├── architecture.md     # Builder rules
│       ├── revenue.md
│       ├── development.md
│       └── app/                # App rules
│
├── .state.json                 # Builder state
├── .ddd_workspaces/            # DDD working directories
├── CLAUDE.md                   # Builder operations
│
├── VISION.md                   # Phase 1 output (root, prominent)
├── ARCHITECTURE.md             # Phase 2 output (root, prominent)
├── ROADMAP.md                  # Phase 2 output (root, prominent)
│
├── docs/features/              # Feature docs (DDD Step 5)
│
└── app/                        # THE APP BEING BUILT
    ├── src/
    ├── public/
    ├── package.json
    └── ...
```

**Key Rules:**
- All app code goes in `app/`
- App primitives go in `.claude/{commands,skills,rules}/app/`
- Builder primitives stay at root level (no nesting)

---

## State Management

**Single source of truth:** `.state.json` at project root.

```json
{
  "mode": "greenfield",
  "app": {
    "name": "MyApp",
    "initialized": "2024-01-15T10:00:00Z",
    "phase": 2
  },
  "features": {
    "F1": { "name": "User Auth", "status": "complete" },
    "F2": { "name": "Dashboard", "status": "in_progress" }
  },
  "ddd": {
    "feature": "F2",
    "step": 3,
    "workspace": ".ddd_workspaces/F2-dashboard/"
  }
}
```

On context load/reload, Claude reads this file and instantly knows:
- Current mode and phase
- All features and their status
- Current DDD position

---

## Document-Driven Design (DDD)

Agents are ephemeral. 200k context window, then compaction or restart. Work cannot live only in context.

**The Rule:** Every phase produces a canonical document. No exceptions.

```
Phase Input → Agent Work → Document Output
```

Documents are the persistent artifacts. Agents are temporary workers that read inputs and write outputs. When an agent's context expires, the document remains.

**Why This Matters:**
- No work is lost to context compaction
- Any agent can pick up where another left off
- Human can review/approve discrete outputs
- Factory model: discrete inputs → discrete outputs

---

## The Factory

Each phase is a machine in the factory. Input → Process → Output.

```
┌─────────────────────────────────────────────────────────────────────┐
│                        APP BUILDER FACTORY                          │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │ ENHANCER MODE ONLY                                          │   │
│  │                                                             │   │
│  │ [Existing Code] ──→ ┌───────────────┐ ──→ [DISCOVERY.md]   │   │
│  │                     │ Phase 0       │     (what exists)     │   │
│  │                     │ Discovery     │                       │   │
│  │                     └───────────────┘                       │   │
│  └─────────────────────────────────────────────────────────────┘   │
│                          │                                          │
│                          ▼                                          │
│  [Human Idea] ──→ ┌───────────────┐ ──→ [VISION.md]                │
│  (or DISCOVERY)   │ Phase 1       │     (features, scope,          │
│                   │ Vision        │      monetization)              │
│                   └───────────────┘                                 │
│                          │                                          │
│                          ▼                                          │
│  [VISION.md] ────→ ┌───────────────┐ ──→ [ARCHITECTURE.md]         │
│                    │ Phase 2       │     (tech stack, design)       │
│                    │ Technical     │ ──→ [ROADMAP.md]               │
│                    │ Foundation    │     (build sequence)           │
│                    └───────────────┘                                │
│                          │                                          │
│                          ▼                                          │
│  [ROADMAP.md] ───→ ┌───────────────┐ ──→ [Feature Code]            │
│  [ARCH.md]         │ Phase 3       │     (working features)         │
│                    │ Build (DDD)   │                                │
│                    └───────────────┘                                │
│                          │                                          │
│                          ▼                                          │
│                    [Working App]                                    │
│                    [Making Money]                                   │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Phases

### Phase 0: Discovery (Enhancer Mode Only)

**Command:** `/phases/0`

**Agent:** `discovery-architect`

**Input:** Existing codebase to enhance.

**Process:**
1. **SCAN**: Automated analysis of tech stack, structure, Claude Code setup
2. **ANALYZE**: Deep dive on data model, API surface, monetization status
3. **SYNTHESIZE**: Produce discovery document

**Output:** `.enhancer/DISCOVERY.md` — Complete map of existing codebase.

**Human role:** Confirm findings, clarify any ambiguities.

**AI role:** Thoroughly analyze the codebase, document patterns to follow, identify enhancement opportunities.

**Completion Criteria:** DISCOVERY.md exists with tech stack, patterns, and monetization assessment.

---

### Phase 1: Vision Synthesis

**Command:** `/phases/1`

**Agent:** `vision-architect`

**Input:**
- Greenfield: Human's rough idea
- Enhancer: DISCOVERY.md + enhancement goals

**Process (Multi-Round, Interactive):**

1. **EXTRACT** (3 rounds of Q&A):
   - Round 1: Foundation (Problem & Users)
   - Round 2: Vision & Workflow & Monetization
   - Round 3: Constraints & Priorities
   - *Summarize after each round. Confirm understanding.*

2. **EXPAND** (Research → Discover → Propose):
   - Deep research: competitors, cutting-edge tech, pricing models
   - **Present findings to human** — including monetization recommendations
   - *Wait for human to approve/reject discoveries*

3. **SCOPE**: Define in/out boundaries for v1, assign feature tiers (Free/Paid/Enterprise)

4. **SYNTHESIZE**: Produce canonical document with monetization section

**Output:**
- Greenfield: `VISION.md`
- Enhancer: `.enhancer/VISION.md`

**Human role:** Answer questions, review research, approve vision and pricing.

**AI role:** Drive extraction, research possibilities, produce document with clear monetization strategy.

**Completion Criteria:** VISION.md exists with features AND monetization section approved.

---

### Phase 2: Technical Foundation

**Command:** `/phases/2`

**Agent:** `tech-architect`

**Input:** VISION.md (features, scope, monetization model)

**Process (Multi-Round, Interactive):**

1. **RESEARCH** (3 rounds):
   - Round 1: Requirements analysis + similar app research
   - Round 2: Technology options with trade-offs + Stripe integration patterns
   - Round 3: Architecture validation
   - *Wait for human confirmation at each round*

2. **ARCHITECT**: Design system including payments infrastructure

3. **SEQUENCE**: Order features with F-PAY (billing) in Phase 1

**Output:**
- `ARCHITECTURE.md` — Tech stack, system design, payments architecture
- `ROADMAP.md` — Build sequence with billing in first phase

**Human role:** Review findings, approve technology choices.

**AI role:** Research approaches, design architecture, ensure payments infrastructure is foundational.

**Completion Criteria:** ARCHITECTURE.md and ROADMAP.md exist with payments architecture defined.

**Key Principle:** Payments infrastructure (Stripe) goes in Phase 1 of the roadmap. MRR is King.

---

### Phase 3: Feature Implementation (DDD Loop)

**Command:** `/phases/3` (orchestrator) or `/ddd/1` through `/ddd/5` (direct)

**Process:** 5-step Document-Driven Design, one feature at a time.

**Document Flow:**
```
Step 1: Understand (/ddd/1)
  Read:  ROADMAP.md, ARCHITECTURE.md, .state.json
  Write: {workspace}/FEATURE_SPEC.md
         ↓
Step 2: Document (/ddd/2)
  Read:  FEATURE_SPEC.md
  Write: {workspace}/DOCS_DRAFT.md
         ↓
Step 3: Code-Breakdown (/ddd/3)
  Read:  FEATURE_SPEC.md, DOCS_DRAFT.md
  Write: {workspace}/IMPLEMENTATION_PLAN.md
         ↓
Step 4: Implement (/ddd/4)
  Read:  IMPLEMENTATION_PLAN.md + all specs
  Write: Code, Tests, {workspace}/PROGRESS.md
         ↓
Step 5: Review (/ddd/5)
  Read:  All workspace artifacts
  Write: docs/features/{feature-id}-{feature-name}.md
  Update: .state.json (feature complete)
```

**Workspaces:**
- Greenfield: `.ddd_workspaces/{feature-id}-{feature-name}/`
- Enhancer: `.enhancer/workspaces/{feature-id}-{feature-name}/`

**The Loop:**
```
For each feature in ROADMAP.md:
    /ddd/1 → Understand & approve spec
    /ddd/2 → Document before building
    /ddd/3 → Break into phases
    /ddd/4 → Build phase by phase
    /ddd/5 → Review & complete
    → Update .state.json, move to next feature
```

**Feature Sizing:** Each feature ~1 hour through full DDD cycle.

**Enhancer Mode:** Includes regression testing before/after each implementation phase.

---

## Path Reference

| Resource | Greenfield | Enhancer |
|----------|------------|----------|
| State | `.state.json` | `.state.json` |
| Discovery | N/A | `.enhancer/DISCOVERY.md` |
| Vision | `VISION.md` | `.enhancer/VISION.md` |
| Architecture | `ARCHITECTURE.md` | `.enhancer/ARCHITECTURE.md` |
| Roadmap | `ROADMAP.md` | `.enhancer/ROADMAP.md` |
| Workspaces | `.ddd_workspaces/` | `.enhancer/workspaces/` |
| Feature docs | `docs/features/` | `.enhancer/docs/features/` |
| App code | `app/` | (existing codebase) |
| Feature IDs | F1, F2, F3 | E-F1, E-F2, E-F3 |

---

## Feature Documentation

One doc per feature. No subfolders. No sprawl.

```
docs/features/
├── F1-user-authentication.md
├── F-PAY-billing-infrastructure.md
├── F2-dashboard.md
└── ...
```

**Created during:** DDD Step 5 (Review) — after code is done and tested.

**Naming:** `{feature-id}-{feature-name}.md`

**Rule:** If a feature needs multiple docs, the feature is too big. Split it.

---

## Deployment Patterns

Different app types require different deployment:

| App Type | CLI Tools |
|----------|-----------|
| iOS | fastlane, xcrun, altool |
| Android | gradle, bundletool, fastlane |
| Web App | vercel-cli, netlify-cli, fly-cli |
| Landing Page | gh-pages, surge, firebase-cli |
| API/Backend | docker, kubectl, flyctl |

**Philosophy: Automate, Don't Document**

```
playbooks/
├── ios/
│   ├── deploy.sh
│   └── setup-once.md
├── android/
├── web-app/
└── landing-page/
```

**In ROADMAP.md**: Include deployment as a feature (e.g., "F-DEPLOY: Deploy to Production").

---

## Command Quick Reference

| Command | Purpose |
|---------|---------|
| `/set-state mode <mode>` | Set greenfield or enhancer |
| `/init` | Initialize project structure |
| `/phases/0` | Discovery (enhancer only) |
| `/phases/1` | Vision |
| `/phases/2` | Technical Foundation |
| `/phases/3` | Build (DDD orchestrator) |
| `/ddd/1` - `/ddd/5` | DDD steps (direct access) |
