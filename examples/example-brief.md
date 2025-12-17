# Project Brief: TaskFlow

## 1. Project Identity (Required)

**Name:** TaskFlow

**One-liner:** A simple task management API with a web dashboard for small teams.

**Problem Statement:** Small teams need a lightweight way to track tasks without the complexity of full project management tools. TaskFlow provides a simple API-first task manager with a clean web interface for teams who want to get things done without learning a complex tool.

---

## 2. Actors & Personas (Required)

### Team Member
- **Role:** Individual contributor who creates and completes tasks
- **Goals:** Track their own work, see what's assigned to them, mark things done
- **Key Actions:** Create tasks, update task status, view their task list, comment on tasks

### Team Admin
- **Role:** Team organizer who manages the workspace
- **Goals:** Set up the team, manage members, oversee task distribution
- **Key Actions:** Invite members, create projects, assign tasks, view team dashboard

### API Consumer
- **Role:** Developer integrating TaskFlow into other tools
- **Goals:** Programmatically create/update tasks, sync with other systems
- **Key Actions:** Authenticate via API key, CRUD operations on tasks and projects

---

## 3. Core Capabilities (Required)

- **Task Management:** Create, update, delete, and organize tasks with status, priority, and due dates
- **Project Organization:** Group tasks into projects for logical separation
- **Team Collaboration:** Assign tasks to team members, add comments
- **API Access:** Full REST API for programmatic access
- **Dashboard:** Web interface for managing tasks and viewing team activity

---

## 4. Key Flows (Required)

### Task Creation Flow
```
User opens dashboard → Clicks "New Task" → Enters title, description, due date, priority → Optionally assigns to team member → Optionally selects project → Saves → Task appears in list
```
**Notes:** Tasks without a project go to "Inbox". Priority levels: Low, Medium, High, Urgent.

### Task Completion Flow
```
User views task list → Clicks task checkbox or opens task → Marks as complete → Task moves to completed section → Completion timestamp recorded
```
**Notes:** Completed tasks remain visible in "Completed" filter for 30 days, then archive.

### Team Invitation Flow
```
Admin opens Settings → Team Members → Invite → Enters email → System sends invite email → Invitee clicks link → Creates account → Joins team
```
**Notes:** Invites expire after 7 days. Admins can resend or revoke.

### API Authentication Flow
```
User generates API key in Settings → Copies key → Uses key in Authorization header → API validates key → Request proceeds
```
**Notes:** Keys can be revoked. Each key has a name for identification.

---

## 5. Technical Stack (Required)

- **Framework:** Next.js 14+ (App Router)
- **Language:** TypeScript (strict mode)
- **Database:** PostgreSQL
- **ORM:** Prisma
- **Styling:** Tailwind CSS + shadcn/ui
- **Auth:** NextAuth.js with email/password + OAuth (Google)
- **Hosting:** Vercel

---

## 6. Integrations (If Applicable)

- **Email (Resend):** Transactional emails for invites, password reset
- **OAuth (Google):** Social login option

---

## 7. Scope Definition (Required)

### In Scope (v1)
- User authentication (email/password + Google OAuth)
- Team workspaces with invite system
- Task CRUD with status, priority, due date, assignee
- Project organization
- Task comments
- REST API with API key authentication
- Web dashboard for all operations
- Basic activity feed

### Out of Scope (v1)
- Mobile apps — web-only for v1
- Real-time updates — polling/refresh for v1
- File attachments — text-only tasks
- Recurring tasks — one-time tasks only
- Time tracking — no time estimates or logging
- Integrations beyond API — no Slack/webhook integrations yet
- Advanced permissions — admin/member only, no custom roles

---

## 8. Phasing Strategy (Required)

**Approach:** UI-first with mock data, then backend implementation

- **Phases 1-2:** Project foundation and dashboard UI shell with mock data
- **Phases 3-4:** Database schema, authentication, and core API
- **Phase 5:** Connect UI to real API
- **Phase 6:** Team features (invites, collaboration)
- **Phase 7:** Polish and production readiness

**Mock vs. Real:** Mock data through Phase 2. Database and real API starting Phase 3. UI connects to real backend in Phase 5.

---

## 9. Conventions & Patterns (Optional)

### File Organization
- API routes in `src/app/api/`
- Server actions in `src/actions/`
- Database models via Prisma in `prisma/schema.prisma`

### Code Patterns
- Use server components by default, client components only when needed
- Zod for all input validation
- Return consistent API response shapes

---

## 10. Data Model (Optional)

- **User:** id, email, name, passwordHash, createdAt
- **Team:** id, name, createdAt
- **TeamMember:** userId, teamId, role (admin/member), joinedAt
- **Project:** id, teamId, name, description, createdAt
- **Task:** id, projectId, creatorId, assigneeId, title, description, status, priority, dueDate, createdAt, completedAt
- **Comment:** id, taskId, userId, content, createdAt
- **ApiKey:** id, userId, teamId, name, keyHash, createdAt, lastUsedAt

---

## 11. Security Requirements (Optional)

- Passwords hashed with bcrypt
- API keys hashed, never stored in plain text
- Users can only access their own team's data
- Rate limiting on auth endpoints

---

## 12. Success Criteria (Optional)

- [ ] User can sign up, create a team, and invite members
- [ ] Tasks can be created, assigned, and completed
- [ ] API allows full CRUD with proper authentication
- [ ] Dashboard is responsive and usable
- [ ] No major security vulnerabilities
