# /init draft (original, unedited)

> This is the draft Claude Code's `/init` produced before any manual edits. Kept here for reference/comparison.

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Node.js/Express API. Entry point: `server.js`. Routes live in `routes/`, and data access goes through `db/store.js`.

## Common Commands

```bash
npm run dev
npm test
npm run lint
```

## Codebase Structure

- `server.js` — app entry point
- `routes/` — one file per resource
- `db/store.js` — data access layer

---

# Final CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Purpose

An Express API. Handles HTTP routes for the app's resources and reads/writes data through a single data-access module rather than scattering database/storage calls across route handlers.

## Commands

- Start the dev server (with reload):
  ```bash
  npm run dev
  ```
- Run the test suite:
  ```bash
  npm test
  ```
- Run the linter:
  ```bash
  npm run lint
  ```
- _(Wish-list addition)_ Run a single test file, once the test runner supports it:
  ```bash
  npm test -- <path/to/file>
  ```
- _(Wish-list addition)_ When a new npm script is added (e.g. `npm run build`), document it here immediately so it isn't lost.

## Conventions

- Use `db/store.js` for all data access, not direct database/file calls inside route handlers — keeps persistence logic in one place and route files thin.
- Use async/await for asynchronous code, not raw `.then()`/`.catch()` chains — keeps route handlers and store functions consistent and easier to read.
- Use one route file per resource under `routes/`, not one giant router file — mirrors the Architecture section below and keeps diffs scoped to a single resource.
- _(Wish-list addition)_ Use `npm run lint` before committing, not just relying on editor lint — catches issues CI will also flag.

## Architecture

- `server.js` — application entry point; creates the Express app, wires up middleware, and mounts the routers from `routes/`.
- `routes/` — one file per resource (e.g. `routes/users.js`, `routes/orders.js`); each file defines the HTTP endpoints for that resource and calls into `db/store.js` for data, rather than talking to storage directly.
- `db/store.js` — single data-access layer; all reads/writes to the underlying data store go through here, so routes stay focused on HTTP concerns.
- _(Wish-list addition)_ As the app grows, consider splitting `db/store.js` by resource (e.g. `db/users.js`) once it gets large, but keep a single import surface so route files don't need to change.

---

## What changed and why

The original `/init` draft was already close to correct (it identified `server.js`, `routes/`, and `db/store.js` accurately), so I kept its Architecture facts and expanded on them rather than replacing them. I added the Conventions section from my wish list — the "use X, not Y" rules on data access, async style, and one-file-per-resource routing — because those aren't things `/init` can infer from the code alone, and I added a lint-before-commit habit and a note about documenting new npm scripts since those are easy to forget. I did not add speculative architecture (e.g. a database engine or auth layer) since I don't want CLAUDE.md asserting things that aren't in the code yet.
