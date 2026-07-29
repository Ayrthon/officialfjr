# MC FJR — Coming Soon

Single-page coming-soon site for **MC FJR** (Fajar Symons), Dutch MC & DJ.

Built with [Astro](https://astro.build). Static output, mobile-first, no build-time framework dependencies beyond Astro itself.

## Stack

- **Astro 5** — static site generator
- **Vanilla CSS** — custom-property driven, mobile-first
- **Google Fonts** — Space Grotesk (display) + JetBrains Mono (mono)
- **Zero JS** shipped to the client (pure static HTML/CSS)

## Getting started

Requires Node.js 18.20+, 20.3+, or 22+.

```powershell
# Install dependencies
npm install

# Start dev server (http://localhost:4321)
npm run dev

# Build for production (outputs to ./dist)
npm run build

# Preview the production build locally
npm run preview
```

## Project structure

```
mcfjr-site/
├── public/
│   ├── favicon.svg
│   └── robots.txt
├── src/
│   ├── layouts/
│   │   └── Layout.astro       # HTML shell, meta tags, fonts
│   ├── pages/
│   │   └── index.astro        # The coming-soon page
│   └── styles/
│       └── global.css         # Design system + all styles
├── astro.config.mjs
├── package.json
└── tsconfig.json
```

## Customization

Most tweaks live in two files:

- **`src/styles/global.css`** — colors, spacing, typography live in the `:root` custom properties at the top.
- **`src/pages/index.astro`** — copy, marquee items, and the bookings email.

### Change the accent color

In `src/styles/global.css`:

```css
:root {
  --accent: #00e5ff;           /* main accent */
  --accent-dim: rgba(0, 229, 255, 0.15);
  --accent-glow: rgba(0, 229, 255, 0.35);
}
```

### Update the bookings email

In `src/pages/index.astro`, find the `mailto:` link.

## Deployment — Netlify

Config lives in [`netlify.toml`](./netlify.toml): build command, publish directory, pinned Node version, and cache/security headers.

To connect:

1. Netlify dashboard → **Add new site** → **Import an existing project** → GitHub → pick `Ayrthon/officialfjr`.
2. Netlify will read `netlify.toml` — no manual build settings needed.
3. Deploy. First build takes ~30–60s.

Every push to `main` will trigger a new deploy automatically.

The `site` field in `astro.config.mjs` is set to `https://mcfjr.com` for canonical URLs — update it once the real domain is picked (Netlify subdomain or custom).
