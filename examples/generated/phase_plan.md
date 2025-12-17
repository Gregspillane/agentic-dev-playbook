# TaskFlow Phase Plan

This document contains all phases, user stories, tasks, and acceptance criteria for the TaskFlow project.  
Update story status as work progresses: `[TODO]` → `[IN_PROGRESS]` → `[DONE]`

---

## Phase 1A — Project Foundation

### [TODO] 1A-1 — Next.js Project Setup

**User Story:**  
As a developer, I need a properly configured Next.js project with TypeScript, Tailwind, and shadcn/ui so I can begin building features.

**Tasks:**  
- Initialize Next.js 14+ with App Router and TypeScript
- Configure Tailwind CSS
- Install and configure shadcn/ui
- Set up ESLint and Prettier
- Create basic folder structure: `/app`, `/components`, `/lib`, `/types`, `/actions`
- Add environment variable template (`.env.example`)
- Configure TypeScript strict mode

**Acceptance Criteria:**  
- `npm run dev` starts development server
- Tailwind styles work correctly
- shadcn/ui components can be imported
- TypeScript compilation succeeds with strict mode
- ESLint passes with no errors

---

### [TODO] 1A-2 — Base Layout & Design System

**User Story:**  
As a developer, I need consistent design tokens and a base layout structure so the application has a cohesive look.

**Tasks:**  
- Define color palette in Tailwind config (brand colors, semantic colors)
- Set up typography scale
- Create base layout component
- Add favicon and metadata
- Install initial shadcn/ui components (Button, Card, Input, etc.)

**Acceptance Criteria:**  
- Design tokens are documented in Tailwind config
- Base layout renders
- Application has proper metadata and favicon

---

## Phase 1B — Dashboard Shell

### [TODO] 1B-1 — Dashboard Layout with Sidebar

**User Story:**  
As a team member, I see a dashboard layout with sidebar navigation so I can access different sections of the app.

**Tasks:**  
- Create dashboard layout with collapsible sidebar
- Add navigation items: Tasks, Projects, Team, Settings
- Implement responsive behavior (mobile menu)
- Add user identity section in sidebar (avatar, name)
- Create placeholder pages for each nav item

**Acceptance Criteria:**  
- Sidebar displays all navigation items
- Active route is highlighted
- Sidebar collapses on mobile with hamburger menu
- Layout is responsive

---

### [TODO] 1B-2 — Task List Page (Mock Data)

**User Story:**  
As a team member, I see my tasks on the main dashboard so I know what work I need to do.

**Tasks:**  
- Create `/dashboard` route as task list view
- Create mock data structure for tasks
- Display tasks grouped by status (To Do, In Progress, Done)
- Show task title, priority badge, due date, assignee avatar
- Add empty state for no tasks

**Acceptance Criteria:**  
- Task list loads with mock data
- Tasks are grouped by status
- Priority is visually indicated
- Due dates and assignees are displayed
- Empty state shows when no tasks

---

### [TODO] 1B-3 — Mock Data Store Setup

**User Story:**  
As a developer, I have a centralized mock data store so UI development can proceed without a backend.

**Tasks:**  
- Create `/lib/mock-data/` directory
- Define TypeScript types for all entities (User, Team, Project, Task, Comment)
- Create mock data seeds
- Create React context for mock state
- Add dispatch mechanism for mock mutations

**Acceptance Criteria:**  
- Mock data is accessible throughout the app
- Data structures match planned schema
- Mock state can be modified for testing UI interactions

---

### [TODO] 1B-4 — Create Task Modal

**User Story:**  
As a team member, I can create a new task so I can track work that needs to be done.

**Tasks:**  
- Create "New Task" button in dashboard header
- Build task creation modal with form fields:
  - Title (required)
  - Description (optional)
  - Project selector (optional)
  - Priority selector (default: Medium)
  - Due date picker (optional)
  - Assignee selector (optional)
- Save to mock data store
- Close modal and refresh list on success

**Acceptance Criteria:**  
- Modal opens from "New Task" button
- All form fields work correctly
- Validation prevents empty title
- New task appears in list after creation
- Modal closes on success

---

### [TODO] 1B-5 — Task Detail View

**User Story:**  
As a team member, I can view and edit task details so I can update my work.

**Tasks:**  
- Create task detail modal/drawer
- Display all task fields with edit capability
- Add status change buttons (To Do → In Progress → Done)
- Show task metadata (created by, created at)
- Implement delete task with confirmation

**Acceptance Criteria:**  
- Clicking a task opens detail view
- All fields are editable
- Status can be changed
- Delete requires confirmation
- Changes persist to mock store

---

## Phase 2A — Projects & Organization

### [TODO] 2A-1 — Projects List Page

**User Story:**  
As a team member, I can view all projects so I can organize my work by project.

**Tasks:**  
- Create `/dashboard/projects` route
- Display projects as cards with name, description, task count
- Add "New Project" button
- Show empty state for no projects

