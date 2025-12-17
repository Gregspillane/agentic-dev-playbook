# Workflow Guide

This document provides a detailed explanation of the agentic development workflow — how it operates, why it was designed this way, and how to use it effectively.

---

## The Problem

AI coding agents are stateless. Every session starts fresh with no memory of:
- What was built in previous sessions
- What patterns and conventions were established
- What decisions were made and why
- Where the project currently stands

Without a solution, each session risks:
- Reinventing patterns that already exist
- Making inconsistent decisions
- Losing context that took time to establish
- Requiring extensive re-explanation from humans

## The Solution

This workflow creates a **documentation-driven memory system** where:

1. **Documentation is the only handoff mechanism** — Everything the next session needs is written down
2. **Conventions are explicit and binding** — Patterns documented in the impl log are followed exactly
3. **Work is structured as discrete stories** — Each session has a clear, bounded scope
4. **State is always known** — The current phase, next story, and completed work are tracked explicitly

---

## Document Hierarchy

Four documents work together:

### 1. Project Brief (Input)

The single source input used to generate everything else. Created once at project start.

**Contains:**
- Project identity and problem statement
- Actors and personas
- Core capabilities and flows
- Technical stack and constraints
- Scope definition (in/out)
- Phasing strategy

**Changes:** Never (after initial creation)

### 2. Overview (`docs/overview.md`)

The source of truth for product behavior, architecture, and business rules.

**Contains:**
- What the product is
- How it behaves (detailed flows)
- Data model concepts
- Security model
- Technical stack details
- What's explicitly out of scope

**Changes:** Rarely — only when fundamental product decisions change

### 3. Phase Plan (`docs/phase_plan.md`)

The complete work queue, organized into phases and stories.

**Contains:**
- All phases with themes
- Every user story with tasks and acceptance criteria
- Status markers (`[TODO]`, `[IN_PROGRESS]`, `[DONE]`)

**Changes:** Per story — only the status marker changes as work progresses

### 4. Implementation Log (`docs/impl_log.md`)

The memory bridge between sessions. This is the most frequently updated document.

**Contains:**
- **Current State** — Where we are, what's next
- **Codebase Conventions** — Patterns that must be followed (critical)
- **Directory Structure** — Project layout
- **Technical Decisions** — Architectural choices with rationale
- **Implementation History** — Per-story record of what was built

**Changes:** Every session — this is how context persists

---

## The Convention System

The **Codebase Conventions** section in the impl log is the most important part of this workflow.

### Why Conventions Matter

When an AI reads the impl log, it needs to immediately know:
- Where files go
- How things are named
- What patterns to follow for common tasks
- What has been decided so it doesn't re-decide

Conventions buried in implementation history entries get missed. Conventions in the dedicated section are always found.

### What Gets Documented as Convention

- File organization (where each type of file lives)
- Naming conventions (files, components, hooks, types, constants)
- Route structure (for web projects)
- Component patterns (modals, forms, lists, etc.)
- State management patterns
- Styling patterns
- Any other pattern that future sessions should replicate

### The Convention Rule

**Once documented, conventions are binding.**

If the conventions say components go in `src/components/` and are named in kebab-case, every future session follows that exactly. No exceptions without explicit human override.

### Updating Conventions

When a session establishes a new pattern:

1. Note it in the Implementation History entry ("Patterns Established")
2. **Add it to the Codebase Conventions section**

The validation question:
> "If the next session ONLY reads Codebase Conventions, will they know about the patterns I just created?"

If no → update Conventions before ending the session.

---

## Session Lifecycle

### Starting a Session

1. **Agent reads `impl_log.md`** — Especially Current State and Codebase Conventions
2. **Agent reads `phase_plan.md`** — Finds the next `[TODO]` story
3. **Agent reads `overview.md`** — If any behavior questions arise

The agent now has full context without human explanation.

### Working on a Story

1. **Restate the story** — Copy title, description, tasks, acceptance criteria
2. **Pre-flight check:**
   - Have I read conventions?
   - Have I identified existing patterns that apply?
   - Have I checked for similar implementations in the codebase?
3. **Plan the implementation** — List files, cite patterns to follow
4. **Implement** — Match existing patterns exactly
5. **Verify** — Confirm all acceptance criteria are met

### Ending a Session

1. **Update `phase_plan.md`** — Mark story `[DONE]`
2. **Update `impl_log.md`:**
   - Current State (next story)
   - Implementation History (what was done)
   - Codebase Conventions (if new patterns established)
3. **Confirm** — Story done, next story identified, conventions updated if needed

---

## Story Sizing

Stories should be completable within a single session. This means:

### Right-Sized Stories

- Narrow scope that fits in working memory
- Can be implemented, tested, and documented without context loss
- Clear start and end points

