# Development Rules

**Agent delegation is default.** Fork context to specialized agents. One message, multiple parallel tool calls.

**Grep over Read.** Search across files with Grep, not by reading multiple files.

**Zero-BS.** No `NotImplementedError`, no TODO placeholders, no stubs. Working code or nothing.

**Test before presenting.** Never ask user to validate what you could have checked.

**No time estimates.** Just execute.

**No version references.** Present tense only. Write as if the feature always existed.

**No preamble/postamble.** Be direct. Answer the question. Stop.

**Primitives.** Never build Claude Code primitives from memory—always consult docs first.

---

## Design Principles

**Regenerate, don't patch.** When changes are needed, rewrite the module from spec rather than line-editing. Each feature is a self-contained "brick" with stable interfaces.

**Decision framework.** For every implementation choice, ask in order:
1. Do we need this right now?
2. What's the simplest solution?
3. Can we solve this more directly?
4. Does complexity add proportional value?
5. How easy to understand and change later?

**Library vs custom.** Use libraries for complex solved problems (auth, crypto). Write custom for simple needs, domain-specific logic, or when libraries need workarounds.

**Embrace complexity only for:** Security, data integrity, core UX, error visibility.

**Aggressively simplify:** Internal abstractions, future-proofing, edge cases, framework usage, state management.
