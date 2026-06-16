# veilens.app

The public marketing site for [veilens](https://github.com/veilensapp/veilens) —
a private, on-device document vault built on the
[headgate](https://github.com/veilensapp/headgate) privacy harness. A
single-page landing built with [Astro](https://astro.build), deployed to
**Cloudflare Workers (Static Assets)** at [veilens.app](https://veilens.app).

veilens runs on top of the [millrace](https://millrace.app) local inference
engine; this is the sister site to [millrace.app](https://millrace.app) and shares
its visual style.

## Develop

```sh
npm install
npm run dev        # http://localhost:4321
```

## Build

```sh
npm run build      # static output → ./dist/
npm run preview    # serve the build locally
```

## Deploy (Cloudflare Workers — Static Assets)

The site is fully static and deploys as an **assets-only Worker** (no Worker
script). [`wrangler.toml`](./wrangler.toml) points `[assets].directory` at
`./dist`.

- **Git integration:** connect the Worker to this repo. On each push to `main`
  Cloudflare runs `npm run build` then `npx wrangler deploy`, which uploads
  `./dist`.
- **Manual:** `npm run build && npx wrangler deploy` (after `wrangler login`).

The custom domain `veilens.app` is attached under the Worker's **Domains &
Routes** tab.