### Signals a Story is Too Large

- Touches more than 3-4 major files
- Introduces more than 2 new patterns
- Requires both UI and backend when phasing separates them
- Has multiple independent acceptance criteria that could stand alone

### Signals a Story is Too Small

- Can be completed in minutes
- Has no meaningful acceptance criteria
- Is just a sub-task of another story

### The Heuristic

If a capability requires multiple distinct components or flows, split it into sequential stories. Each story should represent a coherent increment of functionality.

---

## Phasing Strategy

Phases organize work into logical groupings. The phase structure emerges from the Project Brief's phasing strategy.

### Common Phasing Patterns

**UI-First / Mock-First:**
- Early phases build UI shells with mock data
- Later phases replace mocks with real backend
- Good for: Projects where UX validation is important early

**Vertical Slices:**
- Each phase implements a complete feature end-to-end
- Good for: Projects with independent feature sets

**Foundation → Features → Polish:**
- Phase 1: Infrastructure and scaffolding
- Phases 2-N: Feature implementation
- Final phases: Polish, testing, documentation

### Phase Boundaries

Phases should have natural boundaries:
- A complete UI shell
- A working integration
- A functional feature set

Human review happens at phase boundaries before proceeding.

---

## Error Handling

### When Requirements Are Unclear

Stop and ask. Don't guess at product behavior. The overview is the source of truth — if something isn't covered there, get clarification.

### When Patterns Conflict

Follow the most recently established pattern in Conventions. If there's genuine conflict, flag it for human resolution.

### When a Story Can't Be Completed

Document what was attempted, what blocked progress, and what the next session needs to know. Update impl_log with this context even if the story stays `[TODO]`.

### When the Agent Makes Mistakes

Mistakes happen. The impl log provides recovery:
- Check Implementation History for what was actually done
- Review Conventions for what should have been followed
- Course-correct in the next session

---

## Multi-Developer Scenarios

This workflow supports teams sharing AI coding work:

### Handoff Between Team Members

The documentation IS the handoff. Any team member can:
1. Read the impl_log
2. Understand current state and conventions
3. Pick up the next story
4. Continue with full context

### Parallel Work

For parallel work on different stories:
- Ensure stories are truly independent
- Each developer works in their own session
- Merge documentation updates carefully (impl_log conflicts)
- Consider having one person own impl_log updates

### Review Points

- Phase completion is a natural review point
- Any team member can review the impl_log for pattern consistency
- Overview changes should be reviewed by the team

---

## Customizing the Workflow

### Agent Prompt Customization

The standard agent prompts work for most projects. Customize when:
- Non-standard file organization
- Unusual technology stack
- Project-specific workflows
- Multiple distinct interfaces with different requirements

### Convention Bootstrapping

If your team has existing conventions:
1. Pre-populate the Conventions section in impl_log before starting
2. Conventions from the brief become initial entries
3. AI follows these from session one

### Phase Plan Adjustments

The generated phase plan isn't sacred. Adjust based on:
- Learnings during development
- Priority changes
- Scope adjustments

When adjusting, update both phase_plan.md and note the change in impl_log Technical Decisions.

---

## Common Pitfalls

### Skipping Convention Updates

The most common failure mode. Session establishes new pattern → doesn't add to Conventions → next session reinvents or conflicts.

**Fix:** Make convention updates part of the session end checklist. Don't skip it.

### Stories Too Large

Session can't complete the story → incomplete state → next session confused about what's done.

**Fix:** If you realize a story is too large mid-implementation, stop, document where you are, and split the remaining work into new stories.

### Ignoring the Overview

Making product decisions without checking the overview → inconsistent behavior → technical debt.

**Fix:** Any behavior question should prompt an overview check. If not covered, update the overview with the decision.

### Documentation Drift

Docs become stale → agents follow outdated patterns → inconsistency.

**Fix:** Treat documentation updates as required, not optional. They're part of the story, not an afterthought.

---

## Success Criteria for the Workflow

You know it's working when:

1. **Session starts are fast** — Agent reads docs and starts working without explanation
2. **Patterns are consistent** — Code looks like it was written by one person
3. **Context isn't lost** — No re-explaining decisions or patterns
4. **Human intervention is minimal** — Agent handles the work; human reviews at boundaries
5. **Progress is visible** — Phase plan shows clear progress; impl log tells the story

---

## Getting Started

1. Read the [Project Brief Template](../templates/project-brief.md)
2. Create a brief for your project
3. Use the [Generation Prompt](../templates/generation-prompt.md) to produce your doc set
4. Set up your repository with the standard structure
5. Start your first session with [AGENT_PROMPT.md](../templates/AGENT_PROMPT.md)

See [examples/](../examples/) for a complete worked example.
