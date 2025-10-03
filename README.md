# BibleGateway Dark Mode

A small Chrome/Edge extension that toggles a readable dark theme on BibleGateway.com.

## What it does

- Injects a lightweight CSS style into pages on `www.biblegateway.com` to provide a dark reading theme.
- Stores the enabled/disabled state in extension storage so the choice persists between sessions.
- Updates the extension action icon when toggled.

## Features

- Toggle dark mode from the popup.
- Works on all BibleGateway pages (content script set to `*://www.biblegateway.com/*`).
- Minimal and non-destructive: styles are injected/removed dynamically.

## Install (developer / local)

1. Open Chrome (or Edge) and go to `chrome://extensions/`.
2. Enable **Developer mode** (top-right).
3. Click **Load unpacked** and select this repository folder (for example `C:\Users\pamus\Documents\Extensions\BibleGatewayDarkMode`).
4. Open a BibleGateway page and click the extension icon to open the popup. Use the "Toggle Dark Mode" button.

Tip: After changing code, click the reload icon for the extension on the extensions page to load changes.

## Files

- `manifest.json` - Extension manifest (MV3) with permissions and content script configuration.
- `content.js` - Injects and removes the dark-mode CSS, listens to storage and runtime messages.
- `popup.html` / `popup.js` - Popup UI and logic to toggle the setting and notify the content script.
- `background.js` - Small service worker that updates the extension icon when the mode changes.
- `icon.png`, `icon2.png` - Icons used for enabled/disabled states.

## Development notes

- The extension uses `chrome.storage.local` to persist `bgDarkEnabled` (boolean).
- The content script creates a single `<style>` element and appends/removes it; this avoids duplicating styles across navigations.
- Manifest v3 is used; the background is a service worker (`background.js`).

### Edge cases / considerations

- If a site update changes markup/classes, you can extend or adjust the CSS rules in `content.js`.
- The extension targets only `www.biblegateway.com` by default; change `matches` in `manifest.json` to widen scope.

## Troubleshooting

- If the button doesn't seem to work: reload the extension on `chrome://extensions/`, then reload the BibleGateway tab.
- If styles don't apply: open DevTools on the page and check for console errors or whether the `<style>` element is present in `<head>`.
- Icon doesn't change: ensure the service worker is running (reload extension) and that `background.js` ran without errors.

## Contributing

Small fixes, better CSS targeting, or more robust toggling logic are welcome. Open a PR with a clear description.

## License

This repository currently has no explicit license. If you want this to be open-source, add a `LICENSE` file (MIT or similar).
