# mytodo — brief

A console-themed to-do app built as an installable Progressive Web App.

## Shape

Single-file app: all HTML + CSS + vanilla JS lives in `index.html` (~900 lines).
Supporting files: `manifest.json`, `sw.js` (service worker), `icons/`. No frameworks,
no build step, only a Google Fonts import (JetBrains Mono).

## Aesthetic

Terminal/console look — dark `#0a0a0a` background, monospace font, a `~/tasks $`
shell prompt in the header, `//` comment-style section titles, mint-green accent
(`#00c896`). Mobile-first (max-width 480px, safe-area insets, apple-mobile-web-app
meta tags).

## Features

- Tasks with optional **subtasks** (expandable drawers, `a/b/c` progress like `2/3 done`)
- Two tabs: **active** and **archived** — `✓` archives a task, `✕` deletes it
- **Deadlines** via a custom calendar picker + an iOS-style drum/wheel time picker
  (hours + 5-min minutes), built from scratch with pointer events, drag velocity, fling snap
- Status indicators: pending / upcoming / overdue dots, with an overdue counter in the header

## Persistence & offline

State stored in `localStorage` (`todo_tasks`, `todo_archived`). Service worker caches
the shell (cache-first) so the app works offline and is installable.

## Deployment

Hosted on GitHub Pages (`start_url: "/mytodo/"`; a custom domain via CNAME was tried
then removed).

## Known rough edges

- `deadlineStatus` compares only the hour (not the minute) for same-day overdue checks —
  a task due at `14:30` reads as overdue starting at `14:00`.
- No editing of an existing task — only create, complete, or delete.
- The drum picker's minute-index fallback `|| 0` is a latent trap if the values array changes.
