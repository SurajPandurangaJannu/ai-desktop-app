# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

## Project Overview

Full-stack web application with a React/Next.js frontend and a Node.js backend. All UI work must follow the design intelligence rules below, sourced from the `ui-ux-pro-max` skill, Google Fonts, and Playwright CLI.

---

## Setup & Commands

```bash
# Install dependencies
npm install

# Dev server (frontend)
npm run dev

# Dev server (backend)
npm run server

# Build for production
npm run build

# Run all tests
npm test

# Run a single test file
npx playwright test tests/<file>.spec.ts

# Lint
npm run lint

# Type check
npm run typecheck
```

### Playwright CLI (browser automation & testing)

```bash
# Install globally
npm install -g @playwright/cli@latest

# Install browsers
npx playwright install

# Open a browser session
playwright-cli open https://localhost:3000

# Take a snapshot (captures element references)
playwright-cli snapshot

# Screenshot
playwright-cli screenshot

# Record a new test
playwright-cli codegen https://localhost:3000

# View active sessions dashboard
playwright-cli show

# Run tests headlessly
npx playwright test

# Run one spec
npx playwright test tests/home.spec.ts

# Session management (multiple browsers)
playwright-cli -s=session1 open https://localhost:3000
playwright-cli list
playwright-cli close-all
```

Playwright config lives in `.playwright/cli.json`. Default timeouts: action 5 000 ms, navigation 60 000 ms. Tests target Chromium, Firefox, and WebKit.

---

## UI/UX Design System Rules

This project uses the **UI/UX Pro Max** design intelligence system (v2.5.0). The skill ships 67 UI styles, 161 color palettes, 57 font pairings, 99 UX guidelines, and 161 industry-specific reasoning rules.

### Install the skill

```bash
npm install -g uipro-cli
uipro init --ai claude
```

### Generate a design system for a feature

```bash
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "SaaS landing page" --design-system -p "MyApp"
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "dashboard analytics" --domain style --stack react
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "checkout flow" --domain ux --persist
```

Flags: `--domain` (style / typography / color / chart / ux / landing / product), `--stack` (react / next / vue / html-tailwind / …), `--persist` (saves to `design-system/MASTER.md`).

### Design system generation workflow

1. Receive user request
2. Run 5 parallel domain searches (style, color, typography, ux, landing)
3. Reasoning engine selects the best match
4. Output: pattern structure · style priorities · color palette · typography · key effects · anti-patterns · checklist

---

## Pre-Delivery Checklist (mandatory before every UI commit)

- [ ] No emojis used as icons — use SVG only (Heroicons or Lucide)
- [ ] Every clickable element has `cursor-pointer`
- [ ] Hover states use smooth transitions: 150–300 ms ease
- [ ] Light-mode text contrast ≥ 4.5 : 1 (WCAG AA)
- [ ] All interactive elements have visible `:focus-visible` styles
- [ ] `prefers-reduced-motion` media query respected for all animations
- [ ] Responsive breakpoints tested: 375 px · 768 px · 1024 px · 1440 px

---

## Typography (Google Fonts)

Load fonts via the `<link>` tag or `next/font` (Next.js). Do not self-host unless offline support is required.

**Recommended pairings (from the 57-pair library):**

| Role | Font | Weight |
|---|---|---|
| Display / Hero | Inter, Plus Jakarta Sans, Sora | 700–900 |
| Body | Inter, DM Sans, Nunito | 400–500 |
| Monospace / Code | JetBrains Mono, Fira Code | 400 |
| Accent / Quote | Playfair Display, Lora | 400–600 |

Rules:
- Body size: minimum 16 px
- Line height: 1.5–1.75 for body, 1.1–1.3 for headings
- Max line length: 60–75 ch
- Use `font-display: swap` on all custom fonts

---

## UI Style Guide

Pick one primary style per page/feature and apply it consistently. Popular styles available in the skill:

