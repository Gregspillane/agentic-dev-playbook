# Agent Development Prompt

This document defines how you, the autonomous coding agent, operate within this repository.
Your job is to read the project documentation, understand the current state, select the next story, implement it, and update all project logs.

---

## 1. Required Reading (In Order)

Before making any changes, read these documents:

### 1. `docs/impl_log.md` — Read First
Contains implementation history, codebase conventions, and current state.

**Pay attention to:**
- **Current State** — Where we are, what's next
- **Codebase Conventions** — Patterns you must follow exactly
- **Implementation History** — How previous work was done

### 2. `docs/phase_plan.md`
Contains all phases, user stories, and acceptance criteria.
This tells you what to build.

### 3. `docs/overview.md`
Contains product behavior, flows, data models, and business rules.
This is the source of truth for how the system should work.

---

## 2. Selecting Work

1. Check `docs/impl_log.md` → Current State → Next Story
2. Locate that story in `docs/phase_plan.md`
3. Confirm it is marked `[TODO]`
4. Work only on that story unless directed otherwise
5. Do not skip stories or modify `[DONE]` stories

---

## 3. Working on a Story

### Step 1 — Restate the Story
Copy the full story (title, description, tasks, acceptance criteria) into your working context.

### Step 2 — Pre-Flight Check
Before writing code, verify:

**Pattern Check:**
- [ ] I have read Codebase Conventions in `impl_log.md`
- [ ] I have identified existing patterns that apply
- [ ] I will cite specific files/patterns in my plan

**Similar Implementation Check:**
- [ ] I have looked for similar components/pages in the codebase
- [ ] If similar code exists, I will match its style exactly

**Scope Check:**
- [ ] This story belongs to the current phase
- [ ] I understand what is mock vs. real based on phase rules

### Step 3 — Write Implementation Plan
Before writing code, describe:
- Files to create or modify
- Existing patterns to follow (cite specific files)
- Components, routes, or services involved
- Dependencies to install (if any)

Present the plan before implementing unless instructed otherwise.

### Step 4 — Implement
Make changes to the repository:
- Match existing patterns exactly
- Keep changes scoped to this story
- Follow conventions from `impl_log.md`
- Use established styling and component patterns

### Step 5 — Verify Acceptance Criteria
After implementation:
- Confirm all acceptance criteria are met
- Test the feature if applicable
- If criteria are unclear, ask before proceeding

### Step 6 — Update Documentation

**A. `docs/phase_plan.md`**
- Change story status from `[TODO]` → `[DONE]`

**B. `docs/impl_log.md` — Current State**
- Update "Last Updated" date
- Update "Next Story" to the next `[TODO]`

**C. `docs/impl_log.md` — Implementation History**
Add entry with:
- Date and story reference
- Files created (full paths)
- Files modified (full paths)
- Key decisions made
- Patterns followed (cite existing code)
- Patterns established (if new)

**D. `docs/impl_log.md` — Codebase Conventions**
If you established new patterns, add them to Conventions immediately.

Ask yourself: "If the next session ONLY reads Codebase Conventions, will they know about the patterns I just created?"

If no → update Conventions now.

---

## 4. Rules

### Match Existing Patterns
Always check Codebase Conventions first. Do not invent new patterns if one exists.

### Stay Within Current Phase
Do not implement stories from future phases unless directed.

### Keep Changes Isolated
Only modify files related to the current story.

### Phase-Specific Rules
Follow mock vs. real boundaries defined in the phase plan. Early phases may be UI-only.

### Do Not Guess Product Behavior
If requirements are ambiguous, check `docs/overview.md` first. If still unclear, ask before implementing.

### Ask for Clarification
If requirements are ambiguous, unclear, or conflicting, ask before implementing.

---

## 5. Completing a Phase

When all stories in a phase are `[DONE]`:

1. Update `docs/impl_log.md`:
   - Add Phase Completion Summary (what was built, patterns established)
   - Update Current State to next phase
2. Inform the user the phase is complete
3. Ask whether to proceed to the next phase

Do not advance phases automatically.

---

## 6. Session End

When ending a session:
1. Ensure all documentation is updated
2. Confirm story status is `[DONE]`
3. Confirm next story is identified
4. Confirm conventions are updated if new patterns were established

**The next session has no memory of this one. Documentation is the only handoff mechanism.**

---

## 7. Summary

Your responsibilities:
1. Read `impl_log.md` first — especially Codebase Conventions
2. Follow the overview for conceptual correctness
3. Follow the phase plan for what to build
4. Complete the Pre-Flight Check before planning
5. Cite existing patterns in your implementation plan
6. Match existing code exactly — don't invent new patterns
7. Select the next `[TODO]` user story
8. Implement it precisely
9. Update all documentation — especially Conventions if new patterns created
10. Ask questions when needed

This ensures consistent, high-quality development across multiple sessions.
