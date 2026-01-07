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

**Process:** 6-step Document-Driven Design, one feature at a time.

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

### Phase 4: [TBD]
