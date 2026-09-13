# gofrs community site

A minimalistic, fully static landing page about [the Gofrs](https://github.com/gofrs) — the community-formed group that maintains Go packages including [`gofrs/uuid`](https://github.com/gofrs/uuid) and [`gofrs/flock`](https://github.com/gofrs/flock). Served at **https://gof.rs**.

> **This is an unofficial community site.** It is not affiliated with, endorsed by, or maintained by the Gofrs organization. See [ATTRIBUTION.md](ATTRIBUTION.md).

## What's here

Everything served to visitors lives under `public/`; that directory is what gets uploaded.

| File | Purpose |
| --- | --- |
| `public/index.html` | The landing page — hero, library cards, about, get-involved, attribution footer |
| `public/404.html` | Custom not-found page (served via `not_found_handling`) |
| `public/_headers` | Security headers and cache policy, including a CSP |
| `public/favicon.svg` | Site icon (original mark, not derived from the Gofrs logo) |
| `public/robots.txt`, `public/sitemap.xml` | Basic crawler hints |
| `wrangler.jsonc` | Cloudflare Worker config — worker name and assets directory |
| `.github/workflows/deploy.yml` | Deploys `public/` on every push to `main` |
| `LICENSE` | MIT, covering the site code only |
| `ATTRIBUTION.md` | Full third-party attribution and licensing notes |

There is no build step, no `node_modules`, and no local copies of fonts or CSS. Tailwind CSS and the two fonts load from CDNs at runtime, as requested.

### Local preview

```bash
python3 -m http.server 8080 --directory public
# then open http://localhost:8080
```

Note that `_headers` is a Cloudflare feature and has no effect under a plain local server. To preview with the real asset routing, including `_headers` and the 404 page, use `npx wrangler@4 dev` instead.

## On the gof.rs address

`gof.rs` was previously the Gofrs organization's own address. The [`gofrs/gof.rs`](https://github.com/gofrs/gof.rs) repository still has GitHub Pages enabled, lists `https://gof.rs` as its homepage, and carries a `CNAME` file containing `gof.rs` on its `master` branch, but it was last pushed in August 2018 and that site is obsolete. The registration lapsed and the domain is now held by me.

## Data freshness

Version numbers and star counts in the library cards are baked into the HTML (values as of 12 September 2026) and then refreshed client-side from the public GitHub API on page load. If that request fails — rate limit, blocked, or JavaScript disabled — the baked-in values remain visible, so the page never shows a blank or broken figure.
