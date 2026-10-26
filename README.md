# legal.mss.io

Legal policies for services operated by MSS. A static [Astro](https://astro.build) site styled with Tailwind CSS v4.

## Pages

| Route           | Page                               | File                          |
| :-------------- | :--------------------------------- | :---------------------------- |
| `/`             | Legal home, lists policies by service | `src/pages/index.astro`    |
| `/auth/terms`   | auth.mss.io Terms of Use           | `src/pages/auth/terms.astro`   |
| `/auth/privacy` | auth.mss.io Privacy Policy         | `src/pages/auth/privacy.astro` |

## Project structure

```text
/
├── public/
│   ├── favicon.ico            # fallback for browsers/tools without SVG icons
│   └── favicon.svg            # shield icon, follows the OS light/dark setting
├── src/
│   ├── components/
│   │   └── PolicyNav.astro    # "Back to Legal" + Terms / Privacy tabs
│   ├── data/
│   │   └── auth.ts            # auth.mss.io contact address and "Last updated" dates
│   ├── layouts/
│   │   └── Layout.astro       # header, theme toggle, footer
│   ├── pages/
│   │   ├── index.astro
│   │   └── auth/
│   │       ├── terms.astro
│   │       └── privacy.astro
│   └── styles/
│       └── global.css         # Tailwind import, fonts, accent colors, dark mode variant
└── package.json
```

Policy text lives directly in the page files. There is no CMS or content collection.

## Commands

All commands are run from the root of the project:

| Command           | Action                                       |
| :---------------- | :------------------------------------------- |
| `npm install`     | Install dependencies                         |
| `npm run dev`     | Start the dev server at `localhost:4321`     |
| `npm run build`   | Build the static site to `./dist/`           |
| `npm run preview` | Preview the build locally before deploying   |

## Editing policies

- When a policy changes, update its "Last updated" date in `src/data/auth.ts`. The policy page and the home page both read it from there.
- The auth.mss.io contact address is also set once in `src/data/auth.ts` (`AUTH_CONTACT`).
- Use straight quotes (`"`), not curly quotes.
- The contact address belongs to auth.mss.io only. Keep it off the home page and out of other services' pages.

## Adding a policy page

1. Create `src/pages/<service>/<page>.astro` using `Layout` with `width="max-w-[760px]"` and `headerPadding="pb-10 sm:pb-12"`, like the existing auth pages.
2. Add the sub-nav and a link to the sibling policy in the `footer-links` slot.
3. Add a row for it on the home page under a section for that service.

`PolicyNav` currently only knows the auth.mss.io Terms and Privacy tabs. A new service needs it to take its tabs as a prop.
