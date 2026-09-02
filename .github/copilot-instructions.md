<!-- .github/copilot-instructions.md - Guidance for AI coding agents -->
# Project snapshot

This repository is a tiny static site that uses Tailwind CSS to build a single stylesheet.

- Build flow: `src/input.css` (contains Tailwind directives) -> `tailwindcss` (via PostCSS) -> `dist/output.css` -> served by `src/index.html`.
- No backend, no tests, no bundler beyond Tailwind/PostCSS.

# Quick commands (run at repository root)

- Install dev tools (if needed): `npm install`
- Build production CSS: `npm run build`
- Watch for development changes: `npm run watch`

The `build` script runs:

```
tailwindcss -i ./src/input.css -o ./dist/output.css
```
and `watch` adds `--watch`.

# Key files

- `package.json` — scripts and devDependencies (tailwindcss, postcss, autoprefixer).
- `tailwind.config.js` — content paths: `./src/**/*.{html,js}` (controls which classes are generated).
- `postcss.config.js` — PostCSS plugins used.
- `src/input.css` — Tailwind directives `@tailwind base/components/utilities` (source).
- `src/index.html` — references final stylesheet at `/dist/output.css`.

# Patterns & conventions an AI should follow

- Do not assume a JS/Node app — this is CSS-first static site. Changes to HTML/CSS are primary.
- Keep edits minimal and localized: prefer changing `src/*` files and update `tailwind.config.js` only when expanding content paths or theme tokens.
- Avoid adding a bundler or framework unless requested — the project intentionally uses plain HTML + Tailwind CLI.

# Integration points & deployment notes

- The produced CSS (`dist/output.css`) is the only build artifact. CI or hosting must ensure this file exists at publish time.
- `package.json` has a `homepage` URL indicating a GitHub repo; confirm hosting target before modifying paths.

# Examples (common tasks)

- Add a new page: create `src/newpage.html` and include `<link href="/dist/output.css" rel="stylesheet">`. Add any new classes and run `npm run build`.
- Add utility-safe content path: update `tailwind.config.js` `content` array before adding non-HTML sources.

# When to ask the repo owner

- If you need to introduce a build step that changes output paths (for example, change `/dist/output.css` to another location).
- If deployment requires in-repo `dist` commits vs generating during CI.

# Do not change

- Do not remove the Tailwind/PostCSS devDependencies without a migration plan.
- Do not assume server-side rendering or Node-based routing; this repository is static.

---
If any parts are unclear or you want additional guidance (CI, commit hooks, or GitHub Pages deployment), tell me which area to expand.
