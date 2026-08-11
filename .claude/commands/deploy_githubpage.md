---
description: Deploy this project to GitHub Pages and report the live URL
---

Deploy this repo to GitHub Pages:

1. Determine the target remote from `git remote -v`. Prefer a remote named `fork` (your own repo) over `origin` (likely upstream, not yours). If ambiguous, ask the user which one to use. Parse `<owner>/<repo>` from its URL.
2. Ensure `gh-pages` is installed as a devDependency: `npm install -D gh-pages` if missing.
3. Build with the Pages base path (without touching `vite.config.ts`, to not break the Vercel deploy): `npx vite build --base=/<repo>/`.
4. Publish: `npx gh-pages -d build -r <remote-url>`.
5. If `gh` is authenticated, enable Pages (ignore a 422 — it just means it's already on): `gh api -X POST repos/<owner>/<repo>/pages -f "source[branch]=gh-pages" -f "source[path]=/"`.
6. Report the URL: `https://<owner>.github.io/<repo>/` (note it can take a minute or two to go live on first deploy).

Never push to a remote you haven't confirmed the user owns.
