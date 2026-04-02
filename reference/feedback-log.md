# Feedback Log

Accepted items from external feedback, waiting for implementation.

**Friction log** = things you noticed. **Feedback log** = things others noticed that you agreed with. Both feed into `/maintain`.

---

## How to Use This Log

**When items are added:** After triage — someone provides feedback, the maintainer evaluates it, and accepted items land here.

**When resolved:** During `/maintain` sessions. Update the Status field with date and description. Move resolved entries to `feedback-log-archive.md`.

## Entry Format

```
### YYYY-MM-DD: [Brief title]

- **Source:** Where the feedback came from
- **Verdict:** Accept | Adapt | Defer | Decline
- **Status:** Pending | Resolved (YYYY-MM-DD — what was done)
- **What to do:** The actionable change
- **Why it was accepted:** Why this feedback is right for this project
- **Resolved:** [Date and description when completed]
```

Not all fields are required.

## Entries

### 2026-03-30: Permission behavior test — symlinks vs. direct sibling reads

- **Source:** [mightytech/nla-office-hours#1](https://github.com/mightytech/nla-office-hours/issues/1)
- **Verdict:** Accept
- **Status:** Pending
- **What to do:** Run the test protocol (check settings, test direct reads, test symlink reads, clean up) and report results back to the framework via `/write-letter`.
- **Why it was accepted:** Low-effort test that contributes to framework infrastructure benefiting all NLAs. Directly relevant — this project experiences the permission friction being investigated.
