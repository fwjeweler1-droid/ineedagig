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
