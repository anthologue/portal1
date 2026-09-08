# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Stack & Conventions

This project has two hard constraints that must never be violated:

1. **Single-file project.** The entire project must live in one `index.html`
   file, with all CSS inlined in `<style>` tags and all JavaScript inlined in
   `<script>` tags — never in separate `.css` or `.js` files, and never split
   across additional HTML pages. Linking to external images, CSS libraries,
   and JavaScript libraries (e.g. via `<link>`/`<script src>` to a CDN) is
   allowed. This constraint exists so the finished project can be copy-pasted
   as a single file for sharing in class and on single-file code platforms
   (e.g. CodePen, JSFiddle).
2. **Vanilla only.** Use plain HTML, CSS, and JavaScript only — no frameworks
   or libraries bundled into the project (React, Vue, jQuery, Tailwind build,
   etc.), and no build step (no bundlers, transpilers, or package managers).
   Referencing an external library via a CDN `<script>`/`<link>` tag is fine
   under constraint 1, as long as it doesn't require a build step.

When implementing any feature, keep all markup, styles, and scripts inside
`index.html`. Do not create separate `.css`/`.js` files or additional `.html`
pages.

## Tech stack (hard constraints — do not deviate)
- Vanilla HTML, CSS, and JavaScript only. No React, Vue, or any JS framework.
- Tailwind CSS for all styling (via CDN only).
- No backend, no database. Fully static site.
- A toggle for light and dark theme, with the choice remembered
  across visits.

## Design direction
Standing visual direction for the portal shell and every tool page (based on
the "Sky & Flight" direction, chosen from proposed options) — apply it to
everything already built and to anything added later, automatically, without
being asked again:
- Clean and minimal. Avoid visual clutter, decoration, or busy backgrounds.
- One calm accent color, used sparingly and consistently (e.g. for links,
  active states, and primary actions) — not multiple competing accents.
- Generous white space; don't crowd content.
- Consistent spacing scale and typography (font choices, sizes, weights)
  reused across the shell and every tool, so tools feel like one coherent
  site rather than pasted-together pages.

## Working conventions
- Before implementing any non-trivial feature, ask clarifying
  questions about scope, edge cases, and constraints first —
  don't propose a plan until you've asked.

## Feature Plan

A web portal for a beginner-to-aeronautics class: visitors browse and try
a growing collection of small interactive tools and learning artifacts.
Built to keep growing — new tools get added over time without restructuring
the portal shell.

### Data model
All in-memory in `index.html` (no backend/DB, per hard constraints).
- `TOOLS`: array of tool entries, each `{ id, title, description, render(container) }`
  (or an equivalent pattern — e.g. each tool's markup lives in a `<template>`
  and its behavior in a scoped init function keyed by `id`).
- `theme`: `"light" | "dark"`, persisted in `localStorage`.

### Key flows
- **Portal home**: grid/list of tool cards built from `TOOLS`; clicking a
  card shows that tool (e.g. via view switching within the single page).
- **Add a new tool** (repeated over time): append one entry to `TOOLS` plus
  its markup/logic — should not require touching the shell/nav code.
- **Theme toggle**: switch persists across visits via `localStorage`, applied
  on load before first paint to avoid flash.

### Phase 1 — Portal shell + Airfoil Visualizer
- Portal shell: header/nav, tool grid, theme toggle, routing between home
  and a single tool view — built to hold more than one tool.
- Tool: **Airfoil Visualizer** — interactive airfoil shape/behavior
  explorer for beginners (exact parameters/controls TBD, spec before
  building).
- Second phase-1 tool deferred — pick and spec once Airfoil Visualizer
  is done.

### Phase 2 — Second tool (TBD)
- Spec and build a second tool using the same "append to `TOOLS`" pattern,
  as a check that the shell holds up for a real second entry.

### Later phases
- Add further tools/lessons incrementally, one phase per tool (or small
  batch), each just adding entries — no shell changes expected.
