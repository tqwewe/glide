# Glide - a modern mdBook theme

A clean, modern theme for [mdBook](https://rust-lang.github.io/mdBook/), inspired by
contemporary documentation sites. It features a full-width sticky header with branding
and search, a refined collapsible sidebar, a right-hand "On this page" outline with
scroll-spy, callouts, code blocks with copy buttons, and a tasteful light/dark palette.

**[Live demo →](https://umari.tqwewe.com)** - the [Umari](https://umari.tqwewe.com) docs
are built with Glide.

This repository is also a live demo: the `src/` book renders the theme so you can preview
it locally with `mdbook serve`.

## Preview

```bash
mdbook serve --open
```

## Using the theme in your own book

Copy the `theme/` directory into your book and reference its files from `book.toml`:

```toml
[output.html]
default-theme = "light"
preferred-dark-theme = "navy"          # "navy" is restyled as the Glide dark palette
additional-css = ["theme/glide.css"]
additional-js = ["theme/glide.js"]
no-section-label = true                # cleaner sidebar (no "1." prefixes)

[output.html.fold]
enable = true
level = 1
```

Also copy these theme overrides (they sit alongside the defaults):

- `theme/index.hbs` - the page template (branded header, page-TOC slot, prev/next cards).
- `theme/head.hbs` - sets the optional version pill via `<meta name="glide-version">`.
- `theme/glide.css` - all theme styling (loaded as `additional-css`, layered over mdBook's defaults).
- `theme/glide.js` - progressive enhancements (loaded as `additional-js`).
- `theme/highlight.css`, `theme/tomorrow-night.css`, `theme/ayu-highlight.css` - syntax token colours.
- `theme/fonts/` - self-hosted IBM Plex Sans + JetBrains Mono (works offline).
- `theme/favicon.svg`.

## Design notes

- **Two themes.** A single sun/moon button in the header toggles `light` ⇄ `navy`. The theme
  is still driven by mdBook's own theme system (persisted in `localStorage`), so there is no
  flash on load.
- **Layered, not forked.** `glide.css`/`glide.js` build on top of mdBook's stock `book.js` and
  CSS rather than replacing them, so the theme keeps working across mdBook updates.
- **Callouts** use GitHub-style alerts:

  ```markdown
  > [!NOTE]
  > Text here.
  ```

  Supported: `NOTE`, `TIP`, `IMPORTANT`, `WARNING`, `CAUTION`.
- **Code block labels** show the fenced language (e.g. ```` ```ts ````). Every block gets a
  copy button.
- **Version pill.** Edit the `<meta name="glide-version">` value in `theme/head.hbs`, or remove
  it to hide the pill.

Fonts are bundled from [Fontsource](https://fontsource.org/) (IBM Plex Sans, JetBrains Mono).

## License

Licensed under either of

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE))
- MIT license ([LICENSE-MIT](LICENSE-MIT))

at your option.

The bundled fonts (IBM Plex Sans, JetBrains Mono) are distributed under the
[SIL Open Font License](https://openfontlicense.org/).
