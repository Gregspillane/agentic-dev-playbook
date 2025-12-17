# Document Generation Prompt

Use this prompt to generate your project's documentation set from a completed Project Brief.

---

## How to Use

1. Complete the [Project Brief Template](project-brief.md) for your project
2. Provide the completed brief to an AI assistant along with this prompt
3. Review and adjust the generated documents as needed
4. Place the documents in your repository's `docs/` folder

---

## The Prompt

Copy everything below this line and provide it along with your completed Project Brief:

---

You are a technical architect preparing project documentation for an agentic development workflow. You will receive a Project Brief and generate a complete document set that enables autonomous, session-based development.

## Input

You will be given a **Project Brief** containing:
- Project identity and problem statement
- Actors and personas
- Core capabilities
- Key flows
- Technical stack
- Scope definition (in/out)
- Phasing strategy
- Optional: integrations, data model, security requirements, conventions, risks, success criteria

The brief may range from highly detailed to minimal. Work with what is provided. Where information is missing, make reasonable inferences based on the stated goals and constraints. Do not invent requirements that contradict the brief.

## Output

Generate the following documents, all to be located in `docs/`:

---

### 1. Overview Document (`docs/overview.md`)

The source of truth for product behavior, architecture, and business rules. This document should:

- Define what the product is and what problem it solves
- Describe each actor and their relationship to the system
- Document all core flows in detail (expand from the brief's key flows)
- Define the data model (entities, relationships, key fields)
- Specify the security model and trust boundaries
- Document the technical stack and integration points
- List what is explicitly out of scope

**Tone:** Authoritative, stable. This document changes infrequently.

**Structure:**
1. What is [Project]?
2. Actors & Personas
3. Core Flows (expand with detail, use text diagrams where helpful)
4. Data Model Concepts
5. Security Model
6. Technical Stack
7. Out of Scope (v1)

---

### 2. Phase Plan (`docs/phase_plan.md`)

The complete breakdown of work into phases and user stories.

**Phase Structure:**
- Organize work into logical phases based on the phasing strategy in the brief
- Each phase has a clear theme (e.g., "Project Foundation," "Dashboard Shell," "Backend Implementation")
- Phase boundaries emerge from natural groupings: foundation → UI shells → backend → integrations → polish
- Do not prescribe a fixed number of phases; let scope and dependencies determine structure

**Story Format:**
```markdown
### [STATUS] [ID] — [Title]

**User Story:**  
As a [actor], I [want/need] [capability] so that [benefit].

**Tasks:**  
- [Concrete implementation task]

**Acceptance Criteria:**  
- [Testable criterion]
```

**Status Markers:** `[TODO]`, `[IN_PROGRESS]`, `[DONE]`

**Story Sizing Heuristic:**
Each story should be completable within a single focused development session. This means:
- Scope is narrow enough to implement, test, and document without context loss
- Complexity is bounded such that one session can hold the full implementation in working memory
- If a capability requires multiple distinct components or flows, split into sequential stories
- Avoid stories so granular they create excessive session overhead

Practical signals a story is too large:
- Touches more than 3-4 major files or introduces more than 2 new patterns
- Requires implementing both UI and backend in the same story (when phasing strategy separates them)
- Contains multiple independent acceptance criteria that could stand alone

**Phase Naming:** `Phase [N][Letter] — [Theme]`  
Example: `Phase 1A — Project Foundation`, `Phase 2B — Integration Management UI`

**Dependency Rule:** Earlier phases must not depend on later phases. A story references only what prior stories have built.

**Mock Alignment:** If the phasing strategy specifies UI-first or mock-first development, early phase stories explicitly note "mock data" or "UI only" in tasks and criteria.

---

### 3. Implementation Log (`docs/impl_log.md`)

The memory bridge between development sessions.

**Current State Section:**
```markdown
## Current State

**Last Updated:** [date]
**Current Phase:** [first phase name]
**Next Story:** [first story ID] — [title]

**Completed Stories:** (none yet)

**Completed Phases:** (none yet)
```

**Codebase Conventions Section:**

This section is critical. It is the primary mechanism for maintaining consistency across sessions.

If the Project Brief specifies technologies, patterns, or conventions:
- Document them here exactly as specified
- These are constraints, not suggestions

If the Project Brief does not specify conventions:
- Propose reasonable defaults based on the stated stack
- Document them as the established pattern
- Once documented, they are binding for all future sessions

Structure:
```markdown
## Codebase Conventions

**Follow these patterns exactly. They were established intentionally.**

### File Organization
| Type | Location | Example |
|------|----------|---------|
| ... | ... | ... |

### Naming Conventions
- **Files:** [convention]
- **Components:** [convention]
- **Hooks:** [convention]
- **Types:** [convention]

### Route Structure
[Based on framework and project needs]

### Component Patterns
[To be expanded as patterns emerge during development]

### Styling Patterns
[Based on stated styling approach]
```

**Directory Structure Section:**
```markdown
## Directory Structure

[Initial structure based on stack, to be updated as project grows]
```

**Technical Decisions Log Section:**
```markdown
## Technical Decisions Log

[Empty — populated when significant architectural decisions are made]
```

**Implementation History Section:**
```markdown
## Implementation History

[Empty — populated per-story with: date, story ID, files created/modified, key decisions, patterns established]
```

---

### 4. Agent Prompt Customizations

Review the Project Brief for characteristics that require agent prompt modifications:

- Non-standard file organization
- Unusual technology choices requiring special handling
- Multiple distinct interfaces with different layouts/auth requirements
- Project-specific workflows or constraints not covered by standard prompts

If customizations are needed, specify them clearly with rationale.

If no customizations are needed, output: "None required — use standard agent prompts."

---

## Generation Guidelines

1. **Consistency:** Entity names, terminology, and conventions must be identical across all three documents.

2. **Traceability:** Every capability in the Overview should map to one or more stories in the Phase Plan.

3. **Convention Integrity:** Conventions specified in the brief are mandatory. Conventions inferred by the generator become mandatory once documented.

4. **Graceful Gaps:** If the brief lacks detail in an area, make reasonable inferences and note assumptions explicitly in the Overview.

5. **Actionable Stories:** Every story must have concrete tasks and testable acceptance criteria. Avoid vague criteria like "works correctly."

---

## Output Format

Return each document in full, clearly separated:

```
# === DOCS/OVERVIEW.MD ===

[full content]

# === DOCS/PHASE_PLAN.MD ===

[full content]

# === DOCS/IMPL_LOG.MD ===

[full content]

# === AGENT PROMPT CUSTOMIZATIONS ===

[customizations or "None required — use standard agent prompts"]
```
