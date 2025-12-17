# End Session Prompt

Use this prompt to cleanly close out a development session before clearing context.

---

## Prompt

Copy and paste this into your AI coding tool at the end of your session:

```
End this session. Before stopping:

1. **Update phase_plan.md:**
   - Mark completed stories as [DONE]
   - Update acceptance criteria checkboxes to reflect actual state
   - Do not modify story text or criteria wording

2. **Update impl_log.md:**
   - Update "Last Updated" date
   - Update "Current Story" to the next [TODO] story
   - Add an implementation entry for today's work:
     - Date
     - Story ID and title
     - Files created (full paths)
     - Files modified (full paths with brief description)
     - Patterns followed (cite existing code referenced)
     - Key decisions made
     - Any notes for the next session

3. **Provide a handoff summary:**
   - What was completed this session
   - Current state of the feature
   - What's next (next TODO story)
   - Any blockers, open questions, or risks

Do not start new work. Just save state and summarize.
```

---

## What This Does

- **Persists progress** — The impl_log becomes memory across sessions
- **Updates status** — Phase plan reflects true state
- **Clean handoff** — Next session knows exactly where to pick up

---

## Verification Checklist

Before ending, verify:

- [ ] Story marked `[DONE]` in phase_plan.md (if completed)
- [ ] Implementation entry added to impl_log.md
- [ ] Current Story updated in impl_log.md
- [ ] Existing tests still pass
- [ ] No uncommitted work that should be noted

---

## Phase Completion

If this was the last story in a phase:

- [ ] Add phase completion note to impl_log.md
- [ ] Update Current Phase in impl_log.md
- [ ] Summarize what the phase delivered
- [ ] Ask before proceeding to next phase

---

## Reminder

**The next session has no memory of this one.**

Everything the next session needs must be in the documentation:
- What was built → impl_log.md implementation entries
- What's next → impl_log.md current story + phase_plan.md
- How things work → existing code + feature_overview.md

If you didn't write it down, it didn't happen.
