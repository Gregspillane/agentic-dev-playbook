# TaskFlow Implementation Log

This document tracks implementation progress and serves as the memory bridge between development sessions.

---

## Current State

**Last Updated:** 2024-01-15  
**Current Phase:** Phase 1A — Project Foundation  
**Next Story:** 1A-1 — Next.js Project Setup

**Completed Stories:** (none yet)

**Completed Phases:** (none yet)

---

## Codebase Conventions

**Follow these patterns exactly. They were established intentionally.**

### File Organization

| Type | Location | Example |
|------|----------|---------|
| Pages | `src/app/[route]/page.tsx` | `src/app/dashboard/page.tsx` |
| Layouts | `src/app/[route]/layout.tsx` | `src/app/dashboard/layout.tsx` |
| API Routes | `src/app/api/[route]/route.ts` | `src/app/api/tasks/route.ts` |
| Server Actions | `src/actions/[domain].ts` | `src/actions/tasks.ts` |
| Layout Components | `src/components/layout/` | `sidebar.tsx`, `header.tsx` |
| Feature Components | `src/components/[feature]/` | `tasks/task-card.tsx` |
| UI Components | `src/components/ui/` | shadcn/ui only |
| Types | `src/types/[domain].ts` | `src/types/task.ts` |
| Utilities | `src/lib/[name].ts` | `src/lib/utils.ts` |
| Mock Data | `src/lib/mock-data/` | `context.tsx`, `seeds.ts` |
| Database | `prisma/schema.prisma` | Single schema file |

### Naming Conventions

- **Files:** kebab-case (`task-card.tsx`, `mock-data.ts`)
- **Components:** PascalCase (`TaskCard`, `DashboardLayout`)
- **Hooks:** camelCase with `use` prefix (`useTasks`, `useCurrentUser`)
- **Types/Interfaces:** PascalCase (`Task`, `CreateTaskInput`)
- **Constants:** SCREAMING_SNAKE_CASE (`TASK_STATUS`, `PRIORITY_LEVELS`)
- **API Routes:** kebab-case folders (`/api/api-keys/route.ts`)

### Route Structure

- `/` — Landing page (public)
- `/auth/*` — Authentication pages (login, signup)
- `/dashboard` — Main task list
- `/dashboard/projects` — Projects list
- `/dashboard/projects/[id]` — Project detail
- `/dashboard/team` — Team members
- `/dashboard/settings` — Settings (profile, team, API keys)

### Component Patterns

**To be expanded as patterns emerge during development.**

### Styling Patterns

- Use Tailwind CSS utility classes
- Use shadcn/ui components for UI elements
- Use `cn()` helper for conditional classes
- Define custom colors in `tailwind.config.ts`

### API Response Pattern

```typescript
// Success
{ data: T, error: null }

// Error  
{ data: null, error: { code: string, message: string } }
```

### Validation Pattern

- Use Zod schemas for all input validation
- Schemas live alongside their API routes or actions
- Reuse schemas between client and server

---

## Directory Structure

```
taskflow/
├── docs/
│   ├── overview.md
│   ├── phase_plan.md
│   └── impl_log.md
├── prisma/
│   └── schema.prisma
├── src/
│   ├── app/
│   │   ├── (auth)/
│   │   │   ├── login/
│   │   │   └── signup/
│   │   ├── api/
│   │   │   ├── tasks/
│   │   │   ├── projects/
│   │   │   └── auth/
│   │   └── dashboard/
│   │       ├── projects/
│   │       ├── team/
│   │       └── settings/
│   ├── actions/
│   ├── components/
│   │   ├── layout/
│   │   ├── tasks/
│   │   ├── projects/
│   │   └── ui/
│   ├── lib/
│   │   ├── mock-data/
│   │   └── utils.ts
│   └── types/
└── public/
```

---

## Technical Decisions Log

*Populated when significant architectural decisions are made.*

---

## Implementation History

*Populated per-story with: date, story ID, files created/modified, key decisions, patterns established.*
