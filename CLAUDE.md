# CLAUDE.md

Guidance for Claude Code (and other agents) working in this repository.

## Stack & Conventions

**Hard constraint: vanilla HTML, CSS, and JavaScript only — no frameworks, no build step.**

- No frontend frameworks or libraries (React, Vue, Svelte, jQuery, etc.).
- No CSS frameworks or preprocessors (Tailwind, Bootstrap, Sass/Less).
- No bundlers, transpilers, or build tooling (Webpack, Vite, Babel, TypeScript compiler).
- No `package.json` / `node_modules` dependencies for shipping the site — plain `.html`, `.css`, and `.js` files served as-is.
- Write standard ES modules/scripts directly usable by browsers, with no compilation step.
