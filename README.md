# Himalayan Notice — Advertorial (Men's Health angle)

Clone of `healthdatacenter.site/himalayan-iron/` adapted as news-style advertorial.

## Stack
- Static HTML + Tailwind CDN
- bb-tracker (PostHog + GTM + dataLayer)
- Meta Pixel — country-aware: US (1708777253459299) / DE (2071044117089882)
- TikTok Pixel — D69I62BC77UA1UK9FD7G (account mvb meudon)

## CTA destination
Shopify cart permalink → Evoly GE → Himalayan Shilajit Gummies "Buy 1 Get 1":
`https://0bmqqx-iv.myshopify.com/cart/55535724789928:1?channel=buy_button`

## Deploy
- Vercel project: himalayan-notice
- GitHub: imnotbond/himalayan-notice
- Live: https://himalayan-notice.vercel.app/

## Tracking
- page_id: `himalayan-notice`
- pageType: `advertorial`
- Register in bb-dashboard/lib/offers.ts to surface in dashboard
