# Stylus Inter + IBM Plex Mono

A collection of Stylus userstyles that replace a website's default fonts with
something easier on the eyes.

Inter for sans-serif. IBM Plex Mono for monospace.

That's it.

## Why

Default fonts are fine. But they're not yours. If you spend hours staring at
text, you might as well make it look good.

I got tired of every website having its own opinion about typography. So I
wrote one stylesheet and let it handle the rest.

## What it does

- Swaps `sans-serif` across the board for Inter. Falls back to `InterVariable`
  when variable font support is available. Uses `InterDisplay` for headings.
- Swaps `monospace` across the board for IBM Plex Mono.
- Targets the usual suspects: `code`, `pre`, `kbd`, `samp`, `tt`, plus
  CodeMirror internals (`cm-editor`, `cm-scroller`, `cm-content`, `cm-line`,
  `cm-gutters`), `contenteditable` regions, and GitHub's blob/code viewer
  classes.
- Includes some hand-tuned site-specific class selectors. Because some sites
  just won't cooperate.

## How to use it

1. Install Stylus in your browser. Chrome, Firefox, Edge, Opera. Pick your
   poison.
2. Make sure Inter and IBM Plex Mono are installed on your system. Or don't.
   See "Font loading" below.
3. Open a `.user.css` file from this repo. Click Raw. Stylus will ask if you
   want to install it. Say yes.

## Repo structure

```
.
├── styles/
│   ├── global.user.css          # Every website, no exceptions
│   ├── github.user.css          # Just GitHub
│   └── stackoverflow.user.css   # Just Stack Overflow
├── snippets/
│   └── font-face-import.css     # Google Fonts, if you're into that
└── README.md
```

## What it looks like

```css
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
```

Some selectors above are trimmed. The real file has more — site-specific
classes I added by hand because GitHub, React, and friends keep inventing new
class names. If something slips through, open devtools, grab the class, add it
to the list. That's the whole workflow.

## Font loading

If you don't want to install fonts locally, add this to the top of your
stylesheet:

```css
@import url('https://fonts.googleapis.com/css2?family=Inter&family=IBM+Plex+Mono&display=swap');
```

I don't. But you can. Variable font (`InterVariable`) and `InterDisplay` need
to be installed locally anyway.

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
