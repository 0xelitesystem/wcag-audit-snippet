# wcag-audit-snippet

Quick heuristic WCAG checks for any web page. Single HTML file plus a bookmarklet you can drag to your bookmarks bar to audit any site you visit.

**Live demo:** https://0xelitesystem.github.io/wcag-audit-snippet/

## Why

Real accessibility audits with axe-core, WAVE, and screen readers are essential, but they take 30 minutes per page. This catches the 80% of issues that those tools would also flag, in 100ms, on any page.

Use this for:
- Quick first-pass during dev
- Spot-checking a page after changes
- Auditing pages you don't own (with the bookmarklet)
- Teaching: the bookmarklet's findings are educational

## Use it

Open `index.html` in any browser, or visit the hosted demo at `https://0xelitesystem.github.io/wcag-audit-snippet/` once Pages is enabled.

**Three ways to run a check:**

1. **Bookmarklet**: drag the "WCAG Audit" link to your bookmarks bar. Click it on any page.
2. **Paste HTML**: paste any HTML into the textarea on the demo page and click Audit.
3. **"Load example"**: see the tool find issues in a sample page with deliberate problems.

## What it checks

| Severity | Check |
|---|---|
| Blocker | Missing alt text on `<img>` |
| Blocker | Form controls without labels (no `<label for>`, no `aria-label`, not wrapped) |
| Blocker | Links without text, aria-label, or alt-text-bearing image |
| Blocker | Buttons without text or aria-label |
| Major | Missing `lang` attribute on `<html>` |
| Major | Missing `<title>` |
| Major | Inline-style color contrast under 4.5:1 |
| Major | Empty `<a>` or `<button>` (whitespace only) |
| Major | Page has headings but no `<h1>` |
| Minor | First heading is not `<h1>` |
| Minor | Heading levels skipped (h1 → h3) |

Each finding includes a CSS selector pointing to the offending element and a concrete fix suggestion.

## What it doesn't check

- **Computed styles** (only inline `style=""` attributes for contrast). Tools that run in-page like axe-core can read computed styles; this tool runs against parsed HTML strings.
- ARIA validity (e.g. invalid roles, role-attribute mismatches)
- Keyboard navigation order
- Focus-visible behavior
- Animations and motion
- Language of parts (lang on inline elements)

For those, use [axe-core](https://github.com/dequelabs/axe-core) or the browser DevTools Accessibility panel.

## How the bookmarklet works

The bookmarklet wraps the same check functions in a self-executing script that runs against `document` of whatever page you click it from. Findings render in a fixed-position panel on the page itself. Click the X to dismiss.

The bookmarklet code is around 2.5 KB minified. If your browser has a strict CSP that blocks `javascript:` URLs, the bookmarklet won't run on those pages, that's by design (CSP is doing its job).

## Tech

- Single HTML file, ~700 lines
- Vanilla JS, no frameworks, no dependencies
- Uses `DOMParser` to audit pasted HTML safely
- Light and dark themes with OS preference detection

## License

MIT. See [LICENSE](LICENSE).

## Related

- [dark-mode-tester](https://github.com/0xelitesystem/dark-mode-tester), preview a page in light/dark/auto
- [csp-builder](https://github.com/0xelitesystem/csp-builder), build CSP headers visually
- [readme-slop-checker](https://github.com/0xelitesystem/readme-slop-checker), audit a README for AI cliches
