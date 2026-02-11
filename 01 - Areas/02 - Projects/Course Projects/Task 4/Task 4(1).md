---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - work
note type: Informational Note
---
## Core Requirements:

1. **Database**: Create a UNIQUE INDEX on email field (storage-level uniqueness guarantee)
2. **UI Components**:
    - Table matching the provided screenshot
    - Toolbar with Block, Unblock, Delete actions
    - Checkboxes for multiple selection (including select all)
3. **Sorting**: Data sorted by last login time
4. **Authentication**: Check user exists and isn't blocked before each request
5. **Tech Stack**: JavaScript/TypeScript + React + Database of choice

## Key Features to Implement:

- [ ] User registration/login (no email confirmation needed)
- [ ] User management table with: checkbox, name, email, last login, status
- [ ] All users can block/delete themselves or others
- [ ] Blocked users can't login, deleted users can re-register
- [x] Responsive design using CSS framework (Bootstrap recommended)
- [ ] Proper error handling, tooltips, status messages
- [ ] Deploy to accessible hosting
- [x] .gitignore

*Example of a login page*:
![[preview.webp]]

*Example of a table with toolbar*:
![[preview-1.webp]]
* No need to show sparklines with previous user activity.
