---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - git
  - GitHub
note type: Informational Note
---
# Commands
`git init` - initiate a repository
`rm -rf .git` - completely delete git repository / uninitialize it 
`git status` - status of the repository
`git add .` - add all changes to the staging area for the next commit 
`git reset .` - unstage all files 
`git commit` - commit changes to the repository
`git commit -m "message"` - commit with message
`git branch` - show all branches
`git checkout -b feature` - create `-b` feature branch and checkout to it

`git stash` - stashes without untracked files
`git stash pop` - Applies the most recent stashed changes to your working directory and removes that stash from the stash stack
`git stash apply` - Applies the most recent stashed changes to your working directory but keeps the stash in the stack
`git stash -u` - saves staged and unstaged files temporally   

`git merge feature` - merges all the changes from `feature` branch with the current branch
`git merge feature --squash` - merges the feature branch into the current branch, squashing all its commits into a single staged change

`git push` - pushes all changes to the repository 

`git clone url` - copies the repository from url

`git revert [HEAD]` - used to cancel the last commit for the **remote** repo
`git reset [HEAD]` - used to cancel the last commit for the **local** repo
 
If we want to *exclude* some files or folders from our git repository:
- we need to create a `.gitignore` file 
- add folders like `node_modules/` with the `/` in the end 
- add files like `fileName.js` 