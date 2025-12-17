# TaskFlow Product Overview

This document defines the conceptual foundation of TaskFlow. It serves as the source of truth for product behavior, architecture, and business rules.

---

## 1. What is TaskFlow?

TaskFlow is a lightweight task management platform for small teams. It provides:

1. **Simple Task Management:** Create, organize, and track tasks with status, priority, and due dates
2. **Team Collaboration:** Invite team members, assign tasks, and comment on work
3. **API-First Design:** Full REST API for programmatic access and integrations

TaskFlow is designed for teams who want task management without the complexity of full project management tools.

---

## 2. Actors & Personas

### 2.1 Team Member
An individual contributor who uses TaskFlow to track their work.

Team Members:
- Create and manage their own tasks
- View tasks assigned to them
- Update task status and add comments
- View team activity

### 2.2 Team Admin
A team organizer with additional permissions.

Team Admins:
- All Team Member capabilities, plus:
- Invite and remove team members
- Create and manage projects
- Access team-wide settings
- Generate and manage API keys

### 2.3 API Consumer
A developer or system integrating with TaskFlow programmatically.

API Consumers:
- Authenticate using API keys
- Perform CRUD operations on tasks and projects
- Query task data for external systems

---

## 3. Core Flows

### 3.1 User Registration Flow

```
User visits TaskFlow
    ↓
Clicks "Sign Up"
    ↓
Enters email, password, name
  OR
Clicks "Continue with Google"
    ↓
Account created
    ↓
Prompted to create team or join via invite
```

### 3.2 Team Creation Flow

```
New user completes registration
    ↓
Clicks "Create Team"
    ↓
Enters team name
    ↓
Team created, user is Admin
    ↓
Redirected to empty dashboard
    ↓
Prompted to create first project or invite members
```

### 3.3 Team Invitation Flow

```
Admin opens Settings → Team Members
    ↓
Clicks "Invite Member"
    ↓
Enters email address
    ↓
System sends invite email (via Resend)
    ↓
Invitee clicks link in email
    ↓
If new user: Creates account
If existing user: Logs in
    ↓
Joins team as Member
    ↓
Redirected to team dashboard
```

**Rules:**
- Invites expire after 7 days
- Admins can resend or revoke pending invites
- Users can belong to multiple teams

### 3.4 Task Creation Flow

```
User on dashboard
    ↓
Clicks "New Task" (or uses keyboard shortcut)
    ↓
Modal opens with form:
  - Title (required)
  - Description (optional)
  - Project (optional, defaults to Inbox)
  - Priority (Low/Medium/High/Urgent, defaults to Medium)
  - Due Date (optional)
  - Assignee (optional)
    ↓
User fills form and saves
    ↓
Task created with status "To Do"
    ↓
Task appears in appropriate list
```

**Rules:**
- Tasks without a project appear in "Inbox"
- Creator is recorded for attribution
- Created timestamp is recorded

### 3.5 Task Update Flow

```
User views task (from list or detail view)
    ↓
Can update:
  - Status (To Do → In Progress → Done)
  - Priority
  - Due Date
  - Assignee
  - Description
    ↓
Changes saved immediately
    ↓
Activity logged
```

### 3.6 Task Completion Flow

```
User clicks task checkbox
  OR
User opens task and sets status to "Done"
    ↓
Completion timestamp recorded
    ↓
Task moves to "Completed" section
    ↓
Task remains visible for 30 days
    ↓
After 30 days, task is archived (hidden from default views)
```

### 3.7 API Authentication Flow

```
User opens Settings → API Keys
    ↓
Clicks "Create API Key"
    ↓
Enters key name (for identification)
    ↓
System generates key, displays once
    ↓
User copies key (cannot be retrieved later)
    ↓
Key stored as hash in database
    ↓
API requests include: Authorization: Bearer <key>
    ↓
System validates key hash
    ↓
Request proceeds with user/team context
```

