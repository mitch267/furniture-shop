# Furniture Shop — Custom Store Manager v5

Configured for GitHub `mitch267/furniture-shop` and Cloudflare Worker `furniture-shop`.

## What changed
`/admin/` is now a custom shop-management dashboard instead of Decap's generic editor. It supports:
- visual product list with images
- add/edit/duplicate/delete products
- drag-and-drop product ordering
- drag-and-drop product image upload
- sale toggle and sale price
- stock and featured status
- dedicated Specials view
- store settings
- GitHub publishing, which triggers the connected Cloudflare deployment

## Repository layout
- `src/worker.js` — GitHub OAuth backend
- `public/` — storefront/static assets
- `public/admin/index.html` — custom store manager
- `public/data/products.json` — product/store database
- `wrangler.jsonc` — Cloudflare Worker config

## Cloudflare secrets
Keep these in Cloudflare Production Variables/Secrets:
- `GITHUB_CLIENT_ID`
- `GITHUB_CLIENT_SECRET` (Secret)
- `GITHUB_REPO_PRIVATE=false`

The GitHub OAuth app callback must be:
`https://furniture-shop.mmkoosaletse.workers.dev/api/callback`

## Deploy
Replace the repository contents with this package and commit to `main`. The connected Cloudflare build should run `npx wrangler deploy` automatically.


## v6 login fix
The custom admin OAuth login now registers its callback listener before opening GitHub, validates the callback origin, reports popup blocking/closure errors visibly, and uses a same-origin postMessage callback.
