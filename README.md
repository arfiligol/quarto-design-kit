# Quarto Design Kit

`0.1.0-dev` is an installable development candidate for native Quarto HTML,
validated with Quarto 1.10.18. It is CONVERGING: it is neither a stable release
nor an accepted visual contract.

## Install

Use the exact development revision below. `CANDIDATE_COMMIT` must be replaced
with the frozen `develop` commit before sharing this command:

```bash
quarto add arfiligol/quarto-design-kit@CANDIDATE_COMMIT
```

```yaml
format:
  qdk-html:
    toc: true
    code-copy: true
```

The extension is self-contained at `_extensions/qdk`: it bundles local Source
Sans 3 body text, Schibsted Grotesk title/navigation UI, IBM Plex Mono code,
Lucide icons, Kit MIT license, and third-party notices. Source Sans 3 is the
intentional version-pinned Source Sans Pro successor adaptation in this
Quartz-on-Quarto candidate.
No CDN, Quartz runtime, Python runtime, analytics, or consumer data is added.

The current candidate maps Quartz's typography, tokens, rhythm, links, code,
and callout shell onto Quarto's native navbar/sidebar/TOC and runtime. It does
not introduce Quartz's additional callout families or aliases: that would need
a separate public authoring syntax contract.

QDK is intended as a reusable design-system candidate for direct SCQ-repository
adoption. Its native article-grid defaults are a 260px sidebar, 960px body,
240px margin, and 2.5rem gutter, with the actual reading document centered at
a Quartz-derived 630px measure; consumers retain Quarto's responsive layout,
navigation, and runtime ownership.

## Customize and update

Keep consumer overrides outside the installed extension and make their final
token values explicit. A working pattern appears in
[examples/consumer-override.yml](examples/consumer-override.yml) and
[examples/styles.scss](examples/styles.scss); render the consumer to verify it.
For updates, install a newly reviewed exact revision and commit the consumer's
updated `_extensions` copy. Do not rely on a moving branch or edit the installed
copy.

## Gallery and credits

Render the source gallery locally with `quarto render .`; it demonstrates
article/navigation/TOC/mobile reading, native callouts, tables, code, formulas,
and real saved notebook output. See [credits.qmd](credits.qmd),
[THIRD_PARTY.md](THIRD_PARTY.md), and [ASSET_MANIFEST.md](ASSET_MANIFEST.md).

本 Quarto Design Kit 的視覺設計大量參考 Quartz，並將部分樣式適配至 Quarto；具體來源與修改紀錄列於第三方來源清單。
