# Quarto Design Kit release plan

## Goal and state

This repository owns the `qdk-html` native Quarto HTML extension and its local
gallery. The **0.1.0 release candidate** targets Quarto 1.10.18. Its visual
semantics remain CONVERGING until explicit Human acceptance; a version number,
merge, or tag does not establish semantic stabilization or deployment.

## Ownership and interfaces

The extension is self-contained at `_extensions/qdk` and exposes one public
format name: `qdk-html`. Its token authority is `qdk.scss`: documented Quarto
Sass variables own color, type, callout color, code, navbar, sidebar, and grid
widths, and `scss:rules` applies the remaining Quartz-derived visuals without
importing a Quartz runtime. Schibsted Grotesk (400/700) owns titles and navigation UI;
Source Sans 3 (400/600 plus italic) is the locally pinned Source Sans Pro
successor used for body text; IBM Plex Mono owns code. Consumers own content, IA, execution,
math engine, viewer behavior, privacy, data, and navigation choices. The
gallery at this repository root is the source-backed evaluation surface.
The shared token authority distinguishes content dividers from quieter layout
dividers in each native theme; manual Markdown `---` is the opt-in content
divider, while sidebar and navigation boundaries use the layout token.
QDK is a reusable design-system candidate for direct SCQ-repository adoption.
Its layout contract is the theme variables `$grid-sidebar-width` and
`$grid-margin-width` at 240px, `$grid-body-width` and `$grid-docked-body-width`
at 630px, and `$grid-column-gutter-width` at 1.5rem. `$sidebar-border` is
false. One `scss:rules` track list restates the docked grid from those
variables so the 630px measure stays centered; Quarto's own formula would add
200px to the body and leave the spare space in a right-hand 5fr column. That
track rule is the residual coupling to Quarto's grid line names.

## Candidate behavior and failure boundaries

The candidate supplies local fonts/icons, Quartz-on-Quarto light and dark
tokens, accessible focus, and native Quarto callout styling. It does not replace Quarto collapse,
navigation, highlighting, copying, execution, or rendering runtimes. If the
extension cannot be resolved by Quarto, a consumer must fix its extension
reference; it must not silently fall back to a remotely hosted asset or a
Quartz runtime. Callout type determines color independent of nesting depth.
The five Quarto-native types are reproduced within their DOM boundary; Quartz's
additional twelve-family showcase/aliases are not exposed because doing so
would require a new authoring syntax transformer or public contract.

## Exclusions

No tests or CI are written while this scope is CONVERGING. This package does
not provide a website deployment, analytics, search, graphs,
backlinks, hover previews, robots, emoji, consumer APIs, or scientific
execution policy.

## Validation endpoint

Render this gallery and a clean consumer that installs the reviewed version tag,
including a documented Sass override. Inspect desktop/mobile and light/dark
native Quarto behavior, focus, overflow, callout nesting/collapse, navigation,
TOC and code-copy. Record factual outcomes in `VALIDATION.md`; those findings
are not Human acceptance gates.

## Consolidated visual regression checklist

Before a final candidate review, inspect the native Quarto surface in this
order: Callout geometry/rhythm (including nested and collapsed forms), Header
alignment and toggle visibility, Layout tracks with and without a TOC plus
mobile, Divider hierarchy, Typography rhythm, Code surface/overflow/copy, then
the combined light/dark system. This checklist is a CONVERGING review aid, not
an automated test suite or acceptance gate.
