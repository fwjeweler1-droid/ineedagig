# IneedaGig.net — booking-first network hub
**Current network checkpoint:** [IN-NET-2026-11-08-SYNC-01](https://github.com/fwjeweler1-droid/connect.intentionalnoise.info/blob/main/NETWORK_SYNC_CHECKPOINT_2026-11-08.md)  
**Machine-readable multi-repo marker:** [network-sync.json](network-sync.json)

**Four-site profiles:** Musicians and bands register once through Connect, receive private artist drafts, and opt in to public pages. The same approved artist record is displayed on .info, Connect, .band and IneedaGig via their published-profile routes. Venue booking and musician opportunities are advertised here; sensitive workflows remain in Connect.


**Status (checkpoint IN-NET-2026-11-08-SYNC-01):** Repository public; GitHub Pages deployment succeeded and custom-domain DNS check was reported successful. Live real-browser acceptance and booking/signup end-to-end tests are still PENDING. Older paragraphs below are historical design notes; this status supersedes their deployment assumptions.

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

A simple branded venue landing page can route to the **existing** Connect booking and musician search URLs. It should not write booking records itself. The domain has been connected for deployment; do not advertise production readiness until full live acceptance and safety checks are passed.

**Source of truth for live workflows:** `fwjeweler1-droid/connect.intentionalnoise.info` and its existing Supabase project. This README is a coordination note, not a replacement for project records or user approvals.


## Booking-first V1 implementation — November 8, 2026

**Built, source-verified; not yet deployed or live-browser accepted:**

- \`index.html\` is a mobile-responsive, booking-first website. The venue booking action goes to Connect's existing \`fill-my-stage.html\`; musician opportunities are listed from public, open, future \`venue_booking_requests\` through the existing Supabase Data API and its row-level security.
- The official approved Ineeda Gig image is referenced unchanged from the Connect asset URL (no crop, no modification, no re-upload).
- A publicly open booking can be selected to generate an individual public booking link and prefilled composer links for Facebook, X, Threads, and LinkedIn. The new site does **not** itself write to the booking database and does **not** send social posts to external platforms.
- The Connect booking page now prepares those same share links after **successful public booking publication**; it also provides a Social links control for existing open booking requests. Unique \`?booking=UUID\` public deep-links resolve and highlight an open booking. If a booking is filled, cancelled, hidden or expired, the public link does not surface a private record.
- The website retains \`noindex,nofollow\` pending launch approval. GitHub Pages deploy and domain DNS setup have been reported successful; live TLS/mobile/browser acceptance remains open.

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


## Canonical booking navigation — November 8, 2026

**IneedaGig.net is the single public entry point for booking discovery and booking requests.** Other Intentional Noise sites should link here rather than advertise independent public booking services.

- Venue booking opportunities: \`https://ineedagig.net/#opportunities\`
- Venue booking intake: \`https://ineedagig.net/#book\` (operational Connect form is used after the visitor chooses to post)
- Member auditions, band vacancies and music-work requests: \`https://ineedagig.net/#member-requests\` (existing signed-in Connect member board used to browse and post)
- Shareable public venue booking URL: \`https://ineedagig.net/?booking=<UUID>#opportunities\`; a live, open public record must be checked before showing the opportunity.

Existing secure implementation remains on Connect: \`venue_booking_requests\`, \`venue_booking_interests\`, \`venue_booking_thread_messages\`, and separate members-only \`gig_requests\`. **No member-only data is published anonymously.** No duplicate accounts, tables, submission services, or messages are created on IneedaGig.

The existing \`connect.intentionalnoise.info/fill-my-stage.html\` and \`/gig-requests.html\` stay functional as signed-in operational forms. This is currently **one visitor-facing public hub, not yet a single-domain end-to-end booking form**. Do not redirect or delete those operational pages until equivalent authenticated workflows have been tested on the canonical domain. \`.info\` navigation, \`.band\` links, Connect search, FROG call-to-actions, and newly generated share links now direct public discovery to IneedaGig.

The FROG promotional card board is distinct from dated booking requests; display it as music and gig promotions to prevent visitor confusion. Live browser acceptance and all cross-site links still require confirmation on desktop and mobile.

## Proposed: regional external opportunities (owner review required)

The source-only proposal adds [Opportunities Beyond the Swamp](regional-opportunities.html) and a separate [empty, owner-approved-only external listing feed](regional-opportunities.json), linked from the public booking home. See [listing and outreach gates](REGIONAL_OPPORTUNITIES_REVIEW.md). External organizer announcements link out to the source; they do not become Connect venue offers, member requests, artist pages, or bookings. The initial feed contains no public entries and no contact information. The existing Monday Brief can propose verified leads and suitable public business contact channels for **individual invitation review**; no contact or publication occurs automatically. Live deployment/browser tests remain pending until approved.
