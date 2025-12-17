# Feature Brief Template

Copy this template and fill it out for your feature. This brief becomes the input for generating your feature documentation.

Sections marked **(Required)** must be completed. Sections marked **(Optional)** enhance the generated output.

---

# Feature Brief: [Feature Name]

## 1. Feature Identity (Required)

**Name:** [Feature name]

**Project:** [Parent project/repository name]

**Branch:** [Feature branch name, e.g., `feature/multi-webhook` or `greg-RND-12014`]

**One-liner:** [Single sentence describing what this feature adds]

**Problem Statement:** [What problem does this solve? Who asked for it? Why now?]

---

## 2. Current State (Required)

Describe the relevant parts of the existing system that this feature touches or extends.

### Existing Components
- **[Component/Module]:** [Brief description of what exists today]
- **[Component/Module]:** [Brief description]

### Current Limitations
- [What can't the system do today that this feature addresses?]
- [What workarounds exist, if any?]

### Related Code Locations
- `path/to/relevant/code` — [What it does]
- `path/to/relevant/code` — [What it does]

---

## 3. Proposed Solution (Required)

### What We're Building
[High-level description of the solution]

### Core Concepts
Define any new entities, models, or abstractions this feature introduces:

- **[Concept]:** [Definition and purpose]
- **[Concept]:** [Definition and purpose]

### How It Fits
[How does this integrate with existing architecture? What existing patterns does it follow?]

---

## 4. User Stories (Required)

Describe the key user-facing capabilities. These become the backbone of the phase plan.

### [Capability Name]
**As a** [actor], **I need** [capability] **so that** [benefit].

**Flow:**
```
Step 1 → Step 2 → Step 3 → Outcome
```

**Notes:** [Important details, edge cases, error handling]

### [Capability Name]
**As a** [actor], **I need** [capability] **so that** [benefit].

**Flow:**
```
Step 1 → Step 2 → ...
```

**Notes:**

[Add more capabilities as needed]

---

## 5. Technical Approach (Required)

### Data Model Changes
- **New entities:** [List any new database tables/models]
- **Modified entities:** [List changes to existing models]
- **Migrations required:** [Yes/No, brief description]

### API Changes
- **New endpoints:** [List new API routes]
- **Modified endpoints:** [List changes to existing routes]
- **Breaking changes:** [Yes/No, details if yes]

### UI Changes
- **New pages/views:** [List]
- **Modified pages/views:** [List]
- **New components:** [List]

---

## 6. Scope Definition (Required)

### In Scope
What will be built in this feature:

- [Specific capability or component]
- [Specific capability or component]
- [Specific capability or component]

### Out of Scope
What is explicitly NOT being built (may be future work):

- [Capability] — [Reason or "future consideration"]
- [Capability] — [Reason]

### Dependencies
- [Does this depend on other features or changes?]
- [Are there external dependencies?]

---

## 7. Backwards Compatibility (Required)

### Existing Behavior Preserved
- [What must continue working exactly as before?]
- [What data must be migrated?]

### Migration Strategy
[How do existing users/data transition to the new system?]

### Rollback Plan
[Can this be rolled back? What's the strategy?]

---

## 8. Phasing Strategy (Required)

**Approach:** [How should the work be organized?]

Examples:
- "Schema first, then API, then UI"
- "Vertical slice: complete one capability end-to-end, then the next"
- "API first so other teams can integrate, UI follows"

**Suggested Phases:**
- **Phase 1:** [Theme — what gets built]
- **Phase 2:** [Theme — what gets built]
- **Phase 3:** [Theme — what gets built]

**Story Count Estimate:** [Roughly how many stories? 3-8 for medium, 5-15 for large]

---

## 9. Acceptance Criteria (Required)

How do we know this feature is complete?

- [ ] [Testable criterion]
- [ ] [Testable criterion]
- [ ] [Testable criterion]
- [ ] Existing tests pass
- [ ] New functionality has test coverage
- [ ] Documentation updated

---

## 10. Risks & Open Questions (Optional)

### Known Risks
- [Risk]: [Mitigation]

### Open Questions
- [Question that needs resolution during implementation]

---

## 11. References (Optional)

- [Link to related documentation]
- [Link to design mockups]
- [Link to relevant prior art or research]
- [Commit or PR references for related work]

---

## Notes for Generation

[Any additional context for the AI generating the documentation. Clarifications, preferences, or intent that doesn't fit elsewhere.]
