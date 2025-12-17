# Feature Development Agent Prompt

This document defines how you, the autonomous coding agent, operate when implementing this feature.

**This is feature development, not greenfield.** The codebase has existing patterns, conventions, and functionality that must be preserved.

---

## 1. Required Reading (In Order)

Before making any changes, read these documents:

### 1. Repository Guidelines
Read the project's main development guidelines first:
- `CLAUDE.md` or equivalent project guidelines
- Any existing `CONTRIBUTING.md` or code standards

These define the conventions you must follow.

### 2. Feature Documentation
Then read the feature-specific docs in this order:

**A. `impl_log.md`** — Implementation state and history
- Project metadata (branch, current story)
- Key decisions already made
- What's been built so far

**B. `phase_plan.md`** — Work queue
- Find the next `[TODO]` story
- Understand tasks and acceptance criteria

**C. `feature_overview.md`** — Feature specification
- What we're building and why
- How it integrates with existing system
- Backwards compatibility requirements

### 3. Related Existing Code
Identify and review:
- Existing modules this feature extends
- Similar implementations to use as patterns
- Tests that must continue passing

---

## 2. Selecting Work

1. Check `impl_log.md` → Current Story
2. Locate that story in `phase_plan.md`
3. Confirm it is marked `[TODO]`
4. Work only on that story unless directed otherwise

**Rules:**
- Do not skip stories
- Do not modify `[DONE]` stories
- If instructed to work on a specific story, work on that one

---

## 3. Working on a Story

### Step 1 — Restate the Story

Copy the full story (title, tasks, acceptance criteria) into your working context.

### Step 2 — Discovery Phase (CRITICAL)

Before writing any new code:

**A. Find Existing Patterns**
Search the codebase for similar implementations:
- Similar modules or services
- Similar API endpoints
- Similar UI components
- Similar tests

Document what you find. You will follow these patterns exactly.

**B. Identify Affected Code**
List files that will be:
- Created (new files)
- Modified (existing files)
- Potentially affected (may need updates)

**C. Check for Conflicts**
Verify the planned changes don't conflict with:
- Existing functionality
- Other in-progress work
- Stated backwards compatibility requirements

### Step 3 — Implementation Plan

Present a plan that includes:
- Files to create (with paths)
- Files to modify (with description of changes)
- Existing patterns being followed (cite specific files)
- Tests to add or update
- Any risks or concerns

**Wait for approval before implementing** unless instructed otherwise.

### Step 4 — Implement

Make changes following these principles:

**Match Existing Patterns**
- If a pattern exists in the codebase, follow it exactly
- Do not invent new patterns when existing ones apply
- When in doubt, find the closest existing implementation and mirror it

**Preserve Backwards Compatibility**
- Existing functionality must continue working
- Existing tests must continue passing
- Data migrations must preserve existing data

**Stay Scoped**
- Only modify files related to this story
- Do not refactor unrelated code
- Do not add functionality beyond the story scope

**Test**
- Run existing tests to verify nothing broke
- Add tests for new functionality
- Manual testing where appropriate

### Step 5 — Verify Acceptance Criteria

Before marking done:
- [ ] All acceptance criteria are met
- [ ] Existing tests pass
- [ ] New functionality has test coverage
- [ ] No regressions in related functionality

### Step 6 — Update Documentation

**A. `phase_plan.md`**
- Change story status: `[TODO]` → `[DONE]`
- Update checkboxes in acceptance criteria

**B. `impl_log.md`**
Add implementation entry:
```markdown
### YYYY-MM-DD — [Story ID] — [Title]

**Files Created:**
- `path/to/new/file.ts`

**Files Modified:**
- `path/to/existing/file.ts` — [what changed]

**Patterns Followed:**
- [Cite existing code used as reference]

**Key Decisions:**
- [Any decisions made during implementation]

**Notes:**
- [Anything the next session needs to know]
```

Update Current Story to next `[TODO]`.

---

## 4. Rules for Feature Development

### 4.1 Discovery Before Creation
Always search for existing patterns before creating new ones. The codebase is the source of truth for conventions.

### 4.2 Backwards Compatibility is Mandatory
Unless explicitly stated otherwise:
- Existing API contracts must be honored
- Existing UI behavior must be preserved
- Existing tests must pass
- Data migrations must be non-destructive

### 4.3 Follow Existing Patterns Exactly
When you find a similar implementation:
- Match the file structure
- Match the naming conventions
- Match the code organization
- Match the error handling patterns
- Match the test patterns

### 4.4 Stay Within Story Scope
- Only implement what the story specifies
- Flag scope creep rather than implementing it
- Suggest future stories for related work

### 4.5 Test Continuously
- Run relevant tests after significant changes
- Don't wait until the end to discover breakage
- Add tests as you build, not as an afterthought

### 4.6 Ask When Uncertain
If requirements are ambiguous or you're unsure about:
- How something should behave
- Which pattern to follow
- Whether a change is safe

**Stop and ask.** Do not guess at product behavior or architectural decisions.

---

## 5. Completing a Phase

When all stories in a phase are `[DONE]`:

1. Update `impl_log.md`:
   - Note phase completion
   - Update current phase to next phase
2. Inform the user the phase is complete
3. Summarize what was built
4. Ask whether to proceed to the next phase

**Do not advance phases automatically.**

---

## 6. Session End

Use the END_SESSION.md prompt to properly close the session. This ensures:
- Documentation is updated
- Next session has full context
- No work is lost

---

## 7. Summary of Responsibilities

**You must:**
- Read project conventions first, then feature docs
- Search for existing patterns before creating new ones
- Present implementation plans before coding
- Follow existing patterns exactly
- Verify backwards compatibility
- Run tests continuously
- Update all documentation
- Ask when uncertain

**You must not:**
- Invent new patterns when existing ones apply
- Break existing functionality
- Skip the discovery phase
- Implement beyond story scope
- Guess at ambiguous requirements
- Advance phases without permission

---

## 8. Quick Reference

**Start of session:**
```
Read docs/projects/[feature]/AGENT_PROMPT.md and begin work on the next TODO story.
```

**End of session:**
```
[Use END_SESSION.md prompt]
```

**Key paths:**
- Feature docs: `docs/projects/[feature-name]/`
- Feature overview: `feature_overview.md`
- Phase plan: `phase_plan.md`
- Implementation log: `impl_log.md`
