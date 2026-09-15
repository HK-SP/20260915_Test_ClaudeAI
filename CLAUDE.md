# CLAUDE.md

Guidance for Claude Code (and other agents) working in this repository.

## Stack & Conventions

**Hard constraint: vanilla HTML, CSS, and JavaScript only — no frameworks, no build step.**

- No frontend frameworks or libraries (React, Vue, Svelte, jQuery, etc.).
- No CSS frameworks or preprocessors (Tailwind, Bootstrap, Sass/Less).
- No bundlers, transpilers, or build tooling (Webpack, Vite, Babel, TypeScript compiler).
- No `package.json` / `node_modules` dependencies for shipping the site — plain `.html`, `.css`, and `.js` files served as-is.
- Write standard ES modules/scripts directly usable by browsers, with no compilation step.

**Hard constraint: the entire project must live in a single `index.html` file, with all CSS and JavaScript inlined via `<style>` and `<script>` tags — no separate HTML files.**

- No additional pages — everything is one `index.html`.
- CSS and JS must be inlined in `<style>`/`<script>` tags, not split into separate `.css`/`.js` files.
- Linking external images and external CSS/JavaScript libraries (e.g. via `<link>`/`<script src>` to a CDN) is allowed.
- This is so the finished project can be copy-pasted as a single file for sharing in class and on single-file code platforms.
