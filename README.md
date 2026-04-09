# New New Tab

A browser extension that replaces the new-tab page with a customizable bookmark dashboard. Tabs and bookmarks are configured via a GitHub Gist, so you can update your layout from anywhere without rebuilding the extension.

## How it works

When you open a new tab, the extension loads your configuration from a [GitHub Gist](https://gist.github.com/maxeonyx/fa60371050c93cc141fc0b2086bec30f). The gist contains JSON files — one per profile — that define tabs, bookmarks (with names, links, and icons), and a background image URL. The config is cached in localStorage so the page loads instantly, and there's a refresh button to pull the latest from the gist.

The UI is a header bar with tab navigation over a full-bleed background image, with bookmark cards displayed as a grid. It uses backdrop-filter for a frosted glass effect where supported.

There's also a multi-profile system — if you have multiple JSON files in the gist, you pick which profile to use on first load.

## Building

Requires Node.js and Yarn.

```
yarn install
yarn build
```

The built extension ends up in `dist/`.

## Installing

After building, load the `dist/` directory as a temporary extension:

- **Firefox:** Go to `about:debugging#/runtime/this-firefox` → "Load Temporary Add-on" → select any file in `dist/`
- **Chrome:** Go to `chrome://extensions` → enable Developer Mode → "Load unpacked" → select the `dist/` directory

## Development

```
yarn serve
```

Runs the page with hot-reload at `localhost:8080`. Useful for iterating on the layout, but the extension manifest features (new-tab override, search provider) only work when loaded as an actual extension.
