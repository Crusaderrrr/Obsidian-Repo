---
creation date: 2026-05-09 14:51
modification date: Saturday, 9th May 2026
tags:
  - programming
  - claude-code
  - ai
  - productivity
note type: Informational Note
source: https://youtu.be/jqoFP9QapXI
---
# 1. Context & Token Management
*The single biggest lever on output quality.* Bloated context = worse code. Collapsed context = lost work. The goal is to stay in the productive middle.

1. **Run `/compact` *before* you need it**
	- Replaces full conversation history with a structured summary, freeing up the context window.
	- Run it proactively at *natural breakpoints* (after finishing a feature, before starting a new module), **not** after Claude has already started degrading.
2. **Recognize *context rot* early**
	- Symptoms: repetitive suggestions, regressing on earlier decisions, ignoring constraints you already set.
	- Fix isn't always `/compact` — sometimes you just need a **fresh session**.
3. **Use `ultrathink` for hard problems**
	- Just type the word `ultrathink` (no slash) in the prompt → triggers the maximum thinking-token budget (~32K).
	- Hierarchy: `think` → `think hard` → `think harder` → `ultrathink`.
	- Reserve it for architecture, complex debugging, algorithm design — *not* boilerplate.
4. **Set the effort level explicitly**
	- Claude Code has 4 effort levels: *low, medium, high, max*.
	- Stating it in the prompt (e.g. *"use low effort for this formatting fix"*) saves tokens on small tasks and pushes quality higher on complex ones.
5. **Keep the MCP server list lean**
	- Every enabled MCP server is dumped into context on every request.
	- Disabling unused servers = free token savings, no prompting required.
6. **Monitor context window usage actively**
	- Don't wait for output quality to drop — watch the UI indicator.
	- Around **~70% full** → either `/compact` or wrap up and start fresh.
7. **Use `/btw` for mid-task questions**
	- Lets you ask a question or add context *without consuming a full turn*.
	- Useful for clarifying mid-flow without bloating context.
8. **Start new sessions for unrelated tasks**
	- A session is **a context window, not a persistent assistant**.
	- New task → new session. Simplest token-management habit there is.

---

# 2. Planning & Prompting
*Better inputs produce better outputs.* These tricks change how intent is communicated **before** Claude writes any code.

9. **Always ask for a plan before any code**
	- Have Claude lay out: which files will change, what approach, what edge cases it's accounting for.
	- Review → correct → then say "proceed". Catches misunderstandings before they become broken code.
10. **Use Opus *plan mode* to front-load thinking**
	- Opus does the *planning* (architecture, approach), then a faster/cheaper model does the *execution*.
	- Get Opus-quality decisions without paying Opus prices on every line.
11. **Front-load *constraints*, not just goals**
	- Most prompts describe what to build. Better prompts describe what *not* to do, what patterns to follow, what conventions to respect.
	- Bad: *"add authentication"*.
	- Good: *"add authentication using the existing JWT pattern in `auth.ts`, no new dependencies, following the error-handling pattern already in the codebase"*.
12. **Use the GSD (Get Stuff Done) framework**
	- Three phases, each with its own clean context state:
		1. **G**ather context
		2. **S**pecify the approach
		3. **D**o the work
	- Prevents earlier exploration from polluting later execution.
13. **Use `/simplify` (and `/batch`)**
	- Claude tends to over-engineer (full abstraction layers, retry logic, caching for a simple data fetch).
	- `/simplify` → ask for the simplest working version.
	- `/batch` → group multiple similar small requests into one efficient pass.
14. **Write *failure modes* into your prompts**
	- Don't only describe the happy path.
	- Include: *"Return an error if the user is not authenticated, use the existing `UnauthorizedError` class, don't throw raw exceptions."*
15. **Ask Claude to critique its own output**
	- After it produces something, ask: *"What's wrong with this? What edge cases does it miss? What would a senior engineer flag in code review?"*
	- Works **far better** than the lazy *"does this look right?"* — which always gets a yes.
16. **Use the *Advisor pattern* for architecture decisions**
	- A capable model (Opus) acts as *advisor* → reviews/validates the approach.
	- A faster, cheaper model does the implementation.
	- Quality stays high without paying for premium compute everywhere.

---

# 3. `claude.md` — Your Permanent Instruction Layer
The `claude.md` file lives at the project root and is **auto-loaded** into Claude's context every session. Highest return-on-effort setup task in Claude Code.

17. **Use `claude.md` to avoid repeating yourself**
	- Right place for: project conventions, naming rules, architecture constraints, anything you'd otherwise type repeatedly.
	- Pro tip from the comments scene: add the line  
	  *"Before writing code, ask clarifying questions until you are 95% confident in the requirements."*  
	  → Causes a dramatic shift: Claude asks clarifying questions instead of generating half-right code.
