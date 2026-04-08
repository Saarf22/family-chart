# TODO — family-chart

TypeScript + D3 library for rendering interactive family tree visualizations. This TODO covers library quality, publishing, and feature completeness.
Read `README.md` for full project context before starting any task.

---

## 🔴 HIGH PRIORITY

### 1. Publish to npm
**What:** Library is not published to npm.
**Why:** Other projects (including MFT) depend on it — should be a versioned package, not a git submodule.
**How:** Add `name`, `version`, `main`, `module`, `types` fields to `package.json`. Set `"private": false`. Run `npm publish` with an npm account. Set up a publish workflow in GitHub Actions on tag push (`v*`). Use semantic versioning.

### 2. Unit Tests
**What:** No unit tests — only Cypress e2e.
**Why:** Core layout algorithms and data transformations have no regression protection.
**How:** Add `vitest` or `jest`. Test: data normalization functions, relationship type resolution, layout calculation edge cases (single person, very wide trees). Target 70%+ coverage on non-rendering logic.

### 3. Complete API Documentation
**What:** Typedoc generated but not published or complete.
**Why:** Library is unusable without knowing the API.
**How:** Audit all public exports for JSDoc comments. Publish Typedoc output to GitHub Pages (`gh-pages` branch). Add a "Getting Started" section to README with a minimal code example. Document all config options.

---

## 🟡 MEDIUM PRIORITY

### 4. Accessibility (ARIA Support)
**What:** No ARIA attributes on the SVG/DOM tree.
**Why:** Screen readers can't navigate the tree; fails accessibility audits.
**How:** Add `role`, `aria-label`, `aria-describedby` to person nodes. Add keyboard navigation (arrow keys to move between relatives). Ensure focus indicators are visible.

### 5. Mobile & Touch Interaction
**What:** Touch gestures for pan/zoom are not well-supported.
**Why:** Many users view family trees on phones.
**How:** Add proper touch event handlers (pinch-to-zoom, drag-to-pan). Test on iOS Safari and Android Chrome. Use `pointer events` API for unified mouse/touch handling.

### 6. Additional Relationship Types
**What:** Some relationship types are missing.
**Why:** Real-world family structures are complex (adoption, step-parents, same-sex parents, etc.).
**How:** Audit current relationship enum. Add: adopted, step-parent, foster, partner/unmarried. Document visual treatment for each (line style, color). Ensure backwards compatibility.

### 7. Large Tree Performance (500+ people)
**What:** Performance with large trees untested.
**Why:** A real family tree can have hundreds of nodes — layout and render must stay smooth.
**How:** Profile with a synthetic 500-node dataset. If layout is slow, move calculation to a Web Worker. If render is slow, consider SVG virtualization or canvas rendering for large trees. Document performance limits.

---

## 🟢 LOW PRIORITY / NICE TO HAVE

### 8. Dark Mode Support
**What:** No dark mode styling.
**Why:** Library should respect user's OS theme preference.
**How:** Use CSS custom properties for all colors. Provide a `theme` config option (`light` | `dark` | `auto`). Default to `prefers-color-scheme` via `matchMedia`.

### 9. More Real-World Examples
**What:** Examples are minimal and generic.
**Why:** Developers evaluate libraries by examples — poor examples = low adoption.
**How:** Create 3 example configs: basic nuclear family, multi-generational tree (4+ generations), complex blended family. Host on a demo page (GitHub Pages). Show different layout options.

---

## ✅ DONE
- [x] TypeScript + D3 scaffold
- [x] Rollup build configuration
- [x] Basic family tree rendering
- [x] Cypress e2e tests
- [x] Typedoc setup

---

## Notes for Agents
- Build: `npm run build` → outputs to `dist/`
- The library is used by `repos/MFT` — test changes there before publishing
- D3 version compatibility: check `package.json` — D3 v6/v7 have breaking API differences
- Rollup outputs: CJS + ESM + types — verify all three work after changes
