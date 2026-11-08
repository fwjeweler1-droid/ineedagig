# IneedaGig.net — project foundation

**Status (2026-11-08):** New private repository. Domain recently purchased; DNS/hosting not yet verified. No public launch or functional end-to-end acceptance is claimed.

## Role and navigation

IneedaGig.net is the **venue-facing entry point** for bars, clubs, festivals, and other organizers seeking independent musicians and bands. **Ineeda Gig** is the approved venue-booking mascot (FROG's girlfriend).

Use existing Intentional Noise resources rather than duplicating their systems:

- **Booking workflow:** https://connect.intentionalnoise.info/fill-my-stage.html
- **Musician availability search:** https://connect.intentionalnoise.info/search.html?category=available_for_gigs&distance=any
- **Gig opportunities:** https://connect.intentionalnoise.info/gig-requests.html
- **FROG hub:** https://connect.intentionalnoise.info/releases-and-gigs.html
- **Connect accounts and profiles:** https://connect.intentionalnoise.info/
- **Public artist showcases:** https://intentionalnoise.band/
- **Organization information:** https://intentionalnoise.info/
- **Intentional Noise music:** https://intentionalnoise.com/

## Architecture constraints

1. **Reuse Connect authentication, profiles, and venue-booking tables.** No separate account system, new database, or mirrored member records by default.
2. Avoid duplicating booking submission logic. Link to the current Connect workflow until a secure cross-origin integration is designed, tested, and expressly approved.
3. Maintain existing row-level security and privacy boundaries. Do not put private records, tokens, or credentials in client code or public repository files.
4. The approved Ineeda Gig mascot must not be cropped, zoomed, modified, or regenerated without approval. Authoritative asset is documented in Connect's `INEEDA_GIG_MASCOT_APPROVED_2026-11-08.md`.
5. Preserve **MFA disabled** as explicitly directed; do not change authentication settings as part of this project's initial setup.
6. No payments, subscription tiers, direct booking guarantees, automated matching, or new commission structure without authorization.
7. Keep visitor-facing experience visually continuous with .info / Connect / .band. Prioritize one reversible change at a time.

## Existing evidence and remaining acceptance gates

Connect reports a connected booking workflow and passing privacy/RLS tests, with no leftover test bookings. Those checks do **not** establish a production-ready public launch. The original remaining gates include:

- Verify live deployed browser navigation on desktop and mobile.
- Run a real venue + musician end-to-end test: sign-in, draft, publication, musician response, private conversation, shortlist, filled/closed, sign-out.
- Review reporting, moderation, rate limits, and abuse controls before broad release.
- Verify the new domain's DNS, TLS certificate, and hosting after domain configuration completes.

## Smallest reversible first implementation

A simple branded venue landing page can route to the **existing** Connect booking and musician search URLs. It should not write booking records itself. Do not connect the purchased domain or activate a public launch until its deployment is checked and approved.

**Source of truth for live workflows:** `fwjeweler1-droid/connect.intentionalnoise.info` and its existing Supabase project. This README is a coordination note, not a replacement for project records or user approvals.


## Booking-first V1 implementation — November 8, 2026

**Built, source-verified; not yet deployed or live-browser accepted:**

- \`index.html\` is a mobile-responsive, booking-first website. The venue booking action goes to Connect's existing \`fill-my-stage.html\`; musician opportunities are listed from public, open, future \`venue_booking_requests\` through the existing Supabase Data API and its row-level security.
- The official approved Ineeda Gig image is referenced unchanged from the Connect asset URL (no crop, no modification, no re-upload).
- A publicly open booking can be selected to generate an individual public booking link and prefilled composer links for Facebook, X, Threads, and LinkedIn. The new site does **not** itself write to the booking database and does **not** send social posts to external platforms.
- The Connect booking page now prepares those same share links after **successful public booking publication**; it also provides a Social links control for existing open booking requests. Unique \`?booking=UUID\` public deep-links resolve and highlight an open booking. If a booking is filled, cancelled, hidden or expired, the public link does not surface a private record.
- The website retains \`noindex,nofollow\` until deployment and launch readiness are approved. Domain DNS, TLS and hosting remain pending independent verification.

**Source commits:**
- IneedaGig booking-first page: \`ff51162e409f4d2a49159391d0100f5b9087984f\`.
- Connect sharing module: \`751fbfa49e5aa6aa2e7bb08a50227236a795de4c\`.
- Connect sharing UI: \`a17cffcd944cfdd79a379e269de0ae3a83323947\`.
- Connect save-completion integration and public deep-links: \`cd393f54296b44fbdccb481fbb96085bf2fab73f\`.

### Social publishing distinction

*Automatically generating links* after the booking is posted is implemented. **Unattended posting into an artist's or venue's Facebook/Instagram/Threads/X/etc. account is not implemented.** Platform composer buttons still require the account owner to review and submit the post.

A future opt-in auto-publishing service requires user-authorized account connections with approved platform scopes, server-side secure token storage, per-account consent, explicit publishing controls, platform policy review, idempotency and retries, rate limiting, abuse moderation, revoke/disconnect, success/failure receipts, and reconciliation. Do not add this to anonymous frontend scripts or assert that third-party account authorization has occurred.

### Live acceptance still pending

Test public feed, mobile layout, sign-in roundtrip, one real venue post, one musician response, copy/share links, non-public draft protection, filled/closed link handling, and the exact domain deployment. No automated external posting or real booking was performed as part of this source update. Leave MFA unchanged (disabled).
