
For example when we work with **Claude Code** and make a prompt like "recolor this button", the workflow to get to the result is roughly similar to this:

1. *You type*: “recolor this button.”
2. Claude Code *loads the session context*: your current directory, project files, git state, any `CLAUDE.md` instructions, and the active conversation history.
3. The *model reasons* about what “button” probably refers to and which files are likely relevant.
4. The harness exposes *tools* like file search, file read, edit, shell commands, and tests; the model chooses one, but the tool execution itself is performed by the harness, not the model.
5. *Claude reads the component and stylesheet*, maybe searches for the button’s class name or design system token, then decides on a minimal change.
6. *It proposes or applies the edit*, depending on permission mode, and before editing it can create a reversible snapshot of the file state.
7. *It runs verification*, such as a test, lint, or a quick build step, and uses the output to decide whether more changes are needed.
8. If the result is good, it stops and returns the final answer; if not, it loops again with the new evidence