**Acceptance Criteria:**  
- Projects page loads with mock data
- Each project shows task count
- Empty state is helpful
- New Project button is visible

---

### [TODO] 2A-2 — Create/Edit Project

**User Story:**  
As a team admin, I can create and edit projects so I can organize team work.

**Tasks:**  
- Build project creation modal (name, description)
- Add edit functionality for existing projects
- Implement delete project with confirmation
- Update mock data store

**Acceptance Criteria:**  
- Projects can be created with name and description
- Existing projects can be edited
- Delete requires confirmation
- Changes persist to mock store

---

### [TODO] 2A-3 — Project Detail View

**User Story:**  
As a team member, I can view tasks within a specific project so I can focus on project work.

**Tasks:**  
- Create `/dashboard/projects/[id]` route
- Display project header with name and description
- Show filtered task list (only tasks in this project)
- Add "New Task" that pre-selects this project

**Acceptance Criteria:**  
- Project detail page loads correctly
- Only tasks in this project are shown
- New tasks default to this project
- Navigation back to projects list works

---

## Phase 2B — Team & Settings UI

### [TODO] 2B-1 — Team Members Page

**User Story:**  
As a team admin, I can view team members so I can manage my team.

**Tasks:**  
- Create `/dashboard/team` route
- Display member list with avatar, name, email, role
- Show "Invite Member" button (admin only)
- Add role badge (Admin/Member)

**Acceptance Criteria:**  
- Team page shows all members
- Roles are clearly indicated
- Invite button visible for admins
- Mock data shows realistic team

---

### [TODO] 2B-2 — Invite Member Flow (UI Only)

**User Story:**  
As a team admin, I can invite new members so they can join my team.

**Tasks:**  
- Create invite modal with email input
- Show pending invites list
- Add resend and revoke actions
- Display success/error states

**Acceptance Criteria:**  
- Invite modal accepts email
- Pending invites are displayed
- Resend and revoke buttons work (mock)
- Success message shows after invite

---

### [TODO] 2B-3 — Settings Page Structure

**User Story:**  
As a user, I can access settings so I can manage my account and team.

**Tasks:**  
- Create `/dashboard/settings` route
- Add settings navigation: Profile, Team, API Keys
- Create placeholder pages for each section
- Build profile settings (name, email display)

**Acceptance Criteria:**  
- Settings page loads with navigation
- Profile section shows user info
- Navigation between sections works

---

### [TODO] 2B-4 — API Keys UI (Mock)

**User Story:**  
As a team admin, I can manage API keys so developers can integrate with TaskFlow.

**Tasks:**  
- Create API Keys settings section
- Display existing keys (name, created date, last used)
- Build create key modal
- Show key once on creation (copy button)
- Add revoke key functionality

**Acceptance Criteria:**  
- API keys are listed with metadata
- New keys can be created
- Key value shown once with copy button
- Revoke requires confirmation

---

## Phase 3A — Database & Auth Setup

### [TODO] 3A-1 — Database Schema

**User Story:**  
As a developer, I have a database schema so the application can persist data.

**Tasks:**  
- Initialize Prisma with PostgreSQL
- Create schema for: User, Team, TeamMember, Project, Task, Comment, ApiKey
- Add appropriate indexes and constraints
- Run initial migration
- Create seed script with sample data

**Acceptance Criteria:**  
- Prisma schema compiles without errors
- Migration runs successfully
- Seed script populates test data
- All relationships are correctly defined

---

### [TODO] 3A-2 — NextAuth Configuration

**User Story:**  
As a user, I can sign up and log in so I can access my tasks.

**Tasks:**  
- Install and configure NextAuth.js
- Set up credentials provider (email/password)
- Set up Google OAuth provider
- Create auth API routes
- Implement password hashing with bcrypt

**Acceptance Criteria:**  
- Users can sign up with email/password
- Users can log in with email/password
- Google OAuth login works
- Session persists across page loads

---

### [TODO] 3A-3 — Auth Pages

**User Story:**  
As a user, I see login and signup pages so I can access my account.

**Tasks:**  
- Create `/auth/login` page
- Create `/auth/signup` page
- Add Google OAuth button
- Implement form validation with Zod
- Add error handling and display

**Acceptance Criteria:**  
- Login page renders correctly
- Signup page renders correctly
- Form validation works
- Errors are displayed clearly
- OAuth button initiates flow

---

### [TODO] 3A-4 — Protected Routes

**User Story:**  
As a developer, dashboard routes are protected so only authenticated users can access them.

**Tasks:**  
- Create auth middleware
- Protect all `/dashboard/*` routes
- Redirect unauthenticated users to login
- Pass user context to dashboard pages

**Acceptance Criteria:**  
- Unauthenticated users redirected to login
- Authenticated users can access dashboard
- User context available in protected pages

---

## Phase 3B — Core API Implementation

