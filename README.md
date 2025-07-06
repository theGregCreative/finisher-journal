Finisher Journal Digital App - Requirements Document
✨ Overview
A digital version of the Finisher Secrets Journal system, hosted on Heroku, using a JSON-based data architecture. Each user’s data is stored as daily JSON files, allowing for lightweight access, strong privacy, offline support, and exportable summaries.

The app emphasizes a distraction-free, minimalist journaling experience, enhanced with modern features like reminders, search, and habit tracking.

🛠️ 1. Architecture Overview
Frontend: React (Tailwind CSS preferred)

Backend: Node.js with Express (or GraphQL)

Data Storage: Flat file system with one JSON file per user per day (/data/<user_id>/<YYYY-MM-DD>.json)

Authentication: Firebase Auth or Auth0 (expandable)

Hosting: Heroku

Indexing: Lightweight metadata indexes stored separately (/data/_indexes/)

Optional: File storage on S3 or Google Cloud for media (Phase 2)

📁 2. JSON File System
Structure
yaml
Copy
Edit
/data/
  ├── user123/
  │   ├── 2025-07-06.json
  │   ├── 2025-07-07.json
  │   └── ...
  └── _indexes/
      ├── metadata.json
      └── habit_streaks.json
Naming Convention
YYYY-MM-DD.json per user per day

Indexed metadata files for fast filtering/searching

🔑 3. User Management
Secure Signup/Login via Firebase/Auth0

Email verification + password reset

Role Types:

Basic User: Can access only their own journal

Admin: Internal role for backup/analytics

All journal data is stored locally in JSON by user/day

📂 4. Daily JSON File Format
Each file contains a full snapshot of a user’s entries for that day:

json
Copy
Edit
{
  "user_id": "user123",
  "date": "2025-07-06",
  "journal": {
    "title": "Q3 2025 Journal",
    "status": "active"
  },
  "goal": {
    "title": "Increase coaching clients",
    "description": "Reach 10 clients by Sept 30",
    "target_metric": 10,
    "commitment": "Daily outreach",
    "validated": true
  },
  "weekly_plan": {
    "week_start_date": "2025-07-01",
    "must_deliver_task": "Launch landing page",
    "secondary_tasks": [
      { "priority": "A", "task": "Finalize email copy", "status": "completed" },
      { "priority": "B", "task": "Reach out to 10 leads", "status": "completed" },
      { "priority": "C", "task": "Create new video ad", "status": "deferred" }
    ],
    "habit_tracker": {
      "Morning routine": true,
      "No phone pre-9AM": false
    },
    "review_notes": "Visual design delays dev flow"
  },
  "daily_entry": {
    "must_do": "Write landing page copy",
    "might_do": ["Sketch wireframe", "Call designer"],
    "task_status": {
      "must_do": "completed",
      "might_do_1": "incomplete",
      "might_do_2": "incomplete"
    },
    "reflection_notes": "Strong start to the week!"
  },
  "notes": [
    {
      "title": "CTA Ideas",
      "content": "Add urgency: 10 slots left!",
      "tags": ["#ideas"]
    }
  ]
}
🌟 5. Key Features
🎯 Goal Setting
90-day primary goals with measurable targets

Brainstormed action steps (10–15)

Validator checklist and commitment pledge

📅 Weekly Planning
Must-Deliver Task per week

A/B/C-prioritized secondary tasks

Habit tracker matrix

Weekly review notes

🧮 Daily Planning
Must Do + Might Do x2

Schedule blocks

Checkbox task status

Daily reflections and notes

📝 Notes & Tagging
Rich-text notes linked to day, week, or goal

Tags for searchability (#habit, #idea, #people)

Markdown-style summaries for export

🔍 Search & Navigation
Keyword search across JSONs

Filters by date, tags, goal, journal

Navigation shortcuts: "Today", "This Week", etc.

📈 Progress Visualization
Completion charts

Habit streaks

Weekly performance heatmaps

Summary metrics (% Must-Do completed)

🧩 6. Bonus Modules (Phase 2)
Distraction Filter: Daily checklist of distractions to eliminate

Monk Mode Protocol: 3-rule daily discipline challenge

Perfect Day Scripts: Guided schedule templates

$1000/Hr System: Worksheets + embedded training videos

🎨 7. UI/UX Guidelines
Clean, low-distraction interface

Mobile-first responsive layout

Bold visual cues for today’s focus

Hidden sections until needed

Light gamification: streaks, “win” counters

⏰ 8. Notifications
Daily journal reminder (e.g., 9:00 PM)

Weekly review prompt (e.g., Sunday at 5:00 PM)

Habit nudges (on successful streaks)

🔒 9. Security
Encrypted passwords via bcrypt

Role-based access control

JSON stored privately per user; no public indexing

SSL enforced on Heroku

Optional local encryption for each JSON file (future)

👨‍💼 10. Admin Tools (Optional)
Admin dashboard with user folder indexing

JSON export/download by user

Analytics from metadata indexes

Usage and engagement metrics

🚀 11. MVP Scope
✅ Must-Have
User auth and secure login

JSON-based journaling: Goals → Weeks → Days

Habit tracking, notes, and tagging

Markdown export capability

JSON index search + filtering

🌱 Nice-to-Have
Bonus module viewer

Scheduled notifications

Performance dashboard

PDF/CSV exports for printability

📤 12. Export Template for Summaries
File Naming
yaml
Copy
Edit
2025-07-Week-27-Summary.md
2025-07-Month-July.md
2025-07-Quarter-2-Journal.md
Markdown Summary Template
markdown
Copy
Edit
# 🧭 Weekly Summary: July 7–13, 2025

## 🎯 90-Day Goal:
Increase coaching clients from 5 → 10 by Sept 30  
**Commitment**: Focus on daily outreach, one lead at a time

---

## 📅 Weekly Must-Deliver:
✅ Launch landing page and collect 100 leads

### 🅰️ Secondary Tasks:
- A: Finalize email copy ✅
- B: Reach out to 10 leads via LinkedIn ✅
- C: Create new video ad 🎯 Deferred

---

## 🗓️ Daily Execution

### Monday:
- Must-Do: Write landing page copy ✅
- Might-Do: Sketch wireframe, call designer ❌
- Notes: Brainstormed new call-to-action idea → `#ideas`

### Tuesday:
- Must-Do: Set up lead form ✅
- Might-Do: Test form integrations ✅

...

---

## 📊 Habit Tracker:
| Habit               | Mon | Tue | Wed | Thu | Fri | Sat | Sun |
|---------------------|-----|-----|-----|-----|-----|-----|-----|
| Morning routine     | ✅  | ✅  | ✅  | ❌  | ✅  | ✅  | ✅  |
| No phone pre-9AM    | ✅  | ❌  | ✅  | ✅  | ✅  | ✅  | ❌  |
| 1 Must-Do completed | ✅  | ✅  | ✅  | ✅  | ❌  | ✅  | ✅  |

---

## 🔍 Reflections
**Highlight of the Week**: Launched the first working version of landing page!  
**Lessons Learned**: I procrastinate when the visual design isn't clear.  
**Improvements for Next Week**: Create visual assets before assigning dev tasks.

---

## 🧠 Indexed Notes
- `#idea`: “Get testimonial quote from Jenny” — July 9  
- `#habit`: “Moved meditation to post-lunch break” — July 11