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
