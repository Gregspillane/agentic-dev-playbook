# End Development Session

Checklist before ending the session.

---

## 1. Documentation Updates

Verify these are complete:

- [ ] `docs/phase_plan.md` — Story marked `[DONE]`
- [ ] `docs/impl_log.md` — Implementation History entry added
- [ ] `docs/impl_log.md` — Current State updated (Next Story)

---

## 2. Conventions Check

**If you established new patterns** (folders, components, hooks, naming conventions, UI patterns):

→ Add them to the **Codebase Conventions** section in `impl_log.md`

### Validation Question

Ask yourself:

> "If the next session ONLY reads Codebase Conventions, will they know about the patterns I created?"

**If no → update Conventions before ending.**

This is the most common gap. Patterns buried in Implementation History entries get missed by future sessions. Patterns in Conventions are always found.

---

## 3. Confirm

Provide a summary:

```
Session complete.

Story: [X-X — Title] marked DONE
Next story: [X-X — Title]
Conventions updated: [yes/no]
```

---

## 4. Phase Completion (If Applicable)

If this was the last story in a phase:

- [ ] Add Phase Completion Summary to `impl_log.md`
- [ ] Update Current State to next phase
- [ ] Inform user and ask before proceeding to next phase

---

## Reminder

The next session has **no memory** of this one.

Everything the next session needs must be in the documentation. If you didn't write it down, it didn't happen.
