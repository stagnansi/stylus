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
  font support is available. Uses `InterDisplay` for headings where it matters.
- Swaps `monospace` for IBM Plex Mono on sites that need it.
- Per-site. Each stylesheet targets one domain. No global selectors.
- Hand-tuned selectors for each site. GitHub, Google, Google Play, Instagram,
  WhatsApp Web. More coming when I get annoyed at other sites.
- Metadata block in every file so Stylus can show it in the dashboard and
  check for updates.

## Styles

| Site | File | Sans | Mono |
|------|------|------|------|
| GitHub | `github.user.css` | Inter | IBM Plex Mono |
| Google Search | `google.user.css` | Inter | — |
| Google Play | `google-play.user.css` | Inter | — |
| Instagram | `instagram.user.css` | Inter | — |
| WhatsApp Web | `whatsapp.user.css` | Inter | IBM Plex Mono |

Sites without monospace just don't need it. Google Search doesn't render code.
Instagram doesn't either. When a site does — GitHub, WhatsApp — the mono
import comes along.

## Imports

Every stylesheet starts with these. Inter is always there. IBM Plex Mono only
when the site actually uses it.

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
│   ├── github.user.css
│   ├── google.user.css
│   ├── google-play.user.css
│   ├── instagram.user.css
│   └── whatsapp.user.css
└── README.md
```

Every `.user.css` file is standalone. Imports are duplicated on purpose so
each style works without depending on anything outside itself.

## What it looks like

```css
@import url('https://rsms.me/inter/inter.css');

@-moz-document domain("google.com") {
  .byrV5b,
  .VwiC3b,
  .yXK7lf,
  .p4wth,
  .r025kc {
    font-family: Inter, sans-serif;
    font-feature-settings: 'liga' 1, 'calt' 1, 'zero' 1, 'tnum' 1;
    /* fix for Chrome */
  }

  @supports (font-variation-settings: normal) {
    .byrV5b,
    .VwiC3b,
    .yXK7lf,
    .p4wth,
    .r025kc {
      font-family: InterVariable, sans-serif;
    }
  }
}
```

Selectors above are trimmed. The real files have more — site-specific classes
I add by hand because these sites keep inventing new class names. If something
slips through, open devtools, grab the class, add it to the list. That's the
whole workflow.

## Metadata

Each `.user.css` file starts with a `==UserStyle==` block. Name, version,
author, license, update URL. Stylus reads it, shows it in the dashboard, and
uses it for auto-updates.

```css
/* ==UserStyle==
@name         Google — Inter
@namespace    github.com/stagnansi/stylus
@version      1.0.0
@description  Inter for Google Search. No monospace needed.
@author       stagnansi
@homepageURL  https://github.com/stagnansi/stylus
@supportURL   https://github.com/stagnansi/stylus/issues
@updateURL    https://raw.githubusercontent.com/stagnansi/stylus/main/styles/google.user.css
@license      CC0-1.0
==/UserStyle== */
```

## Customization

- Change the font stacks to whatever you want.
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
