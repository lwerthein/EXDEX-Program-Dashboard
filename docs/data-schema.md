# EXDEx dashboard data schema

All data lives in `const WEEKS = {}` in the HTML file. Each key is a week label for the dropdown.

## Week object

```javascript
"Week 5 – Apr 3, 2026": {
  urgentItems: ["string"],        // Red-tier: hard blockers, dependencies
  attentionItems: ["string"],     // Yellow-tier: delays, scope changes
  gantt: { ... } | null,          // Gantt chart (see below), or null to hide
  workstreams: [ ... ]            // Array of workstream objects (see below)
}
```

## Gantt object

```javascript
gantt: {
  title: "Road to Gonda-19 launch: 14 weeks",
  months: ["01/26","02/26","03/26","04/26","05/26","06/26","07/26"],
  todayPosition: 42,       // % across timeline – UPDATE EACH WEEK
  launchPosition: 96,      // % across timeline
  launchLabel: "Gonda 19 – July 6",
  lanes: [{
    label: "Website",
    color: "#3B82F6",
    status: "on-track",     // "on-track" | "at-risk" | "blocked"
    barStart: 0, barEnd: 100,
    activeStart: 18, activeEnd: 52,
    milestones: [{ pos: 32, label: "Milestone\\nLine 2" }]
  }]
}
```

## Workstream object

```javascript
{
  name: "App / website",
  color: "app",              // "ops" | "app" | "products" | "experiences"
  status: "on-track",        // "on-track" | "at-risk" | "blocked"
  oneliner: "Shown when collapsed.",
  summary: "Shown when expanded.",
  milestones: [
    { label: "Alpha", date: "Apr 2026", status: "soon" }
    // status: "done" | "soon" | "future" | "canceled"
  ],
  progress: { completed: 5, total: 18 },
  inProgress: {
    "Group Name": ["Item 1", "Item 2"]
  },
  upcoming: [
    { date: "Apr", text: "Description" }
  ],
  completed: {
    "Group Name": ["Item A"]
  },
  deliverables: {
    completed: { "Group": ["Item"] },
    upcoming: { "Group": ["Item"] },
    removed: { "Group": ["Item – removed due to pivot"] }
  }
}
```

## Tips for extracting from PDFs

- Urgent = anything with hard dates, dependencies, or cancellations
- Attention = delays, scope changes, things to watch
- Group `inProgress` items by sub-workstream (e.g., "Website", "App")
- Items with "canceled" or "removed" in the text auto-get strikethrough
- `todayPosition` moves ~4% per week on a Jan–Jul timeline