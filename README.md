# TW-Tiny-Bootstrap

**English** · [Français](README.fr.md)

![Status](https://img.shields.io/badge/status-experimental-orange)
![TiddlyWiki](https://img.shields.io/badge/TiddlyWiki-%E2%89%A55.3.5-blue)

A TiddlyWiki plugin bundling Bootstrap 5.3.3's utility and component CSS classes — no JavaScript, pure `class="..."` styling. Self-disables when [Shiraz](https://github.com/kookma/TW-Shiraz) is installed and enabled, since Shiraz already ships the same classes.

## Overview

Extracted from Shiraz's `styles/bs/` folder (24 stylesheets: sizing, spacing, borders, rounded corners, colours, shadows, alerts, badges, buttons, cards, etc.). Usable on any element — tables, `<div>`, headings — not just Shiraz's own widgets.

## Installation

1. Download `TW-Tiny-Bootstrap-Plugin.json` from the [latest release](https://github.com/nikorion/TW-Tiny-Bootstrap/releases/latest)
2. Drag and drop it into your TiddlyWiki (≥ 5.3.5)
3. Save and reload

## Development

```
pnpm install
pnpm dev      # dev wiki + hot reload; the URL (random free port) is printed on start
pnpm build    # generates dist/TW-Tiny-Bootstrap-Plugin.json + docs/TW-Tiny-Bootstrap-Wiki.html
```

Sources are in `src/tiny-bootstrap/`.

## Files

| File | Role |
|---|---|
| `src/tiny-bootstrap/plugin.info` | Plugin metadata |
| `src/tiny-bootstrap/styles/gate.tid` | Self-disable gate (checks for Shiraz), only tiddler tagged `$:/tags/Stylesheet` |
| `src/tiny-bootstrap/styles/*.css` | The 24 Bootstrap stylesheets (untagged, transcluded by `gate.tid`) |

## Version history

### v0.1.0

Initial release — Bootstrap utility/component CSS extracted from Shiraz into its own, self-disabling plugin.

## Credits

Developed with assistance from Anthropic Claude for code, review, and documentation.

## License

MIT License — see `LICENSE`. Bundles a subset of Bootstrap 5.3.3 (MIT), repackaged via Shiraz (MIT).
