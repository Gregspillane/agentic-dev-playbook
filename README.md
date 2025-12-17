# Agentic Development Playbook

A structured workflow for building software with AI coding agents. This playbook enables autonomous, session-based development while keeping humans in the loop through clear documentation and step-by-step execution.

---

## Two Workflows

This playbook provides two workflows for different scenarios:

| Workflow | Use Case | Starting Point |
|----------|----------|----------------|
| **[Greenfield](#greenfield-workflow)** | New projects from scratch | Empty repository |
| **[Feature Development](feature-development/)** | Substantial features in existing codebases | Established codebase |

**Choose Greenfield when:** Building a new project, the repository is empty or nearly empty, you're establishing patterns from scratch.

**Choose Feature Development when:** Adding a significant feature to an existing codebase, patterns and conventions already exist, backwards compatibility matters.

---

## Why This Exists

AI coding agents (Claude Code, Codex, Cursor, etc.) are powerful but have a fundamental limitation: **they have no memory between sessions**. Each new session starts fresh with no context about what was built before, what patterns were established, or what decisions were made.

This playbook solves that problem through structured documentation that serves as the memory bridge between sessions. The AI reads the docs, does the work, updates the docs, and the next session picks up exactly where the last one left off.

---

## Greenfield Workflow

For new projects built from scratch.

### How It Works

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

### Quick Start (Greenfield)

1. **Create Your Project Brief** — Copy `templates/project-brief.md` and fill it out
2. **Generate Your Document Set** — Use `templates/generation-prompt.md` to produce overview, phase plan, and impl log
3. **Set Up Your Repository** — Place docs and start coding
4. **Build Iteratively** — One story per session, update docs, repeat

### Repository Structure (Greenfield)

```
your-project/
├── docs/
│   ├── overview.md
│   ├── phase_plan.md
│   └── impl_log.md
├── AGENT_PROMPT.md
├── AGENT_END.md
└── src/
```

---

## Feature Development Workflow

For adding substantial features to existing codebases.

**[→ Full Feature Development Guide](feature-development/)**

### Key Differences from Greenfield

| Aspect | Greenfield | Feature Development |
|--------|------------|---------------------|
| **Starting Point** | Empty repository | Existing codebase |
| **Input Document** | Project Brief | Feature Brief |
| **Conventions** | Established during development | Inherited, extended carefully |
| **Agent Behavior** | Creates patterns | Discovers and follows patterns |
| **Primary Risk** | Building too much | Breaking existing functionality |

### Quick Start (Feature Development)

1. **Create Feature Brief** — Copy `feature-development/templates/feature-brief.md`
2. **Generate Feature Docs** — Use `feature-development/templates/feature-generation-prompt.md`
3. **Create Feature Branch** — Standard git workflow
4. **Place Docs** — In `docs/projects/[feature-name]/`
5. **Build Iteratively** — Same loop, but with backwards compatibility focus

### Repository Structure (Feature Development)

```
existing-project/
├── docs/
│   └── projects/
│       └── [feature-name]/
│           ├── feature_overview.md
│           ├── phase_plan.md
│           ├── impl_log.md
│           ├── AGENT_PROMPT.md
│           └── END_SESSION.md
├── CLAUDE.md                    # Existing project conventions
└── src/                         # Existing codebase
```

---

## Core Principles

These apply to both workflows:

1. **One story per session** — Each session implements exactly one user story. Small enough to complete without context loss, large enough to avoid overhead.

2. **Documentation is memory** — The implementation log carries patterns, conventions, and decisions forward. What isn't documented doesn't persist.

3. **Conventions are law** — Once a pattern is established and documented, all future sessions follow it exactly. Consistency compounds.

4. **Human in the loop** — Humans review at phase boundaries and can intervene at any story. Autonomous doesn't mean unsupervised.

---

## Repository Contents

```
agentic-dev-playbook/
├── README.md                              # You are here
├── docs/
│   └── workflow.md                        # Detailed greenfield workflow
│
├── templates/                             # Greenfield templates
│   ├── project-brief.md
│   ├── generation-prompt.md
│   ├── AGENT_PROMPT.md
│   └── AGENT_END.md
│
├── feature-development/                   # Feature development workflow
│   ├── README.md                          # Feature workflow guide
│   └── templates/
│       ├── feature-brief.md               # Define your feature
│       ├── feature-generation-prompt.md   # Generate feature docs
│       ├── FEATURE_AGENT_PROMPT.md        # Session start (features)
│       └── FEATURE_END_SESSION.md         # Session end (features)
│
└── examples/                              # Greenfield example
    ├── example-brief.md
    └── generated/
        ├── overview.md
        ├── phase_plan.md
        └── impl_log.md
```

---

## When to Use Which

### Greenfield Workflow

**Good fit:**
- New projects with clear scope
- Projects that will take multiple sessions/days
- Teams sharing AI coding work across members
- Projects where you're establishing patterns

**Less ideal:**
- Quick prototypes or spikes
- Highly exploratory work
- Single-session tasks
- Adding to existing codebases

### Feature Development Workflow

**Good fit:**
- Substantial features in existing codebases
- Features spanning multiple sessions
- Work requiring backwards compatibility
- Features touching multiple parts of the system

**Less ideal:**
- Small bug fixes or tweaks
- Exploratory spikes
- Greenfield projects
- Single-file changes

---

## Key Documents Explained

| Document | Purpose | Updates |
|----------|---------|---------|
| **Project/Feature Brief** | Input — defines what you're building | Once at start |
| **Overview** | Source of truth for behavior | Rarely |
| **Phase Plan** | Work queue with all stories | Per story (status only) |
| **Impl Log** | Session memory — state, history | Every session |
| **Agent Prompt** | Operating instructions | Per project/feature |

---

## Documentation

- [Detailed Greenfield Workflow](docs/workflow.md) — Deep dive into greenfield development
- [Feature Development Guide](feature-development/) — Complete feature workflow
- [Greenfield Templates](templates/) — Starting points for new projects
- [Feature Templates](feature-development/templates/) — Starting points for features
- [Example Project](examples/) — See greenfield workflow in action

---

## Contributing

This playbook emerged from real project experience. If you find improvements or have suggestions, contributions are welcome.

## License

MIT
