# App Builder

Build profitable apps with AI. You provide the idea, AI does the rest.

---

## What Is This?

App Builder is a framework that flips the traditional development process:

- **Traditional:** You design everything, AI helps write code
- **App Builder:** AI designs everything, you just approve

You bring a rough idea. AI researches, designs, architects, and builds a complete application — with payments built in from day one.

---

## The Philosophy

**MRR is King.** Every app exists to generate Monthly Recurring Revenue. Payment infrastructure isn't an afterthought — it's built into Phase 1.

**You're the Operator.** Your job is to say "yes" or "not quite." You don't need to know how to code. You don't need to architect. You approve direction.

**AI is the Driver.** AI handles research, design, technical decisions, and implementation. It asks smart questions, proposes solutions, and builds working software.

---

## Quick Start

### Building a New App (Greenfield)

```
/set-state mode greenfield
/phases/1    → AI interviews you, creates vision
/phases/2    → AI designs architecture, creates roadmap
/phases/3    → AI builds features one by one
```

### Enhancing an Existing App (Enhancer)

```
/set-state mode enhancer
/set-state target /path/to/your/existing/app
/phases/0    → AI analyzes your existing codebase
/phases/1    → AI proposes enhancements
/phases/2    → AI designs within your existing patterns
/phases/3    → AI builds enhancements
```

---

## The Four Phases

### Phase 0: Discovery (Enhancer Only)

AI analyzes your existing app to understand:
- What technologies you're using
- How your code is structured
- What patterns to follow
- Where monetization gaps exist

**Output:** `.enhancer/DISCOVERY.md` — a complete map of your codebase

---

### Phase 1: Vision

AI interviews you in 3 rounds:
1. **Problem & Users** — What problem are you solving? For whom?
2. **Vision & Monetization** — What does the app do? Who pays?
3. **Constraints & Priorities** — What are the boundaries?

Then AI researches competitors, finds opportunities, and proposes features with pricing tiers.

**Output:** `VISION.md` — complete product vision with monetization strategy

---

### Phase 2: Technical Foundation

AI takes your vision and designs:
- Technology choices (with justification)
- System architecture
- Database design
- Payment infrastructure (Stripe)
- Build sequence

**Output:** `ARCHITECTURE.md` + `ROADMAP.md`

---

### Phase 3: Build

AI builds each feature using a 5-step DDD cycle:

| Step | Command | What Happens |
|------|---------|--------------|
| 1. Understand | `/ddd/1` | AI presents spec, you refine together until approved |
| 2. Document | `/ddd/2` | AI writes user docs before building |
| 3. Plan | `/ddd/3` | AI breaks feature into buildable phases |
| 4. Implement | `/ddd/4` | AI writes code, tests at each checkpoint |
| 5. Review | `/ddd/5` | AI verifies everything works, finalizes docs |

**Step 1 includes a refinement loop** — AI presents the feature spec, asks clarifying questions, and loops with you until you explicitly approve. No building happens until you're satisfied.

Repeat for each feature until your app is complete.

---

## Commands Reference

### Core Commands

| Command | What It Does |
|---------|--------------|
| `/set-state mode greenfield` | Start a new app from scratch |
| `/set-state mode enhancer` | Enhance an existing app |
| `/set-state target /path` | Point to existing app (enhancer mode) |
| `/set-state` | View current project state |

### Phase Commands

| Command | What It Does |
|---------|--------------|
| `/phases/0` | Discover existing codebase (enhancer only) |
| `/phases/1` | Create product vision |
| `/phases/2` | Design architecture and roadmap |
| `/phases/3` | Build features (starts DDD cycle) |

### DDD Commands (Direct Access)

| Command | What It Does |
|---------|--------------|
| `/ddd/1` | Understand & approve feature spec |
| `/ddd/2` | Create documentation draft |
| `/ddd/3` | Break down implementation plan |
| `/ddd/4` | Implement the feature |
| `/ddd/5` | Review and finalize |

### Utility Commands

| Command | What It Does |
|---------|--------------|
| `/update-docs` | Sync VISION, ARCHITECTURE, ROADMAP with reality |
| `/create-new-feature` | Add a new feature (mini Phase 1+2 cycle) |

---

## Project Structure

When you build with App Builder, here's what gets created:

```
your-project/
├── .state.json          ← Current state (auto-loaded on context start)
├── VISION.md            ← What you're building
├── ARCHITECTURE.md      ← How it's designed
├── ROADMAP.md           ← Build sequence
│
├── app/                 ← Your app's code lives here
│   ├── src/
│   ├── public/
│   └── ...
│
├── docs/features/       ← Documentation for each feature
├── .ddd_workspaces/     ← Working files during build (archived after)
│
└── .claude/             ← App Builder's brain
    ├── commands/        ← Slash commands
    ├── rules/           ← Behavior rules
    └── skills/          ← Specialized capabilities
```

### Enhancer Mode Structure

Enhancement work is isolated in `.enhancer/`:

```
your-project/
├── .enhancer/
│   ├── DISCOVERY.md     ← Analysis of existing codebase
│   ├── VISION.md        ← Enhancement specs
│   ├── ARCHITECTURE.md  ← How enhancements fit
│   ├── ROADMAP.md       ← Enhancement sequence
│   └── workspaces/      ← DDD working files
```

---

## State & Context Resume

App Builder tracks progress in `.state.json`. If your session ends mid-build, a fresh context automatically loads state and knows:

- Which mode you're in (greenfield/enhancer)
- Which feature you're building
- Which DDD step you're on
- What you were last working on

Just pick up where you left off.

---

## What You'll Need

1. **Claude Code** — The AI assistant that runs App Builder
2. **An idea** — Even a rough one works
3. **Approval energy** — AI proposes, you approve or redirect

That's it. No coding required.

---

## Tips for Success

**Be honest in interviews.** The more AI understands your vision, the better it builds.

**Trust the process.** AI will ask questions that seem basic. Answer them anyway.

**Refine before approving.** In DDD Step 1, take time to adjust the spec. It's easier to change words than code.

**Approve in stages.** Don't try to perfect everything upfront. Approve phase by phase.

**MRR first.** When AI asks about monetization, have an answer. Free apps don't pay bills.

**Stay in your lane.** You're the operator. Let AI drive the technical decisions.

---

## FAQ

**Do I need to know how to code?**
No. AI handles all technical implementation.

**What if I don't like what AI proposes?**
Say "not quite" and explain what's off. AI will adjust. In DDD Step 1, there's a dedicated refinement loop for this.

**Can I enhance an app I didn't build?**
Yes. Enhancer mode analyzes any codebase and proposes improvements.

**What payment provider does this use?**
Stripe. It's the default for all monetization.

**How long does it take to build an app?**
Depends on complexity. Each feature takes roughly 1 hour through the DDD cycle.

**What if my context/session ends mid-build?**
State is saved in `.state.json` and auto-loaded on next session. You'll resume right where you left off.

---

## Getting Help

Stuck? Just ask. AI is designed to guide you through each phase.

If something's broken, check:
1. Is your mode set? (`/set-state`)
2. Is your target set? (enhancer mode)
3. Are you in the right phase?

---

**Ready to build?**

```
/set-state mode greenfield
/phases/1
```

Let's make something that makes money.
