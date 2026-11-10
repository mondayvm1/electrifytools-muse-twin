# Electrify Tools — Muse Twin

Public collaboration repo for turning the Muse mockup into an editable, testable website without changing the existing Electrify Tools production repo.

## Design reference

- Muse mockup: https://muse.ai/s/electrify-tools-website-mockup-xak6mxdgycxc9xm/IHdmRwlNil3TBVRX1_wUbsqIuea7WNFYIOBcOGUbouI
- Reference hero: “The Hero Dial.”

This repo starts from the existing Electrify Tools application stack so collaborators have a working storefront, checkout architecture, tests, and local development setup. The Muse visual treatment still needs to be ported here and verified at desktop and phone widths.

The original production repository is separate and must not be overwritten or force-pushed from this project.

Marketing + storefront site for the Electrify Dial 2.0 (Tesla CAN-bus diagnostics).

Stack: TanStack Start (React 19, Vite, Tailwind 4), Stripe Checkout, deployed on Vercel.

## Local

```sh
npx -y bun@1.3.5 install
cp .env.example .env.local   # add your Stripe secret key
npx -y bun@1.3.5 run dev
```

## Payments

- Products and prices live in `src/config/products.ts` — the server reads prices from there, never from the browser.
- `POST /api/checkout` creates a Stripe Checkout Session (shipping address + phone collected, promo codes allowed).
- `/order/success` confirms the order after Stripe redirects back.
- Orders, receipts and refunds are handled in the Stripe dashboard.

Env vars: `STRIPE_SECRET_KEY` (required), `PUBLIC_ORIGIN` (optional; the site's public URL when it sits behind a proxy).
