# Agentic Development Playbook

A structured workflow for building software with AI coding agents. This playbook enables autonomous, session-based development while keeping humans in the loop through clear documentation and step-by-step execution.

## Why This Exists

AI coding agents (Claude Code, Codex, Cursor, etc.) are powerful but have a fundamental limitation: **they have no memory between sessions**. Each new session starts fresh with no context about what was built before, what patterns were established, or what decisions were made.

This playbook solves that problem through structured documentation that serves as the memory bridge between sessions. The AI reads the docs, does the work, updates the docs, and the next session picks up exactly where the last one left off.

## How It Works

```
┌─────────────────────────────────────────────────────────────┐
│                         INITIALIZE                          │
├─────────────────────────────────────────────────────────────┤
│  1. Create Project Brief (define what you're building)      │
│  2. Generate document set (overview, phase plan, impl log)  │
│  3. Initialize repository                                   │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                      DEVELOPMENT LOOP                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   ┌───────────┐    ┌───────────┐    ┌───────────┐          │
│   │  START    │ -> │ IMPLEMENT │ -> │    END    │          │
│   │  SESSION  │    │   STORY   │    │  SESSION  │          │
│   └───────────┘    └───────────┘    └───────────┘          │
│        │                                   │                │
│        │      Read docs, find next         │                │
│        │      [TODO], implement it,        │                │
│        │      update all docs              │                │
│        │                                   │                │
│        └───────────────────────────────────┘                │
│                    Repeat per story                         │
└─────────────────────────────────────────────────────────────┘
```

## Core Principles

1. **One story per session** — Each session implements exactly one user story. Small enough to complete without context loss, large enough to avoid overhead.

2. **Documentation is memory** — The implementation log carries patterns, conventions, and decisions forward. What isn't documented doesn't persist.

3. **Conventions are law** — Once a pattern is established and documented, all future sessions follow it exactly. Consistency compounds.

4. **Human in the loop** — Humans review at phase boundaries and can intervene at any story. Autonomous doesn't mean unsupervised.

## Quick Start

### 1. Create Your Project Brief

Copy `templates/project-brief.md` and fill it out for your project. This captures:
- What you're building and why
- Who uses it
- Technical stack and constraints
- What's in scope vs. out of scope
- How you want to phase the work

### 2. Generate Your Document Set

Use the generation prompt (`templates/generation-prompt.md`) to produce:
- `docs/overview.md` — Product truth, flows, data models
- `docs/phase_plan.md` — All phases and user stories
- `docs/impl_log.md` — Session memory template

### 3. Set Up Your Repository

```
your-project/
├── docs/
│   ├── overview.md
│   ├── phase_plan.md
│   └── impl_log.md
├── AGENT_PROMPT.md      # Copy from templates/
├── AGENT_END.md         # Copy from templates/
└── src/
```

### 4. Start Building

Each coding session:
1. Point the agent at `AGENT_PROMPT.md`
2. Agent reads docs, finds next `[TODO]` story
3. Agent implements, tests, updates docs
4. End session with `AGENT_END.md` checklist

## Repository Contents

```
agentic-dev-playbook/
├── README.md                          # You are here
├── docs/
│   └── workflow.md                    # Detailed workflow documentation
├── templates/
│   ├── project-brief.md               # Template for defining your project
│   ├── generation-prompt.md           # Prompt to generate doc set
│   ├── AGENT_PROMPT.md                # Session start instructions
│   └── AGENT_END.md                   # Session end checklist
└── examples/
    ├── example-brief.md               # Sample completed brief
    └── generated/                     # Sample generated documents
        ├── overview.md
        ├── phase_plan.md
        └── impl_log.md
```

## When to Use This

**Good fit:**
- Greenfield projects with clear scope
- Projects that will take multiple sessions/days
- Teams sharing AI coding work across members
- Projects where consistency matters

**Less ideal:**
- Quick prototypes or spikes
- Highly exploratory work where scope is undefined
- Single-session tasks

## Key Documents Explained

| Document | Purpose | Updates |
|----------|---------|---------|
| **Project Brief** | Input — defines what you're building | Once at start |
| **Overview** | Source of truth for product behavior | Rarely |
| **Phase Plan** | Work queue with all stories | Per story (status only) |
| **Impl Log** | Session memory — conventions, state, history | Every session |
| **Agent Prompt** | Operating instructions for the AI | Per project (if customization needed) |

## Documentation

- [Detailed Workflow Guide](docs/workflow.md) — Deep dive into how everything works
- [Project Brief Template](templates/project-brief.md) — Starting point for new projects
- [Example Project](examples/) — See the workflow in action

## Contributing

This playbook emerged from real project experience. If you find improvements or have suggestions, contributions are welcome.

## License

MIT
