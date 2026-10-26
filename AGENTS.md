## Development

When starting the dev server, use background mode:

```
astro dev --background
```

Manage the background server with `astro dev stop`, `astro dev status`, and `astro dev logs`.

There is no test suite. Verify changes with `npx astro build`, and for visual changes compare the pages in both light and dark mode.

## Project

Static legal site for legal.mss.io. It currently hosts the Terms of Use and Privacy Policy for auth.mss.io. See `README.md` for routes and file layout.

- `src/layouts/Layout.astro`: shared header, theme toggle and footer. Props: `title`, `width`, `headerPadding`. Named slots: `subnav` and `footer-links`. The footer's right-hand box only renders when `footer-links` is filled. "/ legal.mss.io" in the header is plain text on `/` and a link elsewhere.
- `src/components/PolicyNav.astro`: sub-nav for the policy pages, with `current: 'terms' | 'privacy'`. It is hardcoded to the auth.mss.io pages.
- `src/styles/global.css`: Tailwind v4 setup, with fonts, accent colors and the class-based `dark` variant.

## Conventions

- **Policy wording is the owner's.** Don't reword, reorder or "improve" policy text unless asked. When asked for a text change, change only that text.
- **Straight quotes** (`"`) everywhere. No curly quotes.
- **"Last updated" dates** live in `src/data/auth.ts` (`TERMS_LAST_UPDATED`, `PRIVACY_LAST_UPDATED`). Both the policy page subtitles and the home page rows read from there, so never hardcode a date in a page.
- **The contact email is auth-only.** `AUTH_CONTACT` in `src/data/auth.ts` belongs on the auth.mss.io pages, never on the home page or another service's pages. Render it with `<AuthEmail class="…" />` (`src/components/AuthEmail.astro`), passing only the size/color utilities for that spot. Never type the address.
- **Inline links in policy text** use the `text-link` utility from `global.css` (underline, underline color, accent hover). Add only the size/color/offset utilities a spot needs on top.
- **Favicon:** `public/favicon.svg` is the source. `public/favicon.ico` is a fallback rendered from it in the light-mode blue. Regenerate the `.ico` if the SVG changes.
- **Tailwind v4, installed via `@tailwindcss/vite`.** Never add the Tailwind CDN. Dark mode uses `dark:` utilities, driven by a `dark` class on `<html>`. The only custom colors are `accent` (light) and `accent-dark` (dark mode). Add new tokens to `@theme` in `global.css` only when something uses them.
- **Theme persistence.** The theme is stored in `localStorage` under `color-theme`. Keep every storage access wrapped in `try/catch`.
- **Keep it simple.** The site is static, with no UI framework, no content collections and no extra dependencies unless they're needed.
- `.private/` (gitignored) holds the original Stitch HTML exports and screenshots. They are the visual reference for the design.

## Documentation

Full documentation: https://docs.astro.build

Consult these guides before working on related tasks:

- [Adding pages, dynamic routes, or middleware](https://docs.astro.build/en/guides/routing/)
- [Working with Astro components](https://docs.astro.build/en/basics/astro-components/)
- [Using React, Vue, Svelte, or other framework components](https://docs.astro.build/en/guides/framework-components/)
- [Adding or managing content](https://docs.astro.build/en/guides/content-collections/)
- [Adding styles or using Tailwind](https://docs.astro.build/en/guides/styling/)
- [Supporting multiple languages](https://docs.astro.build/en/guides/internationalization/)
