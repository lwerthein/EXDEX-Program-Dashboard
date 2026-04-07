---
name: exdex-dashboard
description: >
  Generate and update the EXDEx interactive HTML dashboard for the Mayo Clinic Executive Health
  Digital Experience project. Converts weekly status report PDFs into a branded, client-facing
  HTML dashboard. Use when someone asks to update the dashboard, add a new week, or convert a
  status PDF into the dashboard.
---

# EXDEx interactive dashboard

## How to update

1. Read `EXDEx_Dashboard_v5.html`
2. Read the new weekly status PDF the user provides
3. Extract data into the JSON schema (see `docs/data-schema.md`)
4. Add a new week entry to the `WEEKS` object in the HTML file
5. Commit and push

## Data location

All data lives in `const WEEKS = {}` near the top of the HTML file. Each key is a week label
shown in the dropdown. See `docs/data-schema.md` for the full schema.

## Key rules

- Status values: `"on-track"`, `"at-risk"`, or `"blocked"` (never use "risk" alone)
- Workstream colors: `"ops"`, `"app"`, `"products"`, `"experiences"`
- Milestone statuses: `"done"`, `"soon"`, `"future"`, `"canceled"`
- Update `gantt.todayPosition` each week to move the "Today" line
- Sentence case only. En dash with spaces for separators.
- Items containing "canceled" or "removed" auto-get strikethrough styling