# Candidate validation receipt

Date: 2026-09-23. Semantic state: **CONVERGING**. These observations are
technical evidence, not Human acceptance thresholds or visual acceptance.

## Toolchain and scope

- Quarto `1.10.18` rendered the local gallery.
- A temporary, isolated Python 3.13 virtual environment supplied Jupyter only
  for local gallery validation; it is not a repository or extension dependency.
- `notebooks/simple-output.ipynb` was executed by `jupyter nbconvert --execute
  --inplace`; its saved output is `Saved notebook output: [3, 5, 8] -> 16`.
- No durable tests, CI configuration, release artifacts, or deployment files
  were added.

## Commands and factual results

```bash
PATH=/tmp/qdk-render-venv/bin:$PATH quarto render .
```

Succeeded: all gallery pages rendered, including executed
`notebook-output.qmd`; `_site/index.html` contains
`#mobile-callout-inspection-target` and the rendered output contains the saved
notebook result.

The Human-selected Quartz-on-Quarto revision also rendered successfully with
the same command: compiled light/dark styles contain the Quartz token values,
and the gallery ships local Schibsted Grotesk 400/700 alongside Source Sans 3
body and IBM Plex Mono code faces.

After browser review identified Quarto default-callout specificity leakage, the
candidate was rerendered with `.callout.callout-style-*` shell overrides:
compiled CSS confirms the uniform 1px semantic-alpha border, 6.3% semantic
shell fill, transparent header, 5px radius, 1rem horizontal shell padding, and
Quartz warning `#db8942`. A browser surface was unavailable to this worker for
a replacement screenshot; owner browser review remains the visual receipt.

The gallery's native titleless/iconless simple callout now renders as
`title=""` plus Quarto's `no-icon` DOM class, with no title container; QDK
explicitly hides that native no-icon container. Dark navigation surfaces now
resolve through `--qdk-canvas` and `--qdk-border`; clean-consumer installation
and Sass override rendering were rerun successfully.

Nested final children now receive an explicit `1rem` bottom margin through a
type/appearance-specific selector. Collapsible Quarto headers use `.75rem`
block padding while ordinary headers retain `1rem`; title, icon, and chevron
are direct flex items with `align-self: center`. These are authored geometry
values verified in compiled CSS and DOM; browser-computed light/dark geometry
remains an owner-side visual receipt.

The dark-theme code correction was rerendered in `qdk-dark.scss` only. Quarto
switches theme stylesheets without changing the body class, so its compiled
dark-only selectors are intentionally unprefixed: `div.sourceCode` and source
`pre` resolve to `#1f1f22` with a `#393639` border and `#d4d4d4` plain text.
Pandoc comments, keywords/operators, strings/numbers, functions, and
builtins/types resolve respectively to `#8b949e`, `#ff7b72`, `#a5d6ff`,
`#d2a8ff`, and `#79c0ff`. The light stylesheet has no corresponding rules, so
the light code palette remains unchanged. Browser-computed values and
copy-control icon pixels remain owner-side visual inspection evidence.

The common code-shell rule now assigns the visible border and 5px radius to
`div.sourceCode` (with `pre` retained as a standalone fallback). For Quarto's
normal nested structure, `div.sourceCode > pre.sourceCode` and its direct
`code.sourceCode` are explicitly transparent with zero border/radius/shadow;
the dark layer applies `#393639` only to that outer wrapper. Gallery and clean
consumer rendering were rerun after this correction.

The common stylesheet also clears Quarto's automatic H2 border and bottom
padding (including heading pseudo-elements) without depending on the active
theme. Explicit `hr` elements instead render as a 1px top border using
`--qdk-border`; `components.qmd` demonstrates the opt-in native Markdown
sequence of a heading, blank line, and `---`. Browser-computed confirmation in
both stylesheet modes remains owner-side visual evidence.

The divider hierarchy was rerendered with explicit theme tokens. Light content
and layout dividers are respectively `rgba(43, 43, 43, .18)` and
`rgba(43, 43, 43, .08)`; dark values are `rgba(212, 212, 212, .24)` and
`rgba(212, 212, 212, .10)`. The manual `hr` uses the content token at 1px with
`opacity: 1`; mobile/offcanvas inline-end boundaries stay transparent. The
desktop docked sidebar no longer draws a layout-token seam, so the side
columns share the article canvas.

The native article-grid defaults now compile from `$grid-sidebar-width` and
`$grid-margin-width` at 240px, `$grid-body-width` and `$grid-docked-body-width`
at 630px, and `$grid-column-gutter-width` at 1.5rem. `$sidebar-border` is
false, so the desktop docked sidebar does not draw a layout seam. Quarto's
docked formula still widens the body by 200px and leaves spare space in a
right-hand flexible column, so one `qdk.scss` rule restates the desktop docked
grid from those variables: outer flexible tracks, 240px side columns, 1.5rem
gutters, and a 630px measure. `#quarto-document-content`
is a 630px-or-less box with `justify-self: center` and auto inline margins, so
it fills that track and stays centered between the side columns. Navbar rules
center the native container and tools as flex items at desktop width; below
992px the collapse keeps Bootstrap's hidden menu instead of a forced flex row.
Links use a 1.25 line-height with `.25rem` block padding. Article list rhythm
is scoped to `#quarto-document-content`, with the navbar list explicitly reset
to zero block margin so Quarto navigation cannot inherit article spacing.
Desktop links are `.9rem`/400 (active 600) against the `.98rem`/700 brand;
mobile links are `.85rem`. The theme toggle is a 28px control that shows a
sun in the light scheme and a moon in the dark scheme, both painted with
`currentColor`. The callout disclosure is a centered chevron in the same
color as its title. Post-change browser center/contrast measurements remain
owner-side visual evidence.

```bash
quarto add <temporary-qdk-extension.zip> --no-prompt
quarto render .
```

Succeeded in a fresh temporary consumer using
`examples/consumer-override.yml`: its compiled stylesheet contains
`--qdk-link: #2D5E85`; the installed extension contains `licenses/QDK-MIT.txt`
and `assets/fonts/SourceSans3VF-Upright.ttf.woff2`. The Quartz revision
additionally confirmed `assets/fonts/SchibstedGrotesk-Regular.woff2` and
`licenses/Schibsted-Grotesk-OFL.txt`. Its rendered CSS resolves
those local files relative to the installed extension; no CDN is involved.

Asset SHA-256 values and immutable source URLs/revisions are recorded in
`ASSET_MANIFEST.md` and `THIRD_PARTY.md`. Quarto output contains both native
light/dark stylesheet alternatives and the color-scheme toggle script.
Website search is explicitly disabled in `_quarto.yml`; the rendered page has
no search control or `search.json` index.

## Pending manual inspection

The consolidated visual review order is Callout, Header, Layout, Divider,
Typography, Code, then final light/dark system behavior. This current pass
addresses Callout geometry/rhythm only; the remaining entries must be reviewed
as a system after their respective candidate changes settle.

Browser inspection remains required for actual desktop/mobile visual behavior,
keyboard focus traversal, collapse/copy interaction, and clipping/overflow.
Contrast has not been measured; no acceptance threshold is asserted. The
loopback preview is `http://127.0.0.1:4568/` (Quarto preview service); a
2026-09-23 loopback `curl -I` returned `HTTP/1.1 200 OK` with the gallery title.

Quartz's full additional callout aliases remain an explicit limitation: the
candidate faithfully styles Quarto's five native types, nesting, and collapse;
adding the other Quartz authoring names requires a separate public syntax
transformer contract.
