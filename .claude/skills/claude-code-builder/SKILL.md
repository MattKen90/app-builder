---
name: claude-code-builder
description: Build Claude Code primitives correctly. Use when creating slash commands, skills, rules, agents, hooks, or CLAUDE.md files. Reference for proper frontmatter, file structure, and patterns.
allowed-tools: Read, Glob, Grep, Write, Edit
---

# Claude Code Builder

Reference for building Claude Code primitives. Always consult this before creating or modifying:

- Slash commands (`/commands`)
- Skills
- Rules
- Agents
- Hooks
- Memory files (CLAUDE.md)

## Quick Reference

| Primitive | Location | Key File | Frontmatter Required |
|-----------|----------|----------|---------------------|
| Commands | `.claude/commands/` | `*.md` | Yes (`description`) |
| Skills | `.claude/skills/{name}/` | `SKILL.md` | Yes (`name`, `description`) |
| Rules | `.claude/rules/` | `*.md` | Optional (`paths`) |
| Agents | `.claude/agents/` | `*.md` | Yes (TBD) |
| Hooks | `.claude/hooks/` | `*.json` | N/A (JSON format) |
| Memory | `CLAUDE.md` or `.claude/CLAUDE.md` | `CLAUDE.md` | No |

---

## Commands

**Location:** `.claude/commands/*.md` or `.claude/commands/**/*.md`

**Invocation:** `/command-name` or `/folder/command-name`

**Frontmatter:**
```yaml
---
description: Brief description shown in command list
argument-hint: [optional-arg] - hint for arguments
---
```

**Arguments:** Access via `$ARGUMENTS` in the command body.

**Example:**
```markdown
---
description: Initialize a new feature workspace
argument-hint: [feature-name]
---

# Initialize Feature

Create workspace for feature: $ARGUMENTS

1. Create directory
2. Generate spec template
3. Update state
```

---

## Skills

**Location:** `.claude/skills/{skill-name}/SKILL.md`

**Invocation:** Automatic (Claude decides based on description match)

**Frontmatter:**
```yaml
---
name: skill-name
description: What it does and when to use it. Include trigger keywords.
allowed-tools: Read, Grep, Glob  # Optional: restrict tools
model: claude-sonnet-4-20250514  # Optional: specific model
---
```

**Multi-file pattern:**
```
.claude/skills/my-skill/
├── SKILL.md        # Required: overview + navigation
├── reference.md    # Detailed docs (loaded when needed)
├── examples.md     # Usage examples
└── scripts/
    └── helper.py   # Utility scripts (executed, not loaded)
```

**Best practices:**
- Keep SKILL.md under 500 lines
- Put detailed reference in separate files
- Description is critical - Claude uses it to decide when to apply

---

## Rules

**Location:** `.claude/rules/*.md` (recursive)

**Loading:** Automatic on startup (same priority as CLAUDE.md)

**Frontmatter (optional):**
```yaml
---
paths: src/**/*.ts  # Only load when working with matching files
---
```

**Without frontmatter:** Rule loads unconditionally (universal).

**With paths:** Rule only loads when Claude works with matching files.

**Glob patterns:**
| Pattern | Matches |
|---------|---------|
| `**/*.ts` | All TypeScript files |
| `src/**/*` | Everything under src/ |
| `*.md` | Markdown in root only |
| `src/**/*.{ts,tsx}` | TS and TSX under src/ |

---

## Agents

**Location:** `.claude/agents/*.md`

<!-- TODO: Add agent documentation when available -->

---

## Hooks

**Location:** `.claude/hooks/*.json` or `.claude/settings.json`

<!-- TODO: Add hooks documentation when available -->

---

## Memory (CLAUDE.md)

**Locations (priority order):**
1. Enterprise: `/Library/Application Support/ClaudeCode/CLAUDE.md`
2. Project: `./CLAUDE.md` or `./.claude/CLAUDE.md`
3. User: `~/.claude/CLAUDE.md`
4. Local: `./CLAUDE.local.md` (gitignored, personal)

**Imports:**
```markdown
See @README for project overview.
See @docs/architecture.md for design.
```

**Best practices:**
- Keep operational (commands, workflows)
- Domain instructions go in `.claude/rules/`
- Auto-loaded, no configuration needed
