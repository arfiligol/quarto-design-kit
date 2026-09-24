# Quarto Design Kit

`0.1.0` is the first release candidate of the native Quarto HTML design kit,
validated with Quarto 1.10.18. Its visual contract remains CONVERGING until
explicitly accepted; the version does not imply semantic stabilization.

## Install

Install the reviewed release tag once `v0.1.0` is published. Quarto's GitHub
installer accepts branch and tag names, not commit SHA modifiers:

```bash
quarto add arfiligol/quarto-design-kit@v0.1.0
```

```yaml
format:
  qdk-html:
    toc: true
    code-copy: true
```

The GitHub installation lives at `_extensions/arfiligol/qdk`. It bundles local
Source Sans 3 body text, Schibsted Grotesk title/navigation UI, IBM Plex Mono code,
Lucide icons, Kit MIT license, and third-party notices. Source Sans 3 is the
intentional version-pinned Source Sans Pro successor adaptation in this
Quartz-on-Quarto candidate.
No CDN, Quartz runtime, Python runtime, analytics, or consumer data is added.

The Kit maps Quartz's typography, tokens, rhythm, links, code,
and callout shell onto Quarto's native navbar/sidebar/TOC and runtime. It does
not introduce Quartz's additional callout families or aliases: that would need
a separate public authoring syntax contract.

QDK is intended as a reusable design system for direct SCQ-repository
adoption. The theme Sass variables `$grid-sidebar-width` and `$grid-margin-width`
are 240px, `$grid-body-width` and `$grid-docked-body-width` are 630px, and
`$grid-column-gutter-width` is 1.5rem. One docked track rule in `qdk.scss`
uses those variables so the 630px measure stays centered between equal side
columns; consumers retain Quarto's responsive layout, navigation, and runtime
ownership.

## Customize and update

Keep consumer overrides outside the installed extension and make their final
token values explicit. A working pattern appears in
[examples/consumer-override.yml](examples/consumer-override.yml) and
[examples/styles.scss](examples/styles.scss); render the consumer to verify it.
For updates, install a newly reviewed version tag and commit the consumer's
updated `_extensions` copy. Do not rely on a moving branch or edit the installed
copy.

## Gallery and credits

Render the source gallery locally with `quarto render .`; it demonstrates
article/navigation/TOC/mobile reading, native callouts, tables, code, formulas,
and real saved notebook output. See [credits.qmd](credits.qmd),
[THIRD_PARTY.md](THIRD_PARTY.md), and [ASSET_MANIFEST.md](ASSET_MANIFEST.md).
