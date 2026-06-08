# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **single-file static web application** — a Korean-language educational reference for Vibe Coding (AI-assisted development). All content, styles, and logic live in `index.html`. There is no build step, no package manager, and no dependencies.

To preview: open `index.html` directly in a browser, or serve it locally:
```
python3 -m http.server 8080
```

Deployed via GitHub Pages at `https://sung00su99.github.io/VibeCodingData/`.

## Architecture

Everything is in `index.html`, organized in three blocks:

**`<style>`** — All CSS using MICUBE SOLUTION brand tokens:
- Primary Teal: `#0AAFB8` — borders, active tabs, headings, buttons
- Dark Navy: `#1C2D3A` — table headers, toast background
- Light Teal bg: `#E8F7F8` — code block backgrounds

**`<body>`** — Static content structured as:
- `header` → title + download button + logo
- `.tabs-wrapper` → sticky tab bar (7 tabs, `showTab(n)` switches active tab)
- `.content-wrapper` → one `.tab-content` div per tab, each containing `.section` blocks

**`<script>`** — Three feature areas:
- `showTab(n)` — tab switching
- `copyCode(el)` / `fallback()` / `showToast(msg)` — click-to-copy with toast
- `downloadAsMarkdown()` + helpers (`mdChildren`, `mdNode`, `mdInline`, `mdTable`) — converts all tab content to Markdown and downloads as `VibeCodingData.md`

## Content Conventions

Each tab maps to a topic (00–06). Content elements follow strict class naming:

| Class | Renders as |
|---|---|
| `code.copyable` | Block code — click to copy |
| `code.copyable-inline` | Inline code inside tables — click to copy |
| `code.plain` | Non-copyable inline code |
| `pre.code-block` | Non-copyable multi-line code block |
| `p.desc` | Standard paragraph |
| `p.sub-desc` | Indented paragraph (1 level) |
| `p.sub2-desc` | Indented paragraph (2 levels) |
| `p.note` | Red warning/notice text |
| `p.note-sub` | Red warning/notice, indented |
| `p.ref-title` | Red bold section label (참고 N >) |

The `downloadAsMarkdown()` function depends on these class names to produce correct Markdown output — keep them consistent when adding new content.
