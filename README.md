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

- Swaps `sans-serif` across the board for Inter.
- Swaps `monospace` across the board for IBM Plex Mono.
- Targets `code`, `pre`, `kbd`, `samp`, and `textarea` so your terminal
  snippets and documentation actually look like code.
- Works on most sites. GitHub, Stack Overflow, docs pages, forums. The usual
  suspects.

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
@-moz-document regexp(".*") {
  :root {
    --font-sans: "Inter", system-ui, -apple-system, sans-serif;
    --font-mono: "IBM Plex Mono", "Fira Code", monospace;
  }

  body, input, button, select, textarea {
    font-family: var(--font-sans) !important;
  }

  code, pre, kbd, samp, tt {
    font-family: var(--font-mono) !important;
  }
}
```

Simple. Works.

## Font loading

If you don't want to install fonts locally, add this to the top of your
stylesheet:

```css
@import url('https://fonts.googleapis.com/css2?family=Inter&family=IBM+Plex+Mono&display=swap');
```

I don't. But you can.

## Customization

- Change `--font-sans` and `--font-mono` to whatever you want.
- Remove `@-moz-document` blocks to exclude specific domains.
- Fork it and make it yours.

## Fallbacks

| Role       | Primary        | Fallback                           |
|------------|----------------|------------------------------------|
| Sans-serif | Inter          | system-ui, -apple-system, Roboto   |
| Monospace  | IBM Plex Mono  | Fira Code, JetBrains Mono, Menlo   |

## License

CC0 1.0 Universal. Public domain. No rights reserved.
