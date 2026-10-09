# Idea: Extractor for envelope areas by construction and space type

- Record-ID: INBOX-IDEAS-20261009-0956-envelope-area-extraction
- Date: 2026-10-09 09:56
- Project-ID: INBOX-IDEAS
- Type: Idea
- Keywords: opaque envelope extraction, construction type, space type, energy model report, HTML parsing, SQL, window area, area grouping, python script
- People: Not provided
- Source: User dictation, 2026-10-09
- Status: Recorded
- Updated: 2026-10-09 10:04 — implemented as skill "envelope-area-extractor" (C:\EnergySim-Workspace\MySkills\envelope-area-extractor); space type resolved from a user-supplied zone→space-type mapping CSV
- Utilization: Used — built as skill "envelope-area-extractor"; reads eplustbl.htm / eplusout.sql, groups by construction × space type

## Summary

Idea for a tool that automatically extracts **opaque envelope areas** from an energy modeling
report, whether the source is HTML output or a SQL database. The extracted areas are grouped
**by construction**, and within each construction **by space type**. Window areas would be
extracted and integrated in the same way.

The value is fast, flexible area selection. Because each surface carries both its construction
and its space type, it becomes easy to extract or exclude specific slices — for example, select
all exterior wall area that belongs to elevator or stair spaces under a particular concrete
construction, versus other walls that may be steel frame or wood frame. Today this is done by
hand in Excel; the tool would make it routine.

Implementation preference: package it as a **Skill plus a set of Python scripts** that do the
extraction and can be called on demand, so it is convenient to use repeatedly.

## Decision, assumption, or concern

Assumption: the model report retains, per surface, both the construction assignment and the
space type, so the two-level grouping (construction → space type) is derivable from the source.

Concern: report formats vary (HTML vs. SQL, different tool versions), so the parser must be
robust to schema/format differences across projects.

## Basis and evidence

- User statement, 2026-10-09: desire to automatically pull opaque (and window) envelope areas
  from HTML or SQL energy-model reports, grouped by construction then by space type, replacing
  manual Excel work; preferred packaging is a Skill plus Python scripts.

## Follow-up

- ~~Prototype extraction from one sample report (HTML and/or SQL) and confirm the available fields.~~
  Done 2026-10-09: verified on `...\Proposed V4\eplustbl.htm` and `eplusout.sql`.
- ~~Define the grouping keys and output format (e.g. construction × space type area table).~~
  Done 2026-10-09: construction → space type table with kind/area_m2/gross_m2/count.
- ~~Decide the Skill + scripts structure and how it is invoked.~~
  Done 2026-10-09: `envelope-area-extractor` skill with `scripts/extract_envelope.py`.
- Provide the real zone → space-type mapping CSV (currently an example map is used).
