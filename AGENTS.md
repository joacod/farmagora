# AGENTS.md

This file gives coding agents repo-specific instructions for working in `farmagora`.

## Project Snapshot
- Stack: Astro 6, Tailwind CSS 4, Vite, ESM.
- Package manager: `pnpm` is the canonical choice because `pnpm-lock.yaml` is committed.
- Runtime requirement: Node `>=22.12.0`.
- TypeScript config extends `astro/tsconfigs/strict`.
- Current app shape: a small static Astro site with one page at `src/pages/index.astro`.
- Main styling entrypoint: `src/styles/global.css`.
- Build output is generated into `dist/`.

## Repo Layout
- `src/pages/` contains route files.
- `src/styles/` contains global styles and Tailwind import setup.
- `public/` contains static assets such as favicons.
- `astro.config.mjs` defines Astro and Vite integration.
- `tsconfig.json` enables strict Astro TypeScript defaults.
- Do not hand-edit `dist/`.
- Do not hand-edit `.astro/` generated files.

## Commands
### Install
- `pnpm install`
### Development
- `pnpm dev` - start the local Astro dev server.
- `pnpm astro dev --host` - start the dev server on the network when needed.
### Build
- `pnpm build` - production build.
- Verified working in this repo on 2026-03-11.
### Preview
- `pnpm preview` - preview the production build locally.
### Lint / Formatting / Checks
- There is currently no dedicated `lint` script in `package.json`.
- There is currently no Prettier, ESLint, Biome, or Stylelint config committed.
- `pnpm exec astro check` is not currently usable because `@astrojs/check` is not installed.
- If you add a lint or check tool, wire it into `package.json` scripts and document it here.

### Tests
- There is currently no test framework configured.
- There is no `test` script in `package.json`.
- There are no test files committed under `src/` or a dedicated `tests/` directory.

### Single Test Execution
- Not available yet because no test runner is configured.
- If a runner is added later, document the exact single-test command here.
- Good future examples would be commands shaped like `pnpm vitest run path/to/file.test.ts` or `pnpm playwright test tests/example.spec.ts`, but do not assume those exist until added.

## Current Source Conventions
### Imports
- Use ESM imports only.
- Prefer relative imports for nearby files, as shown by `import "../styles/global.css";`.
- Keep imports at the top of the frontmatter block in `.astro` files.
- Import global CSS once from the page or layout entrypoint.
- Avoid unused imports.

### Formatting
- Match the surrounding file instead of enforcing a global formatter style that is not configured.
- In `src/pages/index.astro`, indentation currently uses tabs.
- In JSON and config files, indentation currently uses two spaces.
- Existing JS/TS-style files use semicolons in import/config code; preserve that pattern when touching those files.
- Keep long attribute lists split across lines when readability improves.
- Favor one logical block per section in Astro templates.

### Types
- Respect strict TypeScript defaults inherited from `astro/tsconfigs/strict`.
- Prefer explicit data shapes when page data gets more complex.
- Avoid `any` unless there is a strong, documented reason.
- Keep simple static arrays inline when their shape is obvious and local.
- If shared data grows, extract typed constants or interfaces into dedicated modules.

### Naming
- Use descriptive, domain-oriented names.
- Follow current camelCase names for local constants like `feedOptions` and `reasons`.
- Use PascalCase for components if new Astro or framework components are added.
- Use lowercase kebab-case for route filenames unless Astro conventions require otherwise.
- Keep CSS class naming utility-first when using Tailwind.
- Prefer names that describe content or intent over implementation details.

### Astro Patterns
- Put data declarations in the frontmatter block.
- Keep page metadata in the document head.
- Use semantic HTML sections such as `header`, `main`, `section`, `article`, and `footer`.
- Prefer mapping arrays into repeated markup instead of duplicating similar blocks.
- Keep route files focused; extract repeated UI into components when reuse appears.
- Preserve static-site friendliness unless dynamic behavior is actually needed.

### Styling
- Tailwind CSS 4 is enabled through `@tailwindcss/vite` in `astro.config.mjs`.
- Global stylesheet uses `@import "tailwindcss";`.
- The visual language is intentional, editorial, and farm-themed rather than generic SaaS.
- Preserve the warm palette, soft gradients, rounded shapes, and approachable copy tone unless redesigning deliberately.
- Prefer utility classes in Astro markup for page-specific styling.
- Use `global.css` for true global rules only.
- Keep backgrounds layered and textured when extending the current design.
- Ensure changes still read well on mobile and desktop.

### Content and UX Tone
- Existing copy is playful, specific, and anti-corporate.
- Avoid generic marketing filler.
- Prefer concise, human-sounding text.
- Keep the brand voice friendly, grounded, and slightly witty.

### Error Handling
- There is little runtime logic today, so keep failure paths simple and explicit.
- Fail fast in build-time code when required data is missing.
- Prefer guard clauses over deeply nested conditionals.
- Do not swallow errors silently.
- If you introduce async data loading, surface actionable errors and preserve a usable fallback UI.

### Accessibility
- Keep semantic structure intact.
- Provide meaningful `alt` text for non-decorative images.
- Preserve visible text contrast against layered backgrounds.
- Ensure links and buttons remain distinguishable.
- Keep viewport and metadata tags intact unless intentionally changing SEO behavior.

## What Agents Should Not Do
- Do not edit generated output in `dist/`.
- Do not commit or rely on `node_modules/`.
- Do not add new tooling casually to this small repo.
- Do not introduce a client framework unless the task requires it.
- Do not convert simple static content into unnecessary abstractions.
- Do not replace the established visual tone with a bland default template.

## Cursor and Copilot Rules
- No `.cursor/rules/` directory is present.
- No `.cursorrules` file is present.
- No `.github/copilot-instructions.md` file is present.
- That means there are currently no extra Cursor or Copilot repository rules to merge into agent behavior.

## Safe Change Checklist
- Use `pnpm` for commands unless the repo is changed to another package manager.
- Check whether a change belongs in `src/pages/index.astro`, `src/styles/global.css`, or `public/`.
- Preserve strict TypeScript compatibility.
- Keep imports clean and local.
- Match existing indentation and punctuation in touched files.
- Prefer semantic HTML and Tailwind utilities over ad hoc complexity.
- Rebuild with `pnpm build` after meaningful changes.
- If you add tests or linting later, update this file immediately.

## Suggested Future Improvements
- Add `@astrojs/check` and a `check` script for static validation.
- Add a formatter and linter only if the team wants enforced consistency.
- Add a test runner before introducing behavior-heavy features.
- Once tests exist, document both full-suite and single-test commands here.