### [TODO] 3B-1 — Task API Endpoints

**User Story:**  
As an API consumer, I can perform CRUD operations on tasks.

**Tasks:**  
- Create `GET /api/tasks` (list tasks)
- Create `POST /api/tasks` (create task)
- Create `GET /api/tasks/[id]` (get task)
- Create `PATCH /api/tasks/[id]` (update task)
- Create `DELETE /api/tasks/[id]` (delete task)
- Add Zod validation for all inputs
- Implement authorization checks

**Acceptance Criteria:**  
- All endpoints work correctly
- Input validation returns proper errors
- Users can only access their team's tasks
- Response format is consistent

---

### [TODO] 3B-2 — Project API Endpoints

**User Story:**  
As an API consumer, I can perform CRUD operations on projects.

**Tasks:**  
- Create `GET /api/projects` (list projects)
- Create `POST /api/projects` (create project)
- Create `GET /api/projects/[id]` (get project)
- Create `PATCH /api/projects/[id]` (update project)
- Create `DELETE /api/projects/[id]` (delete project)
- Add task count to project responses

**Acceptance Criteria:**  
- All endpoints work correctly
- Projects include task count
- Authorization enforced
- Consistent response format

---

### [TODO] 3B-3 — Comment API Endpoints

**User Story:**  
As an API consumer, I can add and view comments on tasks.

**Tasks:**  
- Create `GET /api/tasks/[id]/comments` (list comments)
- Create `POST /api/tasks/[id]/comments` (add comment)
- Create `DELETE /api/comments/[id]` (delete own comment)
- Include user info in comment responses

**Acceptance Criteria:**  
- Comments can be added to tasks
- Comments list includes author info
- Users can only delete own comments
- Consistent response format

---

## Phase 4A — Connect UI to Backend

### [TODO] 4A-1 — Replace Mock Data with API Calls

**User Story:**  
As a user, the dashboard shows my real data from the database.

**Tasks:**  
- Replace mock task list with API call
- Replace mock project list with API call
- Update create/edit/delete to use API
- Add loading states
- Add error handling

**Acceptance Criteria:**  
- Dashboard shows real data
- CRUD operations persist to database
- Loading states display during fetches
- Errors are handled gracefully

---

### [TODO] 4A-2 — Team Data Integration

**User Story:**  
As a user, I see real team member data in the UI.

**Tasks:**  
- Create team member API endpoints
- Connect team page to real data
- Update assignee selectors to use real users
- Show real user avatars and names

**Acceptance Criteria:**  
- Team page shows real members
- Assignee dropdowns show team members
- User context is accurate throughout

---

## Phase 5A — Team Features

### [TODO] 5A-1 — Team Invitation System

**User Story:**  
As a team admin, I can invite members who receive email invitations.

**Tasks:**  
- Create invitation database model
- Build invitation API endpoints
- Integrate Resend for email delivery
- Create invitation acceptance flow
- Handle invite expiration (7 days)

**Acceptance Criteria:**  
- Invitations are sent via email
- Invite links work correctly
- Expired invites are rejected
- New users can create accounts from invite
- Existing users can accept invites

---

### [TODO] 5A-2 — API Key Authentication

**User Story:**  
As an API consumer, I can authenticate using API keys.

**Tasks:**  
- Create API key generation endpoint
- Implement key hashing (bcrypt)
- Build API key validation middleware
- Track last-used timestamp
- Create key revocation endpoint

**Acceptance Criteria:**  
- API keys can be generated
- Keys authenticate API requests
- Last-used is tracked
- Revoked keys are rejected immediately

---

## Phase 6A — Polish & Production

### [TODO] 6A-1 — Error Handling & Edge Cases

**User Story:**  
As a user, I see helpful error messages when things go wrong.

**Tasks:**  
- Implement global error boundary
- Add form-level error display
- Handle network errors gracefully
- Add 404 page
- Add loading skeletons

**Acceptance Criteria:**  
- Errors display user-friendly messages
- Network errors don't crash the app
- 404 page exists
- Loading states are smooth

---

### [TODO] 6A-2 — Rate Limiting

**User Story:**  
As a system, auth endpoints are rate limited to prevent abuse.

**Tasks:**  
- Implement rate limiting middleware
- Apply to auth endpoints (10 req/min)
- Apply to API endpoints (100 req/min)
- Return proper 429 responses

**Acceptance Criteria:**  
- Rate limits are enforced
- 429 response includes retry-after
- Legitimate usage is not impacted

---

### [TODO] 6A-3 — Production Configuration

**User Story:**  
As a developer, I can deploy the application to production.

**Tasks:**  
- Configure Vercel deployment
- Set up production database
- Configure environment variables
- Set up error monitoring
- Create deployment documentation

**Acceptance Criteria:**  
- Application deploys to Vercel
- Production database is configured
- Environment variables are secure
- Monitoring is active