18. **Keep it focused and short**
	- More content ≠ better output. A bloated file dilutes the most important rules.
	- Only include things that *vary from defaults* — what Claude would otherwise get wrong.
	- ❌ "write tests" (applies to every project — useless here)
	- ✅ "all database queries go through the repository layer" (codebase-specific)
19. **Version-control your `claude.md`**
	- It evolves with your conventions. Commit changes alongside the code that motivated them.
20. **Use multiple `claude.md` files in monorepos**
	- Root-level `claude.md` for global conventions.
	- Subdirectory `claude.md` files for package-specific rules (frontend vs backend, etc.).

---

# 4. Parallel Development & Multi-Agent Patterns

21. **Use *git worktrees* for parallel work**
	- Multiple Claude Code sessions on separate branches of the same repo, simultaneously, no conflicts.
	- Each worktree is isolated — Claude in one doesn't know or care about the others.
	- Practical ceiling: ~4 parallel sessions before a human falls behind.
22. **Use the *Operator pattern* for multi-terminal work**
	- A coordinating Claude instance manages multiple sub-agents in separate terminals.
	- The operator does *no* implementation — just task assignment, monitoring, and unblocking.
23. **Use the *Split-and-Merge pattern* for big analysis tasks**
	- Split a large codebase across sub-agents → each does a subset → final merge step synthesizes.
	- Ideal for security audits, architecture reviews, dependency analysis.
24. **Use *Headless mode* for automated pipelines**
	- Claude Code with no interactive terminal — pipe in instructions, get output programmatically.
	- Use cases: CI/CD, cron jobs, automated code review.
25. **Use sub-agents for codebase analysis**
	- Avoids rate-limit pain and one-massive-context collapse.
	- Each sub-agent owns a module/directory and stays clean.
26. **Commit *checkpoints* before handing off between agents**
	- Clean baseline for the next agent.
	- Easy rollback if something goes wrong.
	- Readable git history.

---

# 5. Hidden Commands & Features

27. **`think`, `think hard`, `think harder`, `ultrathink`**
	- Prompt modifiers that progressively increase reasoning depth.
	- Each step uses more tokens/time — only worth it for genuinely hard problems.
28. **Use *Auto mode* for safer autonomous runs**
	- Claude can act without per-step confirmation, **but** scoped safely — unlike a full *bypass-permissions* flag.
	- The right default for unattended runs.
29. **`/bug` for faster bug reports**
	- Opens a structured bug-report flow that captures context + session state automatically.
	- Faster than writing the report by hand.
30. **Hidden features from the source-code leak**
	- The Claude Code source went public → revealed undocumented slash commands, internal config options, and agent behavior flags.
	- Worth digging into for power users.
31. **The *Buddy* feature** *(easter egg)*
	- A Tamagotchi-style companion that reacts to your coding activity.
	- Not a productivity feature — just charming. Real, though.
32. **Run Claude Code free with Ollama / OpenRouter**
	- Local models via *Ollama* or cheaper access via *OpenRouter*.
	- Quality varies by model, but for many tasks the results are good enough.

---

# 6. Workflow Patterns That Hold Up at Scale
*(Recurring patterns mentioned throughout the video — the meta-tricks.)*

- **Batch small tasks together** with `/batch` instead of running ten micro-sessions. Session-setup overhead × 10 is real.
- **Start complex tasks with a *research phase*** — *"Read these files and tell me what you understand about the current architecture. Don't write any code yet."* The output becomes the spec for the next phase.
- **Use *structured output formats* for handoffs** — when one session hands work to another, force a specific format: what was done, what's left, current codebase state. Free-form summaries are too ambiguous.
- **Keep a `TASK.md` log file** — Claude updates it at each step with done / in-progress / next. If the session dies or you `/compact`, the log gives a clean resumption point that doesn't depend on conversation history.

---

# 7. Key Takeaways
- *Context management* is the **biggest lever** on output quality → `/compact` proactively, monitor usage, fresh session for unrelated tasks.
- *Planning before coding* consistently produces better output → ask for a plan, review, then proceed. Use plan mode for complex features.
- *`claude.md`* is the **highest ROI setup task** → write once, focused and short, benefit on every session.
- *Git worktrees* remove the biggest bottleneck in multi-feature dev — one session blocking another.
- *Effort modifiers* (`think`, `ultrathink`) and *slash commands* (`/btw`, `/simplify`, `/batch`) give fine-grained control over cost vs quality.
- *Multi-agent patterns* (operator, split-and-merge, headless) handle work that's too big for a single session.

> [!tip] These tricks compound
> The teams shipping most effectively aren't using *one* trick — they're combining context discipline, good prompting habits, a well-maintained `claude.md`, and parallel patterns for large tasks.

---

# Source
- 🎥 Video: [32 Tricks to Level Up Claude Code in 16 Mins](https://youtu.be/jqoFP9QapXI?si=nkcIzYo0rUnnv3Bd)

# Relative Info
- [[00 - Programming MoC]]
- [[Real Workflow]]
- [[Clean Code]]
- [[The most important coding rules]]
