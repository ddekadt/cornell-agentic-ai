# Agentic AI for Social Science and Data Science Research

Materials for the agentic AI workshop at Cornell, Department of Government. The workshop will take place over two sessions, on Friday 11 and Friday 18 September 2026, 9am–12pm.

> **Up to date as of 17 September 2026.** If you are reading this later, assume some of it has changed.

## Before the first session

Install a terminal-based agentic AI and check the rest of your toolchain. Allow 20 minutes.

- [macOS setup](./gemini-cli-setup-mac.md)
- [Windows setup](./gemini-cli-setup-windows.md)

The guides use **[Gemini CLI](https://github.com/google-gemini/gemini-cli)**, which is free with a personal Google account. If you already have Claude Code, Codex CLI or Gemini CLI working in your terminal, use that instead — but it has to run in the terminal, not as a desktop app or in a browser.

You'll need a laptop you can install software on, a personal Google account, and internet access.

## What's in this repo

| File / folder | Purpose |
|---|---|
| `gemini-cli-setup-mac.md` | Setup guide for macOS |
| `gemini-cli-setup-windows.md` | Setup guide for Windows |
| `project_participant/` | Your working folder for the first exercise — a blank `GEMINI.md` to fill in, and pre-staged data under `data/raw/` |
| `slides/` | Slides for both sessions, as `.html` (open in a browser) and `.Rmd` source |

The demo project is added as we go.

## The data

`project_participant/data/raw/` holds American Community Survey data for all 2,327 census tracts in New York City, plus tract boundaries. See [`project_participant/DATA_SOURCES.md`](./project_participant/DATA_SOURCES.md) for what each file contains, where it came from, and how to join the pieces together.

## Questions

If you hit a setup problem before the workshop, email me or raise an issue — sooner is better than Friday morning.
