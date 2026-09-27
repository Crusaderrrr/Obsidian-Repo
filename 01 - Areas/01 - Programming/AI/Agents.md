- These are small workers that do the job that is assigned to them.
- Every agent has its own context window
- They can have different tools access, permissions, skills, mcp servers, etc.
- Can be created manually by adding a .md file to `.claude/agents/`

**Example of an agent**:
```md
---
name: test-runner
description: Run the test suite and report failures. Invoke after any code change.
model: sonnet
tools: ["bash", "read"]
---

You are a focused test runner. Run the project test suite, identify failing
tests, and report results clearly. Do not fix bugs — only report what failed and why.
```

**Ways the agent can be invoked**:
- Automatically if task is appropriate for it
- By suggesting in the prompt ("use test-runner agent"), Claude may comply about it and not invoke it.
- By `@`-mention, guaranteed invocation.