- **Glassmorphism** — frosted-glass cards, `backdrop-filter: blur`, subtle borders
- **Minimalism** — whitespace-first, monochrome palette + one accent
- **Bento Grid** — card-based layouts, asymmetric grid
- **Dark Mode** — true black (#0a0a0a) or near-black, not just inverted light
- **Neumorphism** — soft shadows, same-hue highlights (use sparingly, accessibility risk)
- **Brutalism** — bold borders, raw typography, high contrast
- **AI-Native UI** — streaming text effects, skeleton loaders, pulsing indicators

---

## Color System

Always define a full token set before writing component CSS:

```css
:root {
  --color-brand-primary: /* from chosen palette */;
  --color-brand-accent:  /* complementary */;
  --color-surface-base:  /* page background */;
  --color-surface-raised:/* cards, modals */;
  --color-text-primary:  /* body text */;
  --color-text-muted:    /* secondary text */;
  --color-border:        /* dividers, inputs */;
  --color-success:       /* green */;
  --color-warning:       /* amber */;
  --color-danger:        /* red */;
}
```

Industry colour rules (apply the matching palette from the 161-palette library):
- **SaaS / Tech**: indigo, violet, slate
- **Finance**: navy, forest green, gold
- **Healthcare**: teal, soft blue, white
- **E-commerce**: warm neutrals + high-contrast CTA
- **Creative**: bold, unexpected accent over near-white base

---

## Accessibility Rules (99 UX Guidelines — key subset)

1. All images need descriptive `alt` text; decorative images use `alt=""`
2. Form inputs must have associated `<label>` elements, not just `placeholder`
3. Modal/dialog components trap focus and restore it on close (`aria-modal`, `role="dialog"`)
4. Color is never the sole differentiator (add icon, label, or pattern)
5. Keyboard navigation must be fully functional without a mouse
6. Error messages are associated with their field via `aria-describedby`
7. Skip-to-content link at the top of every page

---

## Component Patterns

- Use **Radix UI** or **shadcn/ui** primitives for accessible headless components
- Animations via **Framer Motion** or CSS transitions — always wrap in `prefers-reduced-motion` check
- Icons: **Lucide React** (default) or **Heroicons** — never raw emoji
- Forms: **React Hook Form** + **Zod** for schema validation
- Data tables: virtual-scroll for > 100 rows

---

## Playwright Testing Rules

- Locate elements by role or `data-testid`, never by class name or CSS selector
- Authenticate once with `state-save`, reuse state across tests
- Use `snapshot` before assertions to capture element references (`e15`-style refs)
- Mock slow or flaky APIs with `route <pattern>` during unit/integration tests
- Record video on failure only: `video: 'retain-on-failure'` in `playwright.config.ts`
- Test against all three engines: Chromium, Firefox, WebKit

---

## Architecture

```
MyApp/
├── app/               # Next.js App Router pages & layouts
├── components/        # Shared UI components
│   ├── ui/            # Primitive / headless wrappers (shadcn/ui)
│   └── features/      # Domain-specific composed components
├── lib/               # Shared utilities, hooks, API clients
├── server/            # Backend (Node.js / Express or Next.js API routes)
│   ├── routes/
│   ├── controllers/
│   └── services/
├── design-system/     # Generated MASTER.md + page-specific overrides (from uipro)
├── tests/             # Playwright specs
├── public/            # Static assets
└── .playwright/       # cli.json config
```

State management: prefer React Server Components + `useState`/`useReducer` for local state. Use a store (Zustand) only for genuinely global client state.

---

## Key Dependencies

| Package | Purpose |
|---|---|
| `next` | Full-stack React framework |
| `tailwindcss` | Utility-first CSS |
| `shadcn/ui` | Accessible component primitives |
| `lucide-react` | Icon library |
| `framer-motion` | Animation |
| `react-hook-form` + `zod` | Forms & validation |
| `@playwright/test` | E2E testing |
| `@playwright/cli` | Agent-driven browser automation |

---

## Knowledge Graph (Graphify)

This project uses **Graphify** (https://github.com/safishamsi/graphify) to maintain a live knowledge graph of the codebase. The graph is stored in `graphify-out/` and committed to version control so all contributors get instant context.

### Install

```bash
uv tool install graphifyy
graphify install
```

### Build / rebuild the graph

```bash
# Full build (first time or after large refactors)
/graphify .

# Incremental update (only changed files — run this after every code change)
/graphify . --update
```

**The graph must be rebuilt after every meaningful code change.** This keeps `graphify-out/graph.json`, `graphify-out/graph.html`, and `graphify-out/GRAPH_REPORT.md` up to date.

### Auto-rebuild on commit

Install the git hook so the graph rebuilds automatically on every commit:

```bash
graphify hook install
```

### Query the graph

```bash
/graphify query "how does authentication flow work"
/graphify path "UserController" "JWTMiddleware"
graphify export callflow-html        # Architecture diagram
```

### Outputs

| File | Purpose |
|---|---|
| `graphify-out/graph.html` | Interactive visual browser |
| `graphify-out/GRAPH_REPORT.md` | God nodes, surprising connections, suggested questions |
| `graphify-out/graph.json` | Full queryable graph data |

### Ignore patterns

Create `.graphifyignore` for patterns to exclude (mirrors `.gitignore` syntax). If absent, `.gitignore` is used.

### Rules for using the graph

- Before asking "where is X defined?" or "what calls Y?", run `/graphify query` first
- After adding a new file, module, or significant refactor, run `/graphify . --update`
- Commit `graphify-out/` — teammates should not need to rebuild from scratch
- Read `graphify-out/GRAPH_REPORT.md` at the start of unfamiliar feature work to orient quickly

### Architecture diagram

```
graphify-out/
├── graph.html          # Visual browser (open in browser)
├── graph.json          # Full graph data
└── GRAPH_REPORT.md     # Findings, god nodes, suggested queries
```

## graphify

This project has a knowledge graph at graphify-out/ with god nodes, community structure, and cross-file relationships.

Rules:
- For codebase questions, first run `graphify query "<question>"` when graphify-out/graph.json exists. Use `graphify path "<A>" "<B>"` for relationships and `graphify explain "<concept>"` for focused concepts. These return a scoped subgraph, usually much smaller than GRAPH_REPORT.md or raw grep output.
- If graphify-out/wiki/index.md exists, use it for broad navigation instead of raw source browsing.
- Read graphify-out/GRAPH_REPORT.md only for broad architecture review or when query/path/explain do not surface enough context.
- After modifying code, run `graphify update .` to keep the graph current (AST-only, no API cost).
