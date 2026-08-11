---
description: Deploy this project to Vercel and report the live URL
---

Deploy the local project in this repo to Vercel and give the user the resulting deployment URL. Work through these steps in order and don't skip any:

1. **Check Vercel auth.** Run `npx vercel whoami`. If it reports not logged in, tell the user to authenticate themselves first by running `npx vercel login` (this is an interactive login flow — suggest they run it via `! npx vercel login` in the Claude Code prompt, or run it in their own terminal), then stop and wait for them to confirm they're logged in before continuing.

2. **Ensure the build output directory is configured.** This project's `vite.config.ts` sets `build.outDir` to `build` (not Vite's default `dist`). Check if `vercel.json` exists at the repo root:
   - If it doesn't exist, create it with:
     ```json
     {
       "buildCommand": "npm run build",
       "outputDirectory": "build"
     }
     ```
   - If it exists, verify `outputDirectory` is `"build"` and fix it if not.

3. **Build locally first** with `npm run build` to catch any build failures before pushing to Vercel. If the build fails, show the actual error output to the user and stop — do not attempt to deploy a broken build.

4. **Deploy to production** by running `npx vercel --prod --yes` from the repo root. This uses/creates the `.vercel` project link automatically (it's already gitignored). Let this run to completion.

5. **Report the URL.** Parse the deployment URL out of the CLI output (it prints a `https://<project>.vercel.app` production URL on success) and give it to the user clearly, e.g.:
   > ✅ Deployed: https://your-project.vercel.app

   If the deploy command fails or errors, show the actual CLI error output rather than guessing at the cause, and suggest a next step (e.g. re-auth, fix build error, check vercel.json).

Notes:
- Use `npx vercel` throughout rather than assuming a global `vercel` install, since the CLI isn't installed globally in this environment.
- Don't use `--yes` on the first-ever `vercel login` — that step is interactive by nature and can't be done on the user's behalf.
- If the user just wants a quick preview deploy instead of production, use `npx vercel --yes` (no `--prod`) and mention the URL is a preview deployment, not production.
