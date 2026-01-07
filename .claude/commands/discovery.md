---
description: Phase 0 - Discover and analyze the existing codebase before enhancement (enhancer mode only)
---

# Discovery (Phase 0)

**Mission**: Analyze the existing codebase to understand what exists. Produce DISCOVERY.md as the foundation for all enhancement work.

**Mode**: Enhancer only. This command is not used in greenfield mode.

**Prerequisites**:
- Mode set to `enhancer` (check `.state.json`)
- `/init` has been run
- `.enhancer/` beachhead exists

**Input**:
- The existing codebase
- Any existing CLAUDE.md, .claude/ setup

**Output**:
- `.enhancer/DISCOVERY.md`
- Updated `.enhancer/state/project.json`

---

## Process

### Step 0: Check Mode

Read `.state.json` file:

```
🔍 Checking mode...
```

**If mode is greenfield or not set:**
```
⚠️ Discovery Not Available

Discovery (Phase 0) is only for enhancer mode.
Current mode: {greenfield|not set}

Discovery analyzes EXISTING codebases before enhancement.
For greenfield projects, skip to Phase 1 (Vision).

To switch to enhancer mode: /set-state mode enhancer
```

### Step 1: Verify Prerequisites

Check that enhancer is initialized:

```
🔍 Checking enhancer setup...

Mode: enhancer ✓
- .enhancer/ exists: {Yes/No}
- state/project.json exists: {Yes/No}
- Current phase: {phase}
```

**If not initialized:**
```
⚠️ Enhancer Not Initialized

Run /init first to set up the beachhead.
```

**If discovery already complete:**
```
ℹ️ Discovery Already Complete

DISCOVERY.md exists at .enhancer/DISCOVERY.md
Created: {timestamp}

Options:
1. View existing discovery → Show summary
2. Re-run discovery → Overwrite existing
3. Continue to Phase 1 → Run /enhancer/vision

Which option?
```

### Step 2: SCAN - Automated Analysis

Systematically scan the codebase:

#### 2A: Project Configuration
```
📡 Scanning project configuration...

Looking for:
- package.json / requirements.txt / Cargo.toml / go.mod / etc.
- Configuration files (.env.example, config/, etc.)
- Build files (webpack, vite, tsconfig, etc.)
```

Read and analyze dependency files to identify:
- Primary language(s)
- Framework(s)
- Key dependencies
- Dev dependencies

#### 2B: Directory Structure
```
📁 Mapping directory structure...

[Show key directories and their apparent purposes]
```

Use Glob and directory listing to understand:
- Source code location (src/, lib/, app/, etc.)
- Test location
- Configuration location
- Documentation location

#### 2C: Claude Code Setup
```
🤖 Checking existing Claude Code setup...

CLAUDE.md: {Exists/Missing}
.claude/commands/: {List or "None"}
.claude/rules/: {List or "None"}
.claude/agents/: {List or "None"}
```

Read existing CLAUDE.md if present - understand project context.

#### 2D: Present Scan Results
```
📊 SCAN COMPLETE

## Tech Stack Detected
| Layer | Technology | Confidence |
|-------|------------|------------|
| Language | {X} | High/Medium/Low |
| Framework | {X} | High/Medium/Low |
| Database | {X} | High/Medium/Low |
| Auth | {X} | High/Medium/Low |
| Payments | {X} | High/Medium/Low |

## Project Structure
{Key directories and purposes}

## Claude Code Setup
{Summary of existing setup}

Proceeding to deep analysis...
```

### Step 3: ANALYZE - Deep Understanding

#### 3A: Data Model Analysis
```
🔍 Analyzing data model...
```

Look for:
- ORM models (Prisma, SQLAlchemy, ActiveRecord, etc.)
- Database migrations
- Schema files
- Type definitions

#### 3B: API Surface Analysis
```
🔍 Analyzing API surface...
```

Look for:
- Route definitions
- API handlers
- GraphQL schemas
- OpenAPI/Swagger specs

#### 3C: Authentication Analysis
```
🔍 Analyzing authentication...
```

Look for:
- Auth middleware
- Session management
- JWT handling
- OAuth integration

