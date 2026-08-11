# AGENTS

## Purpose
This repository is a small React + Vite single-page game. The main feature is a treasure chest mechanic in `src/App.tsx`, with sound and animation.

## Key files
- `src/App.tsx` – primary game logic, state, scoring, animations, and audio handling.
- `src/main.tsx` – app entry point.
- `src/index.css` – the actual CSS loaded by the app. It is a checked-in prebuilt Tailwind-style stylesheet; there is no Tailwind build step.
- `vite.config.ts` – Vite config with versioned import aliases for the scaffolded `src/components/ui` components.
- `src/components/ui/` – generated UI component library scaffold; most files are unused.

## Build / run
- `npm install`
- `npm run dev`
- `npm run build`

## Important conventions
- This is a tiny interactive game, so keep changes simple and localized.
- Do not assume a Tailwind build pipeline. Use only CSS classes already present in `src/index.css`, or add matching CSS manually if new utility styles are required.
- If you add a new package import with a versioned specifier like `@radix-ui/react-dialog@1.1.6`, update `vite.config.ts` alias mapping, or use the normal package import form instead.
- There is no lint/test framework configured in this repo.

## Notes for AI agents
- Prefer edits to `src/App.tsx` for game-related features.
- Avoid adding large architectural changes unless the user explicitly asks.
- Respect the existing visual style and the simple treasure-hunt concept.

## References
- [README](README.md)
- [CLAUDE.md](CLAUDE.md)
