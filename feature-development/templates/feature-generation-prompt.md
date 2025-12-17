# Feature Documentation Generation Prompt

Use this prompt to generate your feature's documentation set from a completed Feature Brief.

---

## How to Use

1. Complete the [Feature Brief Template](feature-brief.md) for your feature
2. Provide the completed brief to an AI assistant along with this prompt
3. Optionally provide relevant existing code context (schema files, related modules)
4. Review and adjust the generated documents
5. Place documents in your repository at `docs/projects/[feature-name]/`

---

## The Prompt

Copy everything below this line and provide it along with your completed Feature Brief:

---

You are a technical architect preparing documentation for a feature development workflow. You will receive a Feature Brief describing a new feature being added to an existing codebase. Generate a complete document set that enables autonomous, session-based development.

## Context

This is **feature development**, not greenfield:
- The codebase already exists with established patterns
- The feature must integrate with existing architecture
- Backwards compatibility is critical
- Existing conventions must be followed, not created

## Input

You will be given a **Feature Brief** containing:
- Feature identity and problem statement
- Current state of the relevant system
- Proposed solution and core concepts
- User stories and capabilities
- Technical approach (data model, API, UI changes)
- Scope definition (in/out)
- Backwards compatibility requirements
- Phasing strategy

## Output

Generate the following documents:

---

### 1. Feature Overview (`feature_overview.md`)

The source of truth for what this feature does and how it integrates with the existing system.

**Structure:**
```markdown
# [Feature Name] — Feature Overview

## Problem Statement
[What problem this solves, who needs it, why now]

## Solution
[High-level description of the approach]

## Core Concepts
[New entities, models, or abstractions introduced]

### [Concept Name]
| Field | Type | Description |
|-------|------|-------------|
| ... | ... | ... |

## Integration with Existing System
[How this fits with current architecture]

## API Contracts (if applicable)
[New endpoints, request/response formats]

## Backwards Compatibility
[What's preserved, migration approach]

## Limits & Constraints
[Rate limits, maximums, security considerations]

## Future Considerations (Out of Scope)
[What's not being built now but may come later]
```

**Tone:** Stable, authoritative. Changes only when feature scope changes.

---

### 2. Phase Plan (`phase_plan.md`)

The complete breakdown of work into phases and stories.

**Structure:**
```markdown
# [Feature Name] — Phase Plan

**Branch:** `[branch-name]`
**Base:** `[base-branch]`
**Status:** Not Started

---

## Phase [N] — [Theme]

### [STATUS] [ID] — [Title]

**User Story:**
As a [actor], I need [capability] so that [benefit].

**Tasks:**
- [Concrete implementation task]
- [Concrete implementation task]

**Acceptance Criteria:**
- [ ] [Testable criterion]
- [ ] [Testable criterion]

---

## Summary

| Phase | Story | Focus | Status |
|-------|-------|-------|--------|
| ... | ... | ... | ... |

**Total Stories:** [N]
```

**Story Sizing:**
- Each story should be completable in a single focused session
- 3-8 stories for medium features, 5-15 for large features
- Avoid stories that touch both schema and full UI in one shot
- Each story should have testable acceptance criteria

**Status Markers:** `[TODO]`, `[IN_PROGRESS]`, `[DONE]`

**Phase Naming:** `Phase [N] — [Theme]` or `Phase [N][Letter] — [Theme]`

---

### 3. Implementation Log (`impl_log.md`)

The memory bridge between sessions.

**Structure:**
```markdown
# [Feature Name] — Implementation Log

## Project Metadata

| Field | Value |
|-------|-------|
| **Branch** | `[branch-name]` |
| **Base** | `[base-branch]` |
| **Started** | Not yet started |
| **Last Updated** | — |
| **Current Phase** | [First phase] |
| **Current Story** | [First story ID] |

---

## Directory Structure

[Where new code will live within the existing structure]

```
existing-project/
├── existing/
│   └── code/
└── new/
    └── feature/
        └── code/
```

---

## Key Decisions

[Empty — populated during implementation when significant decisions are made]

---

## Implementation Entries

[Empty — populated per-story with date, story ID, files created/modified, notes]

---

## Testing Notes

[Commands to run tests, manual testing checklist]

---

## References

- Feature Overview: `docs/projects/[feature]/feature_overview.md`
- Phase Plan: `docs/projects/[feature]/phase_plan.md`
- Related existing code: [paths to relevant existing modules]
```

**Critical Difference from Greenfield:** This document does NOT define codebase conventions. It references existing conventions and documents only decisions specific to this feature.

---

### 4. Agent Prompt (`AGENT_PROMPT.md`)

Operating instructions for the development agent.

**Key adaptations for feature development:**
- Must read existing codebase conventions (CLAUDE.md or equivalent)
- Must search for similar implementations before creating new patterns
- Must verify existing tests still pass
- Must maintain backwards compatibility

Use the [FEATURE_AGENT_PROMPT.md template](FEATURE_AGENT_PROMPT.md) as the base, customizing the paths and project-specific details.

---

### 5. End Session Prompt (`END_SESSION.md`)

Checklist for ending a development session.

Use the [FEATURE_END_SESSION.md template](FEATURE_END_SESSION.md) as the base, customizing paths.

---

## Generation Guidelines

1. **Respect Existing Architecture:** The feature must fit the existing system, not reshape it.

2. **Story Granularity:** Aim for 3-8 stories for medium features. If you're generating 15+ stories, consolidate — the feature brief's phasing strategy should guide this.

3. **Explicit Backwards Compatibility:** Every story that touches existing code should note what must continue working.

4. **Reference, Don't Duplicate:** Point to existing code locations rather than copying patterns into docs.

5. **Testable Criteria:** Every acceptance criterion must be verifiable. Avoid vague criteria.

6. **Phase Boundaries:** Phases should have natural boundaries — complete a layer (schema, API, UI) or a vertical slice before moving on.

---

## Output Format

Return each document in full, clearly separated:

```
# === FEATURE_OVERVIEW.MD ===

[full content]

# === PHASE_PLAN.MD ===

[full content]

# === IMPL_LOG.MD ===

[full content]

# === AGENT_PROMPT.MD ===

[full content, customized from template]

# === END_SESSION.MD ===

[full content, customized from template]
```
