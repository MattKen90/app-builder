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

**Output:** `DISCOVERY.md` — a complete map of your codebase

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

AI builds each feature using a 5-step cycle:

1. **Understand** — AI creates detailed spec, you approve
2. **Document** — AI writes user docs before building
3. **Plan** — AI breaks feature into buildable phases
4. **Implement** — AI writes code, tests at each step
5. **Review** — AI verifies everything works, finalizes docs

Repeat for each feature until your app is complete.

---

## Commands Reference

| Command | What It Does |
|---------|--------------|
| `/set-state mode greenfield` | Start a new app from scratch |
| `/set-state mode enhancer` | Enhance an existing app |
| `/set-state target /path` | Point to existing app (enhancer mode) |
| `/phases/0` | Discover existing codebase (enhancer only) |
| `/phases/1` | Create product vision |
| `/phases/2` | Design architecture and roadmap |
| `/phases/3` | Build features |
| `/set-state` | View current project state |

---

## Project Structure

When you build with App Builder, here's what gets created:

```
your-project/
├── VISION.md           ← What you're building
├── ARCHITECTURE.md     ← How it's designed
├── ROADMAP.md          ← Build sequence
│
├── app/                ← Your app's code lives here
│   ├── src/
│   ├── public/
│   └── ...
│
├── docs/features/      ← Documentation for each feature
│
└── .claude/            ← App Builder's brain (don't touch)
```

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

**Approve in stages.** Don't try to perfect everything upfront. Approve phase by phase.

**MRR first.** When AI asks about monetization, have an answer. Free apps don't pay bills.

**Stay in your lane.** You're the operator. Let AI drive the technical decisions.

---

## FAQ

**Do I need to know how to code?**
No. AI handles all technical implementation.

**What if I don't like what AI proposes?**
Say "not quite" and explain what's off. AI will adjust.

**Can I enhance an app I didn't build?**
Yes. Enhancer mode analyzes any codebase and proposes improvements.

**What payment provider does this use?**
Stripe. It's the default for all monetization.

**How long does it take to build an app?**
Depends on complexity. Each feature takes roughly 1 hour through the build cycle.

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
