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

## Tech stack (hard constraints — do not deviate)
- Vanilla HTML, CSS, and JavaScript only. No React, Vue, or any JS framework.
- Tailwind CSS for all styling (via CDN only).
- No backend, no database. Fully static site.
- A toggle for light and dark theme, with the choice remembered
  across visits.

## Feature Plan

**This is a living plan.** As phases complete, mark their checkboxes done or prune finished detail so this stays skimmable — it isn't meant to accumulate forever.

**The site is a portal for a growing collection of small web tools and learning artifacts**, all living inside the single `index.html` per the hard constraints above. Since there are no separate pages, "browsing" and "using a tool" are just different views inside one page, switched by JS and tracked via `location.hash` so views stay linkable/bookmarkable.

### Phase 0 — Portal shell
- [ ] Page skeleton: Tailwind CDN, header (site title + theme toggle button), footer, main content area.
- [ ] Theme system: read `localStorage.theme` (fallback to `prefers-color-scheme`), apply before first paint, toggle button flips + persists it.
- [ ] Tool registry: a plain JS array of tool metadata (see Data model) — the single source of truth the gallery renders from.
- [ ] Gallery view: responsive card grid rendered from the registry; each card links to `#/tool/<id>`.
- [ ] Tool view + hash router: listens for `hashchange`, shows the matching tool's `<section>` and hides the gallery (and vice versa for `#/` or empty hash), plus a "Back to tools" control.

### Phase 1 — First two tools (proves the pattern)
**Tool choice is a placeholder pending your confirmation** — swap freely before building:
- [ ] Tool A: **Color Converter** — HEX ⇄ RGB ⇄ HSL with a live swatch preview.
- [ ] Tool B: **JSON Formatter & Validator** — paste JSON, pretty-print it, surface parse errors inline.
- [ ] Each tool is a self-contained `<section id="tool-<id>">` plus an `init<Tool>()` function, registered in the tool registry, initialized lazily (only when first navigated to).
- [ ] Confirms the registry → gallery → router → tool-section pattern works end-to-end with two real, unrelated tools before scaling up.

### Future phases (not yet planned)
Adding tool #3+ should mean: append one registry entry + one `<section>` + one init function — no changes elsewhere. Once the collection grows enough to need it, consider search/filter/tags on the gallery (own phase, not scoped yet).

### Data model
```js
// Single source of truth for the gallery — grows by one entry per new tool.
const TOOLS = [
  { id: 'color-converter', title: 'Color Converter', description: '...', tags: ['color', 'converter'] },
  { id: 'json-formatter',  title: 'JSON Formatter & Validator', description: '...', tags: ['text', 'json'] },
];
```
- **Theme state**: `localStorage['theme']` → `'light' | 'dark'`.
- **Route state**: `location.hash` → `''` (gallery) or `'#/tool/<id>'`.
- Both are the *only* persisted/shared state — no backend, no database, per the tech-stack constraint.

### Key flows
1. **Load** → apply saved/preferred theme before paint → parse current hash → render gallery or the matching tool view.
2. **Browse → open a tool** → click a card → hash changes to `#/tool/<id>` → router hides gallery, shows that tool's section, runs its init function once.
3. **Toggle theme** → click button → flip light/dark → persist to `localStorage` → update the root element's theme attribute/class.
4. **Grow the collection** (recurring, every future phase) → add a registry entry + a tool `<section>` + its init function → nothing else in the file needs to change.

## Writing Style

- Use a **bold lead-in** at the start of paragraphs where possible, to make paragraphs easier to scan and read.
