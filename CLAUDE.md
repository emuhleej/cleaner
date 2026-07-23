# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A cleaning tracker: a single-file static web app meant to be hosted on GitHub Pages and embedded in Notion via `/embed`. It tracks daily/weekly/monthly cleaning tasks per room, with all state stored in the browser's `localStorage` — there is no backend, no build system, no package manager, and no test suite.

## Files

- `index.html` — the entire app: markup, CSS, and JavaScript in one file. This is the only file that matters for functionality.
- `cleaning-tracker.html` — a byte-for-byte duplicate of `index.html`. **When editing the app, apply the same change to both files** (or copy `index.html` over it) so they stay in sync.
- `cleaner file.zip` — an archive containing copies of the two HTML files; not used at runtime.
- `DEPLOY.md` — GitHub Pages setup instructions (deploy from branch `main`, folder `/root`).
- `.nojekyll` — makes GitHub Pages serve the folder as plain static files. Do not delete.

## Development

There are no build, lint, or test commands. To check a change, open `index.html` directly in a browser. Deployment is automatic: pushing to `main` triggers the `pages build and deployment` GitHub Action.

The main file must remain named exactly `index.html` at the repo root — GitHub Pages depends on it.

## Architecture of index.html

The `<script>` block is organized into commented sections:

- **CONFIG** — `DAY_ROLLOVER_HOUR = 10` shifts the "day" boundary to 10 AM (night-shift friendly; set to 0 for midnight). `STORAGE_KEY = 'cleaningTracker.v1'` is the localStorage key; bump the version suffix if the data shape changes incompatibly. `DEFAULT_DATA` seeds three rooms (Kitchen, Bathroom, Living Room) on first load.

- **Period keys (reset logic)** — tasks are never un-checked by a timer. Instead, each task stores a `doneKey` string, and a task counts as done only if its `doneKey` equals the current period key (`dayKey()` / `weekKey()` / `monthKey()`, all computed from `shiftedNow()`). Daily resets at the rollover hour, weekly resets Monday, monthly resets on the 1st. A `visibilitychange` listener re-renders when the tab regains focus so resets appear without a reload.

- **State** — the whole app state is one `data` object (`{ rooms: [{ name, tasks: { daily, weekly, monthly } }] }`), loaded from localStorage with a fallback to `DEFAULT_DATA`, plus three transient UI variables: `activeRoom` (index), `activeFreq`, and `editing`. Every mutation calls `save()` then `render()`.

- **Render** — no framework. `render()` rebuilds the room tabs, frequency tabs, task list, and progress bar from scratch on every change. Edit mode is toggled via the `editing` flag and a `body.editing` CSS class that reveals delete buttons and the add-task row.

## Conventions

- Everything stays in one self-contained HTML file — no external JS/CSS files, no dependencies beyond the Google Fonts links (Fraunces + Nunito Sans).
- Colors and radii come from CSS custom properties in `:root`; the three frequencies each have a signature color (daily = amber, weekly = teal, monthly = plum) used consistently across tabs and progress bars.
- The app is designed for a narrow Notion embed: single-column layout, `max-width: 680px`.
