# Newsletter split into its own project (AIX-NEWS)

- Record-ID: INBOX-IDEAS-20261009-0953-newsletter-spun-off
- Date: 2026-10-09 09:53
- Project-ID: INBOX-IDEAS
- Type: Decision
- Keywords: newsletter spin-off, project split, AI x Engineering Newsletter, workspace restructure
- People: Not provided
- Source: User dictation 2026-10-09 (ref: INBOX-IDEAS-20261009-0950-directory-purpose)
- Status: Recorded

## Summary

The "AI × Engineering Newsletter" is separated from `Inbox Ideas` and made its own project.

- New project ID: `AIX-NEWS`, name "AI x Engineering Newsletter".
- The folder was moved from `C:/EnergySim-Workspace/Inbox Ideas/AI x Engineering Newsletter`
  to the workspace root: `C:/EnergySim-Workspace/AI x Engineering Newsletter`.
- The newsletter now has its own log at `.../AI x Engineering Newsletter/ProjectLog`
  (see AIX-NEWS-20261009-0953-purpose-and-architecture).
- `Inbox Ideas` (`INBOX-IDEAS`) now holds only the loose idea notes; the newsletter aliases
  ("AI x Engineering Newsletter", "Newsletter") were removed from this project.

## Decision, assumption, or concern

Decision: the newsletter is a standalone project with its own log; `Inbox Ideas` keeps the raw
idea notes. This resolves the open question recorded in the directory-purpose record.

## Basis and evidence

- User statement, 2026-10-09: the newsletter is in fact already a separate project; make it
  standalone and move it to the workspace root.
- Folder move completed to `C:/EnergySim-Workspace/AI x Engineering Newsletter`.
- `projects.json` updated: `AIX-NEWS` registered; newsletter aliases removed from `INBOX-IDEAS`.

## Follow-up

- All future newsletter work is logged under `AIX-NEWS`, not here.
