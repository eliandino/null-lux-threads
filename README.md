# NULL//LUX THREADS

A dark, neon T-shirt storefront built for GitHub Pages. The starter catalog has one **concept product** with AI imagery based on your surveillance-eye reference. The folder includes a front mockup, an editorial mockup, and a transparent artwork concept. The artwork is only 1027 × 1531 pixels; prepare and verify a full-resolution print file to the selected Printify template before selling. It has no live checkout until you add your own product links.

## Deploy on GitHub Pages

1. Create a GitHub repository and upload the **contents** of this folder to its root (including `index.html`, `studio.html`, `catalog.json`, `styles.css`, `app.js`, `studio.js`, and `assets/`).
2. In **Settings → Pages**, choose **Deploy from a branch**, your default branch, and **/(root)**. Save.
3. Open the Pages URL. Project repository paths work because all references are relative.

If you prefer Pages from `/docs`, put all site files into `/docs` together and choose `/docs` in Pages settings.

## Add and publish products

1. Open `studio.html` at your site URL. Add a name, price, comma separated tags, and one or more mockups. The **New item** and **Hero carousel** controls determine placement and badges. Hit **Save draft**. Counts update from the saved catalog when it is published.
2. The Studio stores drafts in *your current browser* with IndexedDB. This is a draft workspace, not a shared admin panel. Export `catalog.json` after editing, then replace the repository's `catalog.json` and commit. GitHub Pages will publish it.
3. Mockups uploaded in Studio are embedded as data URLs inside the exported JSON. Resize and compress images first (WebP recommended, roughly 1600 px maximum dimension). Keep the repository and JSON file reasonable in size. For larger catalogs, move images into `assets/` and use their relative paths in `catalog.json`.
4. The store reads `catalog.json` fresh on each visit. It counts published products for the header, derives each gallery counter from that product's `images`, and builds filters from tags. Search covers name, description, collection, and tags. Hidden items stay in the JSON but do not show in the store.
5. `purchaseUrl` must be an HTTPS address to an actual checkout/product page. Otherwise the product says **Coming soon**. Confirm fulfillment, pricing, and all consumer details before selling.

The publicly reachable Studio deliberately has **no publishing credentials**. Anyone can open it and make a draft in *their own browser*, but cannot change the live catalog without write access to your GitHub repo. Do not put secrets or Printify API tokens in any file deployed to GitHub Pages.

## Printify and future automation

Printify fulfillment is **not connected** in this starter. A Printify product ID can be stored now as a reference, and the purchase URL can point to a real hosted checkout after you configure one. Printify product creation and payment collection require separate integrations; a static Pages site cannot safely store your Printify token or act as a secure checkout.

The stable catalog contract and suggested bot pipeline live in [`docs/AUTOMATION.md`](docs/AUTOMATION.md). A future server-side job can accept approved mockups, sync products and prices, generate image paths and a validated `catalog.json`, then open a GitHub pull request. Deletions should be reviewed before publication.

## Files

- `catalog.json`: catalog and carousel settings; publish by committing this file.
- `assets/`: bundled concept shirt mockups and transparent artwork concept; replace or expand with your final approved artwork.
- `studio.html` / `studio.js`: local browser editor, import and export.
- `index.html` / `app.js` / `styles.css`: public storefront.

No build command or third-party runtime package is required. Fonts use Google Fonts with local fallbacks.

https://eliandino.github.io/null-lux-threads/
