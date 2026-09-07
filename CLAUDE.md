# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project purpose

Tools for managing an Etsy shop: generating product tags and descriptions, working with design files, and creating new designs.

## Scripts

- Use Python for any logic beyond a few lines.
- Use bash (run directly) for simple one-off operations (file moves, renames, bulk deletes).
- Place Python scripts at the repo root or in a `scripts/` subdirectory as the project grows.

## Running scripts

```bash
python3 <script>.py
```

No virtual environment or package manager is set up yet. If dependencies are needed, install with `pip3` and document them here.
