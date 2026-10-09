# Idea lifecycle — used vs. not used (no closing state)

- Record-ID: INBOX-IDEAS-20261009-0951-idea-lifecycle
- Date: 2026-10-09 09:51
- Project-ID: INBOX-IDEAS
- Type: Decision
- Keywords: idea lifecycle, status model, used, not used, idea reuse, utilization tracking
- People: Not provided
- Source: User dictation, 2026-10-09 (ref: INBOX-IDEAS-20261009-0950-directory-purpose)
- Status: Recorded

## Summary

Defines the state model for ideas kept in `Inbox Ideas`. An idea is never "closed". It has only
two states:

1. **Not used** — captured but not yet put to work.
2. **Used** — has been put to work at least once.

A used idea is not retired: it may be used again in the future. So the log does not need a
closing/archived state; it only needs to record that an idea was used and **where** it was used.

## Decision, assumption, or concern

Decision: track ideas by utilization only — whether an idea has been used, and where. Do not
introduce a "closed" or "done" status for ideas. Because a used idea can be reused, its record
stays live and the "where used" log can grow across multiple uses.

## Basis and evidence

- User statement, 2026-10-09: ideas have only "used" and "not used" states; a used idea may be
  used again, so it is enough to record that it was used and where.

## Follow-up

- Decide how "where used" is captured (e.g. link to a produced record, newsletter issue number,
  or another project).
- Apply this model to existing idea notes when they are captured as records.
