# Deploy With GitHub Pages

GitHub Pages hosts the cleaning tracker. No Firebase or other services are needed — everything runs in the browser.

## 1. Create A GitHub Repo

1. Go to [github.com/new](https://github.com/new).
2. Name it something like `cleaning-tracker`.
3. Keep it Public (GitHub Pages on free accounts requires a public repo).
4. Click `Create repository`.

If you are adding this to an existing repo that already has GitHub Pages turned on, skip to step 2 and then you are done — no need to redo step 3.

## 2. Upload To GitHub

Upload the contents of this folder, not the folder itself:

- `index.html`
- `README.md`
- `DEPLOY.md`
- `.nojekyll`

In the repo: `Add file` -> `Upload files` -> drag the files in -> `Commit changes`.

Important: the main file must be named exactly `index.html` — all lowercase, no `(1)` from a re-download, no folder around it.

## 3. Turn On GitHub Pages

In the GitHub repo:

1. Open `Settings`.
2. Open `Pages`.
3. Under `Build and deployment`, choose `Deploy from a branch`.
4. Choose branch `main`.
5. Choose folder `/root`.
6. Click `Save`.

GitHub will give you a link like:

`https://your-username.github.io/cleaning-tracker/`

## 4. Wait For The Deploy

1. Open the repo's `Actions` tab.
2. Wait for `pages build and deployment` to show a green check (usually 1 to 5 minutes).
3. Open your Pages link in a browser. You should see the tracker, not a 404.

If you see a 404 after the green check, wait 2 more minutes and hard-refresh (Ctrl+Shift+R, or Cmd+Shift+R on Mac).

## 5. Use It In Notion

1. Open Notion.
2. Type `/embed`.
3. Paste the GitHub Pages link.
4. Choose `Embed`.

## Troubleshooting 404

- The working link ends in `.github.io/...`, not `github.com/...`.
- The repo must contain `index.html` at the top level, not inside a subfolder.
- Pages must show `Your site is live at ...` in `Settings` -> `Pages`.
- The first deploy after enabling Pages can take up to 10 minutes.
