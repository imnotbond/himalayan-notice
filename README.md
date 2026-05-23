# Himalayan Notice — Advertorial (Men's Health angle)

News-style advertorial promoting Himalayan Iron Shilajit Gummies. Single-market US.

## Stack

- Static HTML + Tailwind CDN
- bb-tracker (PostHog 162012 + GTM + dataLayer + Meta CAPI + TikTok browser pixel)
- Meta Pixel — `3477159645768812` (Himalayan Iron dedicated, single-market US)
- TikTok Pixel — `D88K7TBC77U17CDP3710` (Himalayan Iron dedicated, browser + server CAPI)

## CTA destination

Single `data-bb-cta` (line 840) → Shopify product page → Evoly GE → Himalayan Shilajit Gummies:
`https://evolymultivitaminesge.site/products/himalayan-shilajit-gummies`

bb-tracker forwards `attributes[fbc/fbp/fbclid/ttclid]` on the CTA href so Shopify writes them to `order.note_attributes`. The shopify-purchase webhook reads those back to populate Meta CAPI Purchase `user_data` (lift match quality).

## Deploy

- Vercel project: himalayan-notice
- GitHub: imnotbond/himalayan-notice
- Live: <https://himalayan-notice.vercel.app/>

## Tracking

- `page_id`: `himalayan-notice`
- `pageType`: `advertorial`
- `currency`: `USD`
- Registered in `bb-dashboard/lib/offers.ts` so the dashboard surfaces it
- PostHog project token: `phc_CGpemz5jFwEpAWNJeZNdo4UPBbivs2ZkJF3YTdJ8yPsJ` (project 162012)

## Server-side CAPI

- bb-tracker page_init → Meta `PageView` server-side via `bb-tracker-beta/api/capi/event` (dedupes with the browser fbq fired by bb-tracker.js using the same event_id)
- bb-tracker cta_clicked → Meta `InitiateCheckout` server-side (same event_id pattern)
- Shopify webhook `orders/create` on `0bmqqx-iv.myshopify.com` → `bb-tracker-beta/api/capi/shopify-purchase` → Meta CAPI Purchase with `event_id=fb_purchase_<orderId>` (dedupes with Custom Pixel checkout_completed)

## Inline `_fbc/_fbp` bridge

Inline script BEFORE `fbq init` sets `_fbc=fb.1.<ts>.<fbclid>` and seeds `_fbp` if absent. Survives adblock that blocks `connect.facebook.net`.

## Files

- `index.html` — the advertorial (single file, ~1600 lines, Tailwind CDN)
- `BOTTLES/` — product images
- `images/` — content images
- `trusted-by/` — media outlet logos
- `vercel.json` — `{cleanUrls: false, trailingSlash: false}`
