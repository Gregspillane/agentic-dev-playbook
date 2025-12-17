# Feature Development Workflow

A structured workflow for building substantial features within existing codebases using AI coding agents.

---

## When to Use This

Use this workflow when:

- Adding a significant feature to an existing, established codebase
- The feature is large enough to span multiple development sessions
- You need to preserve consistency with existing patterns and conventions
- Multiple developers (human or AI) may work on the feature

**Not ideal for:**

- Greenfield projects (use the [standard playbook](../README.md) instead)
- Small changes or bug fixes
- Exploratory work where scope is undefined

---

## How It Differs from Greenfield

| Aspect | Greenfield | Feature Development |
|--------|------------|---------------------|
| **Starting Point** | Empty repository | Existing codebase with patterns |
| **Input Document** | Project Brief (whole product) | Feature Brief (scoped to feature) |
| **Overview** | Defines entire product | Defines feature + how it fits existing system |
| **Conventions** | Established during development | Inherited from codebase, extended carefully |
| **Agent Behavior** | Creates new patterns | Discovers and follows existing patterns |
| **Scope Risk** | Building too much | Breaking existing functionality |

---

## Document Structure

Feature documentation lives in a dedicated folder within your project:

```
your-project/
├── docs/
│   └── projects/
│       └── [feature-name]/
│           ├── feature_overview.md    # What the feature is
│           ├── phase_plan.md          # Stories with [TODO]/[DONE]
│           ├── impl_log.md            # Implementation memory
│           ├── AGENT_PROMPT.md        # Session start instructions
│           └── END_SESSION.md         # Session end checklist
└── src/
    └── ... (existing code)
```

---

## The Four Documents

### 1. Feature Overview (`feature_overview.md`)

The source of truth for what the feature does and how it integrates with the existing system.

**Contains:**
- Problem statement and solution
- Core concepts introduced by this feature
- How the feature fits with existing architecture
- API contracts (if applicable)
- Future considerations (out of scope for now)

**Changes:** Rarely, only when feature scope changes

### 2. Phase Plan (`phase_plan.md`)

The work queue, organized into phases and stories.

**Contains:**
- Phases with clear themes
- User stories with tasks and acceptance criteria
- Status markers: `[TODO]`, `[IN_PROGRESS]`, `[DONE]`

**Changes:** Per story (status updates only)

### 3. Implementation Log (`impl_log.md`)

The memory bridge between sessions. This is the most important document for continuity.

**Contains:**
- Project metadata (branch, current state)
- Directory structure (what goes where)
- Key decisions made during implementation
- Implementation history (per-story record)

**Note:** Unlike greenfield, this document does NOT define conventions — it references the existing codebase conventions and documents any extensions.

**Changes:** Every session

### 4. Agent Prompts

Two prompts control the development loop:

- **AGENT_PROMPT.md** — Read at session start, provides operating instructions
- **END_SESSION.md** — Used at session end, ensures documentation is updated

---

## Workflow

### Initial Setup

1. **Create Feature Brief** — Define what you're building (use template)
2. **Generate Documents** — Use generation prompt to create the doc set
3. **Create Feature Branch** — Standard git workflow
4. **Place Documents** — In `docs/projects/[feature-name]/`

### Development Loop

```
┌─────────────────────────────────────────────────────────────┐
│ START SESSION                                               │
│ "Read docs/projects/[feature]/AGENT_PROMPT.md and begin     │
│  work on the next TODO story."                              │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│ REVIEW PLAN                                                 │
│ Agent reads docs, shows implementation plan                 │
│ You approve or adjust                                       │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│ IMPLEMENT                                                   │
│ Agent implements the story                                  │
│ You review and iterate                                      │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│ END SESSION                                                 │
│ Use END_SESSION.md prompt                                   │
│ Agent updates docs and provides handoff                     │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│ CLEAR & REPEAT                                              │
│ New session, full context from docs                         │
└─────────────────────────────────────────────────────────────┘
```

---

## Critical Principles for Feature Development

### 1. Discover Before Inventing

Before creating new patterns, the agent must search the existing codebase for similar implementations. If a pattern exists, follow it exactly.

### 2. Backwards Compatibility

Unless explicitly stated otherwise, existing functionality must continue working. New code is additive, not replacing.

### 3. Test Existing Tests

Before marking a story done, existing tests must still pass. New functionality should have new tests.

### 4. Reference, Don't Duplicate

The agent should reference existing code by file path rather than duplicating patterns in documentation. The codebase IS the convention documentation.

### 5. Scope Discipline

Feature development has more scope creep risk than greenfield. Each story must stay focused on its defined scope.

---

## Story Sizing for Features

Stories should be completable in a single session while being meaningful units of work.

**Right-sized:**
- Implements one cohesive piece of functionality
- Touches a focused set of files
- Has clear acceptance criteria
- Can be tested independently

**Too large (split it):**
- Requires both schema changes AND full UI implementation
- Touches more than one major subsystem
- Has multiple independent acceptance criteria

**Too small (combine it):**
- Just creates a file with no functionality
- Has no testable outcome
- Is a sub-task of another story

**Heuristic:** 3-8 stories for a medium feature, 5-15 for a large feature. If you have 20+ stories, your feature might need to be broken into multiple features.

---

## Templates

- [Feature Brief Template](templates/feature-brief.md) — Define your feature
- [Generation Prompt](templates/feature-generation-prompt.md) — Generate docs from brief
- [Agent Prompt Template](templates/FEATURE_AGENT_PROMPT.md) — Session start instructions
- [End Session Template](templates/FEATURE_END_SESSION.md) — Session end checklist

---

## Example

The Multi-Webhook feature for SafePassage was built using this workflow. See the SafePassage repository for a real-world example:

```
safepassage/docs/projects/multi-webhook/
├── feature_overview.md
├── phase_plan.md
├── impl_log.md
├── AGENT_PROMPT.md
└── END_SESSION.md
```

---

## Getting Started

1. Copy `templates/feature-brief.md` and fill it out for your feature
2. Use `templates/feature-generation-prompt.md` with an AI to generate your doc set
3. Create your feature branch
4. Place generated docs in `docs/projects/[feature-name]/`
5. Start your first session with the AGENT_PROMPT
6. Build iteratively, one story at a time
