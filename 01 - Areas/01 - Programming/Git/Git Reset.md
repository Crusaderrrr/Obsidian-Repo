`git reset` is used to revert the state of the project and has **3 stages**:
1. `--soft <commit>`
	This one is used to move HEAD to `<commit>`, and all the **changes since** `<commit>` are ready to be recommitted
2. `--mixed <commit>`
	Changes since `<commit>` are still in the files but unstaged. Basically "undo my last commit but keep changes"
3. `--hard <commit>` 
	Everything since `<commit>` is gone.

**Common target:** `<commit>` is often `HEAD~1` (one commit back), `HEAD` itself (to just unstage without moving commits — that's `git reset` with no soft/hard flag, using `HEAD` implicitly), or a specific commit hash.