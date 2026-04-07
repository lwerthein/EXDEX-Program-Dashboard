# EXDEx Program Dashboard

Interactive weekly status dashboard for the Mayo Clinic Executive Health Digital Experience (EXDEx) project.

**[View live dashboard](https://lwerthein.github.io/EXDEX-Program-Dashboard/)**

## How to update weekly

### Option 1: Claude Code (recommended)

1. Clone this repo
2. Give Claude Code a weekly status PDF and say: *"Update the EXDEx dashboard with this week's data"*
3. Claude reads the PDF, adds a new week to the `WEEKS` object, and commits

The `SKILL.md` file gives Claude all the context it needs.

### Option 2: Manual edit

1. Open `EXDEx_Dashboard_v5.html`
2. Find `const WEEKS = {` near the top
3. Copy the last week's entry as a template
4. Update the data following the schema in `docs/data-schema.md`
5. Update `gantt.todayPosition` (moves ~4% per week)
6. Commit and push — GitHub Pages deploys automatically

## Structure

```
EXDEx_Dashboard_v5.html   # The dashboard (single self-contained file)
SKILL.md                  # Claude Code skill for automated updates
docs/data-schema.md       # JSON schema reference
```

## How it works

The entire dashboard is one HTML file. All data lives in a `WEEKS` JavaScript object. The client selects a week from the dropdown and the page re-renders. No build step, no dependencies.