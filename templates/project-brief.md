# Project Brief Template

Copy this template and fill it out for your project. This brief becomes the input for generating your overview, phase plan, and implementation log.

Sections marked **(Required)** must be completed. Sections marked **(Optional)** can be included if relevant to your project.

---

# Project Brief: [Project Name]

## 1. Project Identity (Required)

**Name:** [Project name]

**One-liner:** [Single sentence describing what this is]

**Problem Statement:** [What problem does this solve? For whom? Why does it matter?]

---

## 2. Actors & Personas (Required)

List each distinct user type that interacts with the system.

### [Actor Name]
- **Role:** [What they do / who they are]
- **Goals:** [What they're trying to accomplish]
- **Key Actions:** [Primary things they do in the system]

### [Actor Name]
- **Role:** 
- **Goals:** 
- **Key Actions:** 

[Add more actors as needed]

---

## 3. Core Capabilities (Required)

What does the system do? List the major functional areas.

- **[Capability]:** [Brief description of what this enables]
- **[Capability]:** [Brief description]
- **[Capability]:** [Brief description]

[Add more as needed]

---

## 4. Key Flows (Required)

Describe the most important user journeys. These become the backbone of the phase plan. Include 2-5 core flows that represent the primary paths through your system.

### [Flow Name]
```
Step 1 → Step 2 → Step 3 → Step 4
```
**Notes:** [Important details, branching logic, error cases, edge cases]

### [Flow Name]
```
Step 1 → Step 2 → ...
```
**Notes:** 

[Add more flows as needed]

---

## 5. Technical Stack (Required)

Define the technology choices for this project.

- **Framework:** [e.g., Next.js 14+, Rails 7, Django]
- **Language:** [e.g., TypeScript (strict mode), Python 3.11+]
- **Database:** [e.g., PostgreSQL, MongoDB, SQLite]
- **Styling:** [e.g., Tailwind CSS + shadcn/ui, styled-components]
- **Auth:** [e.g., Passkeys, NextAuth, Clerk, custom JWT]
- **Hosting:** [e.g., Vercel, AWS, fly.io, self-hosted]

---

## 6. Integrations (If Applicable)

Third-party services the system must integrate with.

- **[Service]:** [Purpose / what it's used for]
- **[Service]:** [Purpose]

[Remove this section if no integrations]

---

## 7. Scope Definition (Required)

### In Scope (v1)
What will be built in this version:

- [Feature or capability]
- [Feature or capability]
- [Feature or capability]

### Out of Scope (v1)
What is explicitly NOT being built (and optionally why):

- [Feature] — [Reason if relevant]
- [Feature] — [Reason]
- [Feature]

---

## 8. Phasing Strategy (Required)

How should the work be organized?

**Approach:** [Describe your phasing strategy]

Examples:
- "UI-first: Build all UI shells with mock data in early phases, implement backend in later phases"
- "Vertical slices: Each phase delivers a complete feature end-to-end"
- "Foundation first: Infrastructure and auth in Phase 1, features in subsequent phases"

**Mock vs. Real:** [When does mock data get replaced with real implementation?]

**Phase Boundaries (Optional):** [If you have specific phase cuts in mind, list them here]

---

## 9. Conventions & Patterns (Optional)

If you have existing conventions or specific patterns you want enforced, document them here. These will be pre-populated in the implementation log.

### File Organization
[Where should different types of files live?]

### Naming Conventions
[Any specific naming rules?]

### Code Patterns
[Specific patterns you want followed?]

---

## 10. Data Model (Optional)

Sketch of key entities and relationships, if known.

- **[Entity]:** [Key fields, purpose, relationships]
- **[Entity]:** [Key fields, purpose]

[Leave blank if you want the overview generation to propose a data model]

---

## 11. Security Requirements (Optional)

Non-negotiable security constraints.

- [Requirement]
- [Requirement]

---

## 12. Risks & Assumptions (Optional)

### Assumptions
- [Assumption about users, integrations, technical constraints]

### Known Risks
- [Risk]: [Mitigation strategy, if known]

---

## 13. Success Criteria (Optional)

How do we know this project is complete and successful?

- [ ] [Criterion]
- [ ] [Criterion]

---

## Notes for Generation

[Any additional context that would help generate better documentation. This section is for the human filling out the brief to communicate intent that doesn't fit elsewhere.]
