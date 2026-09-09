# Gamepad Tester

A one-page browser tool that reads live controller input: every button with its analog
value, both sticks, both triggers, rumble motors, and a resting-drift measurement.
No build step, no dependencies, no data leaves the device.

```
index.html    the whole site (markup, styles, script)
og.png        1200x630 social share image
robots.txt    crawler rules + sitemap pointer
sitemap.xml   single URL
vercel.json   security and cache headers
```

## Deploy to Vercel

**Drag and drop** — go to vercel.com/new, drop this folder in, done.

**Git** — push the folder to a repo, import it on Vercel, leave the framework preset
as *Other*. No build command, no output directory.

**CLI**
```bash
npm i -g vercel
cd gamepad-tester
vercel --prod
```

## After deploying: change the domain

Five places hold the placeholder `https://gamepad-tester.vercel.app`. Find and replace
it with your real domain, or the canonical tag and share cards will point at the wrong
site.

- `index.html` — `<link rel="canonical">`, `og:url`, `og:image`, `twitter:image`, and the two `@id` fields in the JSON-LD
- `robots.txt` — the `Sitemap:` line
- `sitemap.xml` — the `<loc>` and `<lastmod>`

## What was done for SEO and performance

**Crawlability** — one `<h1>`, section headings in order, a canonical URL, `lang="en"`,
robots.txt and sitemap.xml, and no content hidden behind JavaScript. The preloader is a
visual overlay, not a render gate, so crawlers get the full document immediately.

**Structured data** — a `@graph` with a `WebApplication` entity and a `FAQPage` built
from the three explanation blocks near the bottom. Those answers are real text on the
page, which is what makes the FAQ markup eligible rather than spammy.

**Share cards** — Open Graph and Twitter tags with a real 1200x630 image and alt text.

**Speed** — one HTML file, one font request, zero JS libraries, an inline SVG favicon
(no extra round trip), and `font-display: swap`. Nothing is fetched at runtime. Expect
a very high Lighthouse performance score; the only network dependency is Google Fonts,
and you can self-host Archivo and IBM Plex Mono to remove even that.

**Accessibility** — visible focus rings, `aria-live` on the connection status, an
`aria-label` on the controller diagram, labelled form controls, `prefers-reduced-motion`
respected, and text contrast above 4.5:1 throughout.

## Browser support

Chrome, Edge, Opera and Firefox read the Gamepad API fully. Safari's support is partial
and rumble is unavailable there. Controllers stay invisible to every browser until they
send input — that is a privacy measure in the spec, not a bug, which is why the empty
state asks for a button press.

---

Melted Code
