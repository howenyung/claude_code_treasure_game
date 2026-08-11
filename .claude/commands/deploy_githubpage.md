---
description: Deploy this project to GitHub Pages and report the live URL
---

Deploy this repo to GitHub Pages:

1. Determine the target remote from `git remote -v`. Prefer a remote named `fork` (your own repo) over `origin` (likely upstream, not yours). If ambiguous, ask the user which one to use. Parse `<owner>/<repo>` from its URL.
2. Ensure `gh-pages` is installed as a devDependency: `npm install -D gh-pages` if missing.
3. Build with the Pages base path (without touching `vite.config.ts`, to not break the Vercel deploy): `MSYS_NO_PATHCONV=1 npx vite build --base=/<repo>/`. The `MSYS_NO_PATHCONV=1` is required on Windows/Git Bash — without it, MSYS silently rewrites the leading-slash `--base` argument into a Windows path (e.g. `/repo/` becomes `/Program Files/Git/repo/`), which corrupts every asset URL in the built `index.html` and produces a blank page in production.
4. Verify the build output before publishing: `grep -o 'src="[^"]*"\|href="[^"]*"' build/index.html` should show `/<repo>/assets/...` paths, not an absolute filesystem path.
5. Publish: `npx gh-pages -d build -r <remote-url>`.
6. If `gh` is authenticated, enable Pages (ignore a 422 — it just means it's already on): `gh api -X POST repos/<owner>/<repo>/pages -f "source[branch]=gh-pages" -f "source[path]=/"`.
7. Report the URL: `https://<owner>.github.io/<repo>/` (note it can take a minute or two to go live on first deploy, and the CDN can take up to ~90s to pick up a redeploy — poll if verifying immediately).

Never push to a remote you haven't confirmed the user owns.
