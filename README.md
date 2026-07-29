# OFFICIAL FJR — Open Format DJ & MC

Single-page personal brand site for **FJR** (Fajar Symons), Open Format DJ & MC based in The Netherlands.

Built with [Astro](https://astro.build). Static output, mobile-first, zero client-side framework runtime.

## Stack

- **Astro 5** — static site generator
- **Vanilla CSS** — custom-property driven, mobile-first, scoped per component
- **Google Fonts** — Space Grotesk (display) + JetBrains Mono (mono)
- **Netlify Forms** — booking form submissions land in the Netlify dashboard, zero backend
- **~5KB of client JS total** (mobile menu toggle + reveal-on-scroll + scroll-spy nav)

## Sections

Single-page scroll layout. Nav anchors map to these `<section>` ids:

| Anchor          | Section                                                         |
| :-------------- | :-------------------------------------------------------------- |
| `#home`         | Hero with tagline + Book Now / Download Presskit CTAs           |
| `#about`        | Bio + "Based in The Netherlands. Available Worldwide."          |
| —               | Genres grid (9 icon cards)                                      |
| `#experience`   | Experience grid (Festivals, Clubs, Corporate, Private, Asia, UK)|
| `#gallery`      | 6-tile photo grid                                               |
| `#videos`       | 4 video thumbnails with play overlay                            |
| —               | Testimonials (3 quote cards with 5-star ratings)                |
| `#presskit`     | Presskit download card                                          |
| `#contact`      | Booking form (Netlify Forms) with name/email/date/location/etc. |

Plus a `/thanks` page users are redirected to after a successful booking submission.

## Getting started

Requires Node.js 18.20+, 20.3+, or 22+ (Netlify build pins Node 22).

```powershell
npm install
npm run dev       # http://localhost:4321
npm run build     # outputs to ./dist
npm run preview   # preview the production build locally
```

## Placeholder assets — what to swap before launch

Every image on the site is currently a styled placeholder block clearly labeled "Photo — …". They're deliberately visible so nothing accidentally ships as final.

Replace them by editing these components and swapping the `<Placeholder … />` calls for `<img …>` (or Astro's `<Image />` component if you install `@astrojs/image`):

| Component                             | Placeholders                                                       |
| :------------------------------------ | :----------------------------------------------------------------- |
| `src/components/Hero.astro`           | Full-screen background photo (crowd + performer)                   |
| `src/components/About.astro`          | DJ-at-the-deck photo (4:3)                                         |
| `src/components/Experience.astro`     | 6 event-type thumbnails (4:3)                                      |
| `src/components/Gallery.astro`        | 6 stage photos (4:3, tiles 1 & 6 span 2 cols on desktop)           |
| `src/components/Videos.astro`         | 4 video thumbnail backgrounds + real YouTube/Vimeo `href`s + durations |
| `src/components/BookingForm.astro`    | Portrait MC-on-the-mic photo (3:4)                                 |
| `public/presskit.pdf`                 | The actual presskit PDF (currently 404s — "Download Presskit" button links here) |

Also swap these text/URL placeholders in `src/components/Footer.astro`:

- Real phone number (currently `+31 6 12345678`)
- Real booking email (currently `bookings@officialfjr.com`)
- Real socials (TikTok, YouTube, Spotify, SoundCloud, LinkedIn currently all `#`)

## Customization

Design tokens live at the top of `src/styles/global.css`:

```css
:root {
  --bg: #0a0a0a;
  --fg: #ffffff;
  --accent: #e11d2c;
  /* … */
}
```

Change the accent color there and it propagates everywhere.

## Netlify Forms

The booking form (`src/components/BookingForm.astro`) uses [Netlify Forms](https://docs.netlify.com/forms/setup/). It's set up with:

- `data-netlify="true"` — Netlify detects it at build time from the static HTML
- `data-netlify-honeypot="bot-field"` — a hidden field to trap spam bots
- `action="/thanks"` — successful submissions redirect to `/thanks`
- `name="booking"` — submissions appear under this form name in the Netlify dashboard

After the first successful deploy, go to Netlify → your site → **Forms** to enable email notifications to `bookings@officialfjr.com`.

## Deployment — Netlify

Config lives in [`netlify.toml`](./netlify.toml): build command, publish directory, pinned Node version, security + cache headers.

1. Netlify dashboard → **Add new site** → **Import an existing project** → GitHub → `Ayrthon/officialfjr`.
2. Netlify reads `netlify.toml` — no manual settings needed.
3. Every push to `main` triggers a redeploy.

Update the `site` field in `astro.config.mjs` to the real production URL when the domain is picked.

## Project structure

```
mcfjr-site/
├── public/
│   ├── favicon.svg
│   └── robots.txt
├── src/
│   ├── components/
│   │   ├── About.astro
│   │   ├── BookingForm.astro
│   │   ├── Experience.astro
│   │   ├── Footer.astro
│   │   ├── Gallery.astro
│   │   ├── Genres.astro
│   │   ├── Header.astro
│   │   ├── Hero.astro
│   │   ├── Icon.astro
│   │   ├── Placeholder.astro
│   │   ├── Presskit.astro
│   │   ├── Testimonials.astro
│   │   ├── TrustedBy.astro
│   │   └── Videos.astro
│   ├── layouts/
│   │   └── Layout.astro
│   ├── pages/
│   │   ├── index.astro
│   │   └── thanks.astro
│   └── styles/
│       └── global.css
├── astro.config.mjs
├── netlify.toml
├── package.json
└── tsconfig.json
```
