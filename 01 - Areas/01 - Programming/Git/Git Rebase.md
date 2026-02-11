---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - git
note type: Informational Note
---
Git rebase works like that:
![[Pasted image 20250923131341.png]]
`git rebase main`
![[Pasted image 20250923131409.png]]
`git rebase bugFix`
![[Pasted image 20250923131450.png]]

So, basically it *takes all the commits* from one branch and places them on top of the other branch, where we rebase.

## Why Use Git Rebase

- To maintain a **clean, linear project history** without unnecessary merge commits.
- It streamlines commit history making it easier to follow changes chronologically.
- Facilitates **easier debugging and bisecting** since the commit log is less cluttered.
- Helps keep your feature branch updated with the latest commits from the main branch before merging back.
- Can be used interactively to edit, squash, reorder, or remove commits for a cleaner commit history before publishing.