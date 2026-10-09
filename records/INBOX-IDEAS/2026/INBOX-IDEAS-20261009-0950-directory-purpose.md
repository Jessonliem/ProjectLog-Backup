# Inbox Ideas — purpose and operating intent

- Record-ID: INBOX-IDEAS-20261009-0950-directory-purpose
- Date: 2026-10-09 09:50
- Project-ID: INBOX-IDEAS
- Type: Document
- Keywords: idea management, newsletter writing, AI x Engineering Newsletter, thought seeds, content pipeline, engineering automation
- People: Not provided
- Source: User dictation, 2026-10-09
- Status: Recorded
- Updated: 2026-10-09 09:51 — idea lifecycle decided (used / not used, no closing state); see INBOX-IDEAS-20261009-0951-idea-lifecycle
- Updated: 2026-10-09 09:53 — newsletter split into its own project (AIX-NEWS) and moved to the workspace root; see INBOX-IDEAS-20261009-0953-newsletter-spun-off

## Summary

`C:/EnergySim-Workspace/Inbox Ideas` is the personal capture-and-development workspace where
scattered ideas and the "AI x Engineering" newsletter are collected, kept, and grown. The
intent is to have one place that holds every raw idea and every piece of newsletter writing,
with this project log acting as the managed layer over it so that nothing is lost and each item
can be searched, tracked, and developed.

At the time of this record the folder mixed two kinds of material (the newsletter was later split
out into its own project on 2026-10-09):

- Flat, standalone idea notes at the top level — tool and script concepts (Excel/parameter
  extraction, gbXML window adjustment/migration, LPD and infiltration checks, SimParametric DSL,
  SimVisAssign helpers, sensitivity analysis), workflow notes, and a LinkedIn post draft.
- The `AI x Engineering Newsletter` subfolder — the working area for the newsletter, containing
  numbered issues (#0–#4), outlines, "thought seeds", a `Next stage` planning area with a master
  architecture / series map, images, and its own Git repository.

The project log is being established now (2026-10-09) as the index for all of this: ideas and
newsletter activity are to be captured as records under project ID `INBOX-IDEAS`.

## Decision, assumption, or concern

Decision: register `Inbox Ideas` as a single managed project (`INBOX-IDEAS`) whose `record_dir`
is `C:/EnergySim-Workspace/Inbox Ideas/ProjectLog`, and treat both the idea notes and the
newsletter as content flowing through this one log.

Concern: the material is currently a flat pile of files with no status or lifecycle. Without a
log, ideas and newsletter fragments are hard to retrieve, prioritise, or carry forward. The log
is intended to give each item a citable record and a status.

Open question: whether the newsletter should eventually be split into its own dedicated project
(and log) or stay a sub-area of `INBOX-IDEAS`. — Resolved 2026-10-09: split into its own project
`AIX-NEWS` (see INBOX-IDEAS-20261009-0953-newsletter-spun-off).

## Basis and evidence

- Directory listing of `C:/EnergySim-Workspace/Inbox Ideas`: ~18 top-level idea/notes files, an
  `OpenCodeStart.bat`, and the `AI x Engineering Newsletter` subfolder.
- Newsletter folder structure observed: issues `AI x Engineering #0–#4`, `Thought Seeds 01–08`,
  `Next stage/` with `00 - Master Architecture & Series Map` and issue outlines for #04–#10,
  plus `Archive/` and `Picture/`, and a `.git` repository.
- Stated user intent, 2026-10-09: manage all ideas and the newsletter writing here.

## Follow-up

- ~~Define how an "idea" graduates through stages (captured → developed → produced/archived).~~
  Resolved 2026-10-09: ideas have only "used" / "not used" states (see
  INBOX-IDEAS-20261009-0951-idea-lifecycle).
- Decide how newsletter issues map to records (one record per issue? per thought seed?).
- ~~Decide whether the newsletter becomes its own project/log later.~~ Resolved 2026-10-09:
  newsletter is now its own project `AIX-NEWS`.
- Capture each existing idea and newsletter issue as an individual record over time.