**Rules:**
- Keys are never stored in plain text
- Keys can be revoked (immediate effect)
- Last-used timestamp is tracked

---

## 4. Data Model Concepts

### 4.1 User
Represents an individual with a TaskFlow account.

- **ID:** Unique identifier
- **Email:** Primary identifier, unique
- **Name:** Display name
- **Password Hash:** Bcrypt hash (null for OAuth-only users)
- **Created At:** Account creation timestamp

### 4.2 Team
A workspace containing projects and tasks.

- **ID:** Unique identifier
- **Name:** Team display name
- **Created At:** Team creation timestamp

### 4.3 Team Member (Join Table)
Links users to teams with roles.

- **User ID:** Reference to User
- **Team ID:** Reference to Team
- **Role:** "admin" or "member"
- **Joined At:** When user joined the team

### 4.4 Project
A grouping of related tasks within a team.

- **ID:** Unique identifier
- **Team ID:** Owning team
- **Name:** Project name
- **Description:** Optional description
- **Created At:** Creation timestamp

### 4.5 Task
The core work item.

- **ID:** Unique identifier
- **Project ID:** Owning project (nullable for Inbox)
- **Team ID:** Owning team (for Inbox tasks without project)
- **Creator ID:** User who created the task
- **Assignee ID:** User assigned to the task (nullable)
- **Title:** Task title
- **Description:** Optional detailed description
- **Status:** "todo", "in_progress", "done"
- **Priority:** "low", "medium", "high", "urgent"
- **Due Date:** Optional due date
- **Created At:** Creation timestamp
- **Completed At:** Completion timestamp (nullable)

### 4.6 Comment
A comment on a task.

- **ID:** Unique identifier
- **Task ID:** Parent task
- **User ID:** Comment author
- **Content:** Comment text
- **Created At:** Comment timestamp

### 4.7 API Key
Authentication credential for API access.

- **ID:** Unique identifier
- **User ID:** Owning user
- **Team ID:** Scoped to team
- **Name:** Human-readable identifier
- **Key Hash:** Bcrypt hash of the key
- **Created At:** Creation timestamp
- **Last Used At:** Last API request timestamp

---

## 5. Security Model

### 5.1 Authentication
- **Web:** Email/password or Google OAuth via NextAuth.js
- **API:** Bearer token (API key)

### 5.2 Authorization
- Users can only access data within their teams
- API keys are scoped to a single team
- Role-based access:
  - **Member:** CRUD on tasks/comments, view projects
  - **Admin:** All Member permissions + team settings, member management, API key management

### 5.3 Data Protection
- Passwords hashed with bcrypt (cost factor 12)
- API keys hashed, never stored plain
- All traffic over HTTPS
- Rate limiting on auth endpoints (10 req/min)

### 5.4 Trust Boundaries
- Web UI authenticated via session cookie
- API authenticated via bearer token
- All mutations require authentication
- Team data is isolated by team_id foreign keys

---

## 6. Technical Stack

- **Framework:** Next.js 14+ (App Router)
- **Language:** TypeScript (strict mode)
- **Database:** PostgreSQL
- **ORM:** Prisma
- **Styling:** Tailwind CSS + shadcn/ui
- **Auth:** NextAuth.js (email/password + Google OAuth)
- **Email:** Resend (transactional emails)
- **Validation:** Zod
- **Hosting:** Vercel

---

## 7. Out of Scope (v1)

- **Mobile apps:** Web-only for v1
- **Real-time updates:** Polling/refresh, no WebSocket
- **File attachments:** Text-only tasks
- **Recurring tasks:** One-time tasks only
- **Time tracking:** No estimates or time logging
- **External integrations:** No Slack, webhooks, or third-party integrations beyond the API
- **Advanced permissions:** Admin/member roles only, no custom roles
- **Task dependencies:** No blocking/dependency relationships
- **Subtasks:** Flat task structure only
