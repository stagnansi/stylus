# Stylus Inter + IBM Plex Mono

A collection of Stylus userstyles that replace a website's default fonts with
something easier on the eyes.

Inter for sans-serif. IBM Plex Mono for monospace.

That's it.

## Why

Default fonts are fine. But they're not yours. If you spend hours staring at
text, you might as well make it look good.

I got tired of every website having its own opinion about typography. So I
wrote a stylesheet for each one. Per-site. No global override. Because global
selectors break more than they fix.

## What it does

- Swaps `sans-serif` for Inter. Falls back to `InterVariable` when variable
  font support is available. Uses `InterDisplay` for headings.
- Swaps `monospace` for IBM Plex Mono.
- Per-site. Each stylesheet targets one domain. GitHub gets GitHub selectors.
  Whatever comes next gets its own file.
- Hand-tuned selectors for GitHub: CodeMirror internals (`cm-editor`,
  `cm-scroller`, `cm-content`, `cm-line`, `cm-gutters`), `contenteditable`
  regions, blob code viewer classes, and React-generated class fragments.
- Metadata block so Stylus can show the style in its dashboard and check for
  updates.

## Styles

Currently:

- `github.user.css` — GitHub. Sans, mono, diffs, CodeMirror, blob viewer,
  markdown code blocks.

More when I get annoyed at other sites.

## Imports

Every stylesheet starts with these. They pull the fonts in so you don't have
to install anything locally.

```css
@import url('https://rsms.me/inter/inter.css');

@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;1,100;1,200;1,300;1,400;1,500;1,600;1,700&family=IBM+Plex+Sans:ital,wght@0,100..700;1,100..700&display=swap');
```

The first one is Inter from rsms.me. The canonical source. Gets you
`InterVariable` and `InterDisplay`.

The second is IBM Plex Mono from Google Fonts. All weights, all italics. It
also pulls IBM Plex Sans, which the styles don't currently use. It's just
there. Sitting quietly. Available if you want it.

## How to use it

1. Install Stylus in your browser. Chrome, Firefox, Edge, Opera. Pick your
   poison.
2. Open a `.user.css` file from this repo. Click Raw. Stylus will ask if you
   want to install it. Say yes.
3. That's it. The imports handle the fonts. No local installation needed.

## Repo structure

```
.
├── styles/
│   └── github.user.css
└── README.md
```

Every `.user.css` file starts with the imports and metadata block shown above.

## What it looks like

```css
@import url('https://rsms.me/inter/inter.css');

@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;1,100;1,200;1,300;1,400;1,500;1,600;1,700&family=IBM+Plex+Sans:ital,wght@0,100..700;1,100..700&display=swap');

@-moz-document domain("github.com") {
  span,
  h1,
  h2,
  h3,
  h4,
  h5,
  h6,
  input,
  textarea,
  a,
  button,
  p,
  ul,
  li,
  table,
  .text-italic {
    font-family: Inter, sans-serif;
    font-feature-settings: 'liga' 1, 'calt' 1; /* fix for Chrome */
  }

  @supports (font-variation-settings: normal) {
    span,
    h1,
    h2,
    h3,
    h4,
    h5,
    h6,
    input,
    textarea,
    a,
    button,
    p,
    ul,
    li,
    table,
    .text-italic {
      font-family: InterVariable, sans-serif;
    }
  }

  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    font-family: InterDisplay, sans-serif !important;
  }

  html body code,
  html body pre,
  html body kbd,
  html body samp,
  html body tt,
  html body .cm-editor,
  html body .cm-editor *,
  html body .cm-scroller,
  html body .cm-content,
  html body .cm-line,
  html body .cm-gutters,
  html body [contenteditable="true"],
  html body [contenteditable="plaintext-only"],
  html body .blob-code,
  html body .blob-code-inner,
  html body .markdown-body code,
  html body .markdown-body pre,
  html body [class*="CodeLine"] *,
  html body [class*="CodeText"] *,
  html body [class*="BlobContent"] *,
  html body [class*="CodeViewer"] * {
    font-family: "IBM Plex Mono", monospace !important;
  }
}
```

Some selectors above are trimmed. The real file has more — site-specific
classes I added by hand because GitHub keeps inventing new class names. If
something slips through, open devtools, grab the class, add it to the list.
That's the whole workflow.

## Metadata

Each `.user.css` file starts with a `==UserStyle==` block. Name, version,
author, license, update URL. Stylus reads it, shows it in the dashboard, and
uses it for auto-updates.

```css
/* ==UserStyle==
@name         GitHub — Inter + IBM Plex Mono
@namespace    github.com/stagnansi/stylus
@version      1.0.0
@description  Inter for sans-serif, IBM Plex Mono for monospace. Hand-tuned for GitHub.
@author       stagnansi
@homepageURL  https://github.com/stagnansi/stylus
@supportURL   https://github.com/stagnansi/stylus/issues
@updateURL    https://raw.githubusercontent.com/stagnansi/stylus/main/styles/github.user.css
@license      CC0-1.0
==/UserStyle== */
```

## Customization

- Change `--font-sans` and `--font-mono` to whatever you want.
- Remove `@-moz-document` blocks to exclude specific domains.
- Add `[class*="..."]` selectors when a site fights back.
- Fork it and make it yours.

## Fallbacks

| Role       | Primary               | Fallback                           |
|------------|-----------------------|------------------------------------|
| Sans-serif | Inter / InterVariable | system-ui, -apple-system, Roboto   |
| Display    | InterDisplay          | Inter, sans-serif                  |
| Monospace  | IBM Plex Mono         | Fira Code, JetBrains Mono, Menlo   |

## License

CC0 1.0 Universal. Public domain. No rights reserved.
