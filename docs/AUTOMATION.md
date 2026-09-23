# Automation contract — version 1

The public store loads `catalog.json`. It has no privileged API endpoints. Keep this file as the handoff contract for a future trusted worker or bot.

## Product shape

```json
{
  "id": "immutable-slug-or-printify-id",
  "name": "GHOST SIGNAL",
  "collection": "SYSTEM / 01",
  "description": "Product description",
  "price": 38,
  "currency": "USD",
  "tags": ["Cyber", "AI"],
  "isNew": true,
  "featured": true,
  "published": true,
  "createdAt": "2026-09-23T00:00:00.000Z",
  "images": ["assets/ghost-signal.png"],
  "printifyProductId": "",
  "purchaseUrl": ""
}
```

Top level: `schemaVersion: 1`, `settings: { carouselStyle: "slide" | "fade", carouselSeconds: 2..20 }`, `products: []`. Keep IDs stable during updates. Product count includes published entries; mockup counts equal each product's image count. The hero rotates through the images of published products marked `featured`.

## Proposed trusted integration

1. Receive a new design and its mockups in private storage. Keep original files and a human review state.
2. Use a server-side Printify token in a secret store to create or update the Printify product. Capture its product ID, variants, shipping information, and finalized retail price. Never expose the token in this repository or browser code.
3. Publish mockups under versioned `assets/` paths or a trusted image host; validate supported formats, sizes, ownership, and HTTPS origins.
4. Upsert by stable `id` or `printifyProductId`; validate names, nonnegative price, tags, image count, and purchase URL. Set `isNew` deliberately and retire old badges as part of the drop cadence.
5. Open a pull request changing `catalog.json` and assets, with a diff of additions, price changes, and removals. Review and merge to publish on GitHub Pages. For deletions, prefer `published: false` first to preserve history.
6. Reconcile Printify order/stock status in the **checkout integration**. A GitHub Pages catalog by itself cannot reserve inventory, collect payment, or receive secure webhooks.

For high-volume catalogs, migrate the source of truth to a database and serve images from object storage; keep a versioned public JSON export or adapt `app.js` to call your own read-only catalog endpoint. Add authentication and authorization to any future admin API before exposing write operations.