#### 3D: Monetization Analysis (MRR Lens)
```
💰 Analyzing monetization infrastructure...
```

Look for:
- Stripe integration (stripe in dependencies, webhook handlers)
- Subscription management
- Pricing/tier logic
- Feature gating
- Payment-related routes

**Present monetization assessment:**
```
💰 MONETIZATION ASSESSMENT

Current State: {None / Partial / Complete}

Checklist:
- [ ] Payment provider integration (Stripe, etc.)
- [ ] Subscription management
- [ ] Customer portal
- [ ] Webhook handling
- [ ] Feature gating by tier
- [ ] Pricing page
- [ ] Upgrade prompts

{If gaps found}:
Revenue Opportunities:
- {Gap}: {Why it matters for MRR}
```

#### 3E: Code Patterns Analysis
```
🔍 Analyzing code patterns...
```

Identify:
- Component/module structure
- Naming conventions
- Error handling patterns
- Testing approach
- State management (if frontend)

### Step 4: SYNTHESIZE - Write DISCOVERY.md

Compile all findings into `.enhancer/DISCOVERY.md`:

```
📝 Writing DISCOVERY.md...
```

Use the template from discovery-architect agent to create comprehensive document.

### Step 5: Present Summary

```
✅ Discovery Complete (Phase 0)

## Summary
- **App**: {name/description}
- **Tech Stack**: {primary technologies}
- **MRR Status**: {None/Partial/Complete}

## Key Findings
- {Finding 1}
- {Finding 2}
- {Finding 3}

## Enhancement Opportunities
1. {Opportunity}: {Impact}
2. {Opportunity}: {Impact}
3. {Opportunity}: {Impact}

## Output
- .enhancer/DISCOVERY.md (full analysis)

## Next Steps
Ready for Phase 1: Define what enhancements to build

Run: /enhancer/vision
```

### Step 6: Update State

Update `.enhancer/state/project.json`:

```json
{
  "enhancer": {
    "phase": "1"
  },
  "discovery": {
    "status": "complete",
    "completed": "{timestamp}",
    "tech_stack": {
      "language": "{X}",
      "framework": "{X}",
      "database": "{X}"
    },
    "monetization_status": "{none/partial/complete}"
  }
}
```

---

## Discovery Focus Areas

### Must Discover
- [ ] Tech stack (language, framework, database)
- [ ] Project structure
- [ ] Existing Claude Code setup
- [ ] Data model
- [ ] API surface
- [ ] Authentication approach
- [ ] Monetization infrastructure
- [ ] Code patterns to follow

### Nice to Discover
- [ ] Test coverage
- [ ] CI/CD setup
- [ ] Deployment approach
- [ ] Performance characteristics
- [ ] Known issues/tech debt

---

## Edge Cases

### Monorepo Detection
```
ℹ️ Monorepo Detected

This appears to be a monorepo with multiple packages:
- /packages/web
- /packages/api
- /packages/shared

Options:
1. Analyze entire monorepo
2. Focus on specific package: {which?}
3. Analyze shared dependencies only

Which approach?
```

### Minimal Codebase
```
ℹ️ Minimal Codebase

This repo has limited code. Discovery found:
- {X} source files
- {Y} lines of code

This may be:
- A new project (consider greenfield mode)
- A library/package (different enhancement approach)
- Incomplete (more code elsewhere?)

Continue with discovery? [Yes / Switch to greenfield]
```

### No Monetization Found
```
💰 No Monetization Infrastructure

This app has no payment integration detected.

This is a significant enhancement opportunity:
- Add Stripe integration
- Implement subscription tiers
- Add feature gating

Flag this as priority for Phase 1? [Yes / No]
```

---

## Success Criteria

Discovery is complete when:
- [x] Tech stack identified
- [x] Project structure mapped
- [x] Existing Claude Code setup documented
- [x] Data model understood
- [x] API surface catalogued
- [x] Monetization status assessed
- [x] Code patterns documented
- [x] Enhancement opportunities identified
- [x] .enhancer/DISCOVERY.md written
- [x] State updated to Phase 1
- [x] Ready for /enhancer/vision

---

**Discovery maps the territory. Now you know what you're enhancing.**
