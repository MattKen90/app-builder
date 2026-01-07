# App Builder Architecture

## First Principles

**Human = Operator.** Minimal involvement. Provides intent, approves direction.

**AI = Driver.** Full ownership of product vision, feature selection, research, and implementation.

**Spec-Driven Design (SDD).** Human specs what they want, AI expands and builds it.

## The Inversion

Traditional: Human designs, AI assists.

App Builder: **AI designs, human approves.**

The human's role is to say "yes" or "not quite" — not to architect.

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
┌─────────────────────────────────────────────────────────────────┐
│                        APP BUILDER FACTORY                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  [Human Idea] ──→ ┌───────────────┐ ──→ [VISION.md]             │
│                   │ Phase 1       │     (features, scope)        │
│                   │ Vision Synth  │                              │
│                   └───────────────┘                              │
│                          │                                       │
│                          ▼                                       │
│  [VISION.md] ────→ ┌───────────────┐ ──→ [ARCHITECTURE.md]      │
│                    │ Phase 2       │     (tech stack, design)    │
│                    │ Tech Found.   │ ──→ [ROADMAP.md]            │
│                    └───────────────┘     (build sequence)        │
│                          │                                       │
│                          ▼                                       │
│  [ROADMAP.md] ───→ ┌───────────────┐ ──→ [Feature Code]         │
│  [ARCH.md]         │ Phase 3       │     (working features)      │
│                    │ Build         │                              │
│                    └───────────────┘                              │
│                          │                                       │
│                          ▼                                       │
│                    [Working App]                                 │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Phases

### Phase 1: Vision Synthesis

**Agent:** `vision-architect`

**Input:** Human's rough idea, proposal document, or general concept.

**Process (Multi-Round, Interactive):**

1. **EXTRACT** (3 rounds of Q&A):
   - Round 1: Foundation (Problem & Users)
   - Round 2: Vision & Workflow (What Success Looks Like)
   - Round 3: Constraints & Priorities (Boundaries)
   - *Summarize after each round. Confirm understanding.*

2. **EXPAND** (Research → Discover → Propose):
   - Deep research: competitors, cutting-edge tech, user pain points
   - Synthesize discoveries into categories
   - **Present findings to human** — "Here's what I found. Which of these do you want?"
   - *Wait for human to approve/reject discoveries*

3. **SCOPE**: Define in/out boundaries for v1

4. **SYNTHESIZE**: Produce canonical document

**Output:** `VISION.md` — The bible of the app. What we're building, for whom, why, and what's in scope.

**Human role:** Answer questions across rounds, review research discoveries, approve the final VISION.md.

**AI role:** Drive multi-round extraction, research and present mind-expanding possibilities, produce the document.

**Completion Criteria:** VISION.md exists and is approved.

---

### Phase 2: Technical Foundation

**Agent:** `tech-architect`

**Input:** `VISION.md` (specifically the feature list and technical approach section)

**Process (Multi-Round, Interactive):**

1. **RESEARCH** (3 rounds):
   - Round 1: Requirements analysis + initial research on similar apps
   - Round 2: Technology options deep dive — **present options with trade-offs**
   - Round 3: Architecture validation — confirm stack before detailed design
   - *Wait for human confirmation at each round*

2. **ARCHITECT**: Design the system based on confirmed stack

3. **SEQUENCE**: Order the features into a buildable roadmap

**Output:**
- `ARCHITECTURE.md` — Tech stack, system design, database schema, API structure, deployment approach
- `ROADMAP.md` — Ordered feature build sequence with dependencies mapped

**Human role:** Review research findings, approve technology choices, flag constraints (existing infrastructure, team skills, etc.)

**AI role:** Research cutting-edge approaches, **present discoveries for approval**, design elegant architecture, sequence the build optimally.

**Completion Criteria:** ARCHITECTURE.md and ROADMAP.md exist and are approved.

**Key Principle:** Don't just pick "safe" technologies. Research what's actually best for THIS app. **Present cutting-edge discoveries** — let the human see what's possible and choose. The architecture should exceed what the human would have designed alone.

---

