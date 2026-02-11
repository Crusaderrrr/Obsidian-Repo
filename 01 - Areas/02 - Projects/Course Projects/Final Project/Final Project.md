---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - courses
note type: Informational Note
---
#### Step 2: Login/Register UI (Client-Side)

- **Goal**: Build responsive login and registration pages with guest mode, theme, and language support.
- **Tasks**:
    - Create LoginForm.tsx: Email, password, submit, guest mode button, register link.
    - Create RegisterForm.tsx: Name, email, password, confirm password, submit, login link.
    - Add Header.tsx: Search bar, language selector (English/Spanish), theme toggle (light/dark).
    - Use react-hook-form and zod for form validation.
    - Implement i18next for translations.
    - Style with Bootstrap for responsiveness.
    - Add ThemeContext.tsx for light/dark theme switching.
    - Test accessibility (ARIA labels, keyboard navigation).

#### Step 3: Server Setup and Authentication (Server-Side)

- **Goal**: Set up the Express server, database, and authentication APIs to connect login/register.
- **Tasks**:
    - Install Prisma: npm install prisma @prisma/client.
    - Set up PostgreSQL (local or cloud like Heroku Postgres).
    - Define schema.prisma with User model (id, name, email, password, role).
    - Run migrations: npx prisma migrate dev.
    - Create API routes:
        - POST /api/auth/register: Validate input, hash password (bcryptjs), create user, return JWT (jsonwebtoken).
        - POST /api/auth/login: Validate credentials, return JWT.
        - GET /api/auth/me: Protected route to fetch user data.
    - Add middleware to verify JWT for protected routes.
    - Connect client forms to APIs using axios.

#### Step 4: Main Page for Non-Authenticated Users

- **Goal**: Build the main page with a gallery, top 5 popular templates, and tag cloud for non-authenticated users.
- **Tasks**:
    - Create MainPage.tsx with:
        - Gallery of latest templates (Bootstrap cards: title, description, image, author).
        - Table of top 5 templates (sorted by form count).
        - Tag cloud (use react-tagcloud).
    - Add server APIs:
        - GET /api/templates/public: Fetch public templates.
        - GET /api/tags: Fetch tags for tag cloud.
    - Update Header.tsx with login/register buttons for non-authenticated users.
    - Ensure responsiveness and accessibility.
#### Step 5: Template Viewing (Read-Only for Non-Authenticated Users)

- **Goal**: Allow non-authenticated users to view public templates in read-only mode.
- **Tasks**:
    - Create TemplatePage.tsx to display:
        - Template details (title, description with markdown via marked, topic, image).
        - Questions (read-only, no editing).
        - Comments (view-only, no adding).
        - Likes (view count, disabled for guests).
    - Add server API:
        - GET /api/templates/:id: Fetch template by ID (public or restricted with access check).
    - Disable actions (e.g., “Fill Form” button) with tooltips (“Log in to fill”).
    - Add full-text search API (GET /api/search) and SearchResults.tsx page.

#### Step 6: Template Creation and Management (Authenticated Users)

- **Goal**: Enable authenticated users to create, edit, and manage templates.
- **Tasks**:
    - Update schema.prisma with Template, Question, Tag, TemplateTag, TemplateUser models.
    - Create TemplateForm.tsx for creating/editing templates:
        - Fields: title, description (markdown), topic (dropdown), image (cloud upload via cloudinary), tags (autocomplete with react-select), access (public/restricted with user autocomplete).
        - Questions: Up to 4 per type (single-line, multi-line, integer, checkbox), drag-and-drop reordering (use react-beautiful-dnd).
    - Add server APIs:
        - POST /api/templates: Create template.
        - PUT /api/templates/:id: Update template.
        - DELETE /api/templates/:id: Delete template.
    - Create UserDashboard.tsx with sortable tables for templates and forms.

#### Step 7: Form Filling and Results

- **Goal**: Allow authenticated users to fill forms and view results.
- **Tasks**:
    - Create FormFill.tsx to fill a template’s questions (auto-include user and date fields).
    - Add server APIs:
        - POST /api/forms: Create form with answers.
        - GET /api/templates/:id/forms: Fetch forms for a template.
    - Update TemplatePage.tsx with tabs:
        - General settings.
        - Questions.
        - Results (list of forms with links).
        - Aggregations (e.g., average for numeric fields).
    - Ensure only admins or form/template owners can edit/delete forms.

#### Step 8: Admin Features

- **Goal**: Implement admin page for user and content management.
- **Tasks**:
    - Create AdminPage.tsx with:
        - User management table (view, block, unblock, delete, add/remove admin).
        - Ability for admins to edit any template/form.
    - Add server APIs:
        - GET /api/users: List users (admin-only).
        - PATCH /api/users/:id: Update user status/role.
        - DELETE /api/users/:id: Delete user.
    - Ensure admins can remove their own admin access.

#### Step 9: Comments, Likes, and Real-Time Updates

- **Goal**: Add commenting and liking features with real-time comment updates.
- **Tasks**:
    - Update TemplatePage.tsx to show comment list and add comment form (authenticated users only).
    - Add server APIs:
        - POST /api/templates/:id/comments: Add comment.
        - POST /api/templates/:id/likes: Add like (one per user).
    - Use WebSockets (socket.io) for real-time comment updates (2-5s delay allowed).

#### Step 10: Testing, Polish, and Final Deployment

- **Goal**: Test the app, fix bugs, and deploy the final version.
- **Tasks**:
    - Test all features (guest mode, authentication, template creation, form filling, admin actions).
    - Ensure responsiveness, accessibility, and multilingual support.
    - Optimize performance (e.g., add indexes in Prisma, paginate API results).
    - Deploy client (Vercel/Netlify) and server (Render/Heroku).
    - Document progress and prepare for defense.