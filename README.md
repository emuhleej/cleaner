# Cleaning Tracker

Static GitHub Pages friendly cleaning tracker for Notion embeds.

Three rooms (renameable) with daily, weekly, and monthly task lists. Daily tasks reset at 10 AM (night-shift friendly), weekly tasks reset every Monday, monthly tasks reset on the 1st.

## Files

- `index.html` contains the full app.
- `DEPLOY.md` has the GitHub Pages setup steps.
- `.nojekyll` helps GitHub Pages serve the folder as plain static files.

## Notion Embed

1. Publish this folder with GitHub Pages.
2. Copy the public URL for the page.
3. In Notion, type `/embed`.
4. Paste the URL.

## Notes

No Firebase needed. Checked-off tasks are saved in the browser that opens the app (localStorage), tied to the page URL. Progress persists between visits as long as the URL stays the same.

To edit rooms or tasks, tap `Edit lists` inside the app.