### Phase 3: Feature Implementation (DDD Loop)

**Process:** 5-step Document-Driven Design, one feature at a time.

**Document Flow:**
```
Step 1: Understand
  Read:  ROADMAP.md, ARCHITECTURE.md
  Write: .ddd_workspaces/{feature}/FEATURE_SPEC.md
         ↓
Step 2: Document
  Read:  FEATURE_SPEC.md
  Write: .ddd_workspaces/{feature}/DOCS_DRAFT.md
         ↓
Step 3: Code-Breakdown
  Read:  FEATURE_SPEC.md, DOCS_DRAFT.md
  Write: .ddd_workspaces/{feature}/IMPLEMENTATION_PLAN.md
         ↓
Step 4: Implement
  Read:  IMPLEMENTATION_PLAN.md + all specs
  Write: Code, Tests, .ddd_workspaces/{feature}/PROGRESS.md
         ↓
Step 5: Review
  Read:  All workspace artifacts
  Write: docs/features/{feature-id}-{feature-name}.md
```

All workspace files live in `.ddd_workspaces/{feature-id}-{feature-name}/`. Each step knows where to read and write.

**Input:**
- `ROADMAP.md` (which feature to build next)
- `ARCHITECTURE.md` (how to build it)

**The Loop:**
```
For each feature in ROADMAP.md:
    /ddd:1 → Step 1
    /ddd:2 → Step 2
    /ddd:3 → Step 3
    /ddd:4 → Step 4
    /ddd:5 → Step 5
    /ddd:6 → Step 6
    → Feature complete, move to next
```

**Output:** Working, tested feature code + feature documentation.

**Feature Sizing:** Each feature ~1 hour through full DDD cycle. Right-sized = independently deployable, visible user value, 1-2 hours implementation.

**Completion Criteria:** All features from ROADMAP.md implemented and working.

---

## Feature Documentation

One doc per feature. No subfolders. No sprawl.

```
docs/features/
├── F1-user-authentication.md
├── F2-dashboard.md
├── F3-data-export.md
└── ...
```

**Created during:** DDD Step 5 (Review) — after code is done and tested.

**Naming:** `{feature-id}-{feature-name}.md`

**Rule:** If a feature needs multiple docs, the feature is too big. Go back and split it.

---

## Deployment Patterns (Build as You Go)

Different app types require different deployment and testing:

| App Type | CLI Tools to Research |
|----------|----------------------|
| iOS | fastlane, xcrun, altool, Transporter CLI |
| Android | gradle, bundletool, adb, fastlane |
| Web App | vercel-cli, netlify-cli, aws-cli, fly-cli |
| Landing Page | gh-pages, surge, firebase-cli |
| API/Backend | docker, kubectl, flyctl, railway-cli |

**Philosophy: Automate, Don't Document**

The AI executes deployment via CLI tools and bash commands. Playbooks contain **executable scripts**, not instructions.

**Priority Order:**
1. **CLI tools first** - Research what's available for Linux/Arch
2. **Bash automation** - Script the entire deployment process
3. **AI executes** - Run the deployment, don't tell human to do it
4. **Document only what can't be automated** - Store credentials, one-time setup

**Strategy: Learn Once, Automate Forever**

1. **First app of a type**: Research CLI tools, build automation scripts, deploy
2. **Capture the automation**: Store scripts in `playbooks/{app-type}/`
3. **Future apps**: Run the scripts, refine automation

```
playbooks/
├── ios/
│   ├── deploy.sh           # Automated deployment script
│   ├── test.sh             # Automated testing script
│   ├── setup-once.md       # One-time setup (credentials, certs)
│   └── troubleshooting.md  # When automation fails
├── android/
├── web-app/
└── landing-page/
```

**In ROADMAP.md**: Include deployment as a feature (e.g., "F-DEPLOY: Deploy to App Store").
- First time = research CLI tools, build scripts, execute deployment
- Future = run existing scripts

**Research First**: Before any deployment, search for CLI tools packaged for Arch Linux or available via AUR. Prefer tools that run natively on Linux over those requiring macOS.

The factory gets smarter and more automated with each app type you ship.
