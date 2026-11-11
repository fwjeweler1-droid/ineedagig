# Opportunities Beyond the Swamp — review and outreach procedure

**Status:** Reversible source proposal. This does not create a new account system, database, booking pipeline, or public listing submission form. No external opportunities are approved or published on the initial feed.

## Boundaries
- **IneedaGig.net** remains the canonical public booking hub.
- **Public venue bookings** remain connected to Connect's existing \`venue_booking_requests\` read path and owner-managed venue workflow.
- **Member gig requests** remain inside signed-in Connect; no public exposure of \`gig_requests\` or private communications.
- **Regional external opportunities** live on \`regional-opportunities.html\` and use a separately curated, static public \`regional-opportunities.json\` feed. They always link *out* to the original opportunity; IneedaGig does not apply for or book them.
- Never publish a lead merely because a scheduled search found it. A human owner must explicitly approve *each individual listing*. No unattended scraping, uploads, automatic social publishing, unsolicited invitations, or cross-origin account writes.

## Qualifying listings
Use a straight-line search radius of **500 miles from central Fort Wayne, Indiana**; record evidence for the radius check in a private review worksheet rather than publishing personal information. Prefer direct public organizer/venue/festival audition or talent-call listings.

A public entry requires:
1. A **direct HTTPS organizer/source URL** to the particular opportunity; verify the source is legitimate and still actionable.
2. Event/audition date or application deadline, a clear city/location, named organizer, and category.
3. A concise *original* factual summary, not copied commercial text, logos, or photographs.
4. Verification date, explicit expiration date, and indication of paid/unpaid/undisclosed compensation when supported.
5. An affirmative, dated **owner approval for this individual listing**, separate from an outreach approval.
6. Clear display as **external**, not an IneedaGig booking or Connect member gig request.

Newly verified leads should be proposed privately in the existing Intentional Noise Monday Brief. If no strong lead is found, do not manufacture a public listing.

## Publishing gate

Only an approved review becomes a new item inside \`regional-opportunities.json\`:

\`\`\`json
{
  "schema_version": 1,
  "updated_on": "2026-11-11",
  "opportunities": [
    {
      "id": "unique-nonpersonal-id",
      "title": "Specific audition or performer opportunity",
      "organizer": "Official organizer name",
      "location": "City, State",
      "category": "Audition",
      "source_url": "https://example.org/original-listing",
      "summary": "Original short verified factual summary.",
      "event_date": "2026-12-12",
      "application_deadline": "2026-12-01",
      "compensation": "Not disclosed",
      "verified_on": "2026-11-11",
      "expires_on": "2026-12-01",
      "approval_status": "approved",
      "approved_by_owner": true
    }
  ]
}
\`\`\`

The sample is **illustrative only**; none of its values is an actual lead. The live JSON deliberately begins with an empty array. Allowed categories are: \`Audition\`, \`Musicians wanted\`, \`Gig opportunity\`, \`Festival or showcase\`, and \`Collaboration\`. Either \`event_date\` or \`application_deadline\` is required; the other can be omitted. Both, if present, must be current/future. The browser shows only individual owner-approved items with valid HTTPS URLs and expiration dates that have not passed; listings verified more than 21 days ago also vanish until manually rechecked. These browser checks supplement—not replace—owner review and editorial control. The JSON file is **public**, so never put an email address, phone number, staff name, private note, credential, submission message or unapproved lead there.

Once an organizer creates its own Connect profile, refer the organizer to the existing venue booking flow; **do not silently convert an external lead into a venue-owned booking record**. Any venue-owned listing remains theirs to publish, modify, fill or expire.

## Invitation path — proposed, not sent

Use **only a contact channel explicitly advertised by the organizer for professional business, booking or relevant event inquiries**. A public performer-application-only address is *not* automatically consent to promotional outreach. Prefer an appropriate general venue/organizer business inquiry address or contact form, and obey posted outreach restrictions.

The Monday Brief can include a short **private** invitation candidate note: original source URL, organizer name, advertised suitable business contact channel (or "not suitable"), why outreach makes sense, and a *draft* for Charlie to review. Never paste the contact list into public site data. Do not build an automated marketing list. Do not contact anyone until Charlie explicitly approves the specific recipient and final message. Respect any opt-out; do not repeatedly follow up uninvited.

**Suggested individual invitation (edit before approval):**

> Subject: Your music opportunity on IneedaGig
>
> Hello,
>
> I noticed your public announcement seeking performers for [event or venue]. We're building IneedaGig, a free place where organizers and musicians can find one another. You're welcome to create a venue/organizer profile and post your own openings through Intentional Noise Connect.
>
> Take a look: https://ineedagig.net/ — profile signup: https://connect.intentionalnoise.info/auth.html?role=venue
>
> If this isn't relevant, no response is needed. We won't contact you further about it.
>
> Intentional Noise / IneedaGig

The message does not promise that messaging, payment collection, automatic posting, or end-to-end bookings are live. Use normal human review and applicable anti-spam requirements. Never imply the organizer has joined or endorsed us.

## Review and acceptance

Before merging to \`main\`, inspect the homepage navigation and regional directory in phone and desktop widths; verify the empty state; test the type and text filters, failure handling, malformed/unapproved/expired records, stale verification, HTTPS-only links, and no exposed private fields. Use test fixtures only on a nonpublic branch; do not publish fictitious opportunities. Check GitHub Pages deployment and live HTTPS after any authorized release. This change deliberately leaves all current Supabase tables, RLS, member auth, MFA, artwork, privacy rights, and synchronized project records untouched.


## Nationwide directory approval and daily refresh — superseding note (November 11, 2026)

Charlie explicitly approved publishing **all 47 organizer-source entries** returned in the nationwide November 11 research and maintaining them **every morning**. This authorization supersedes the earlier requirement for another individual approval for these exact 47 external source summaries. It does **not** authorize contacting organizations, applying for performances, posting to their accounts, or making bookings. Those remain separate permission gates.

The approved live candidate feed is \`regional-opportunities.json\` (schema version 2). It contains **16 festival/audition application routes** and **31 rolling venue-booking inquiry routes**. These are independent organizer submission channels, not booked gigs or promises of available dates. The page \`regional-opportunities.html\` displays them in **two separate tables**. All source links are HTTPS to the organizer's own site or designated application portal. Text is an original factual summary, not copied marketing content.

The directory is now nationwide; the separate Fort Wayne 500-mile discovery watch in the Monday Brief may continue to prioritize regional matches. Do not conflate it with the national directory's scope.

### Every-morning editorial update

The existing **Morning Start, 8:00 a.m. America/Indiana/Indianapolis** is the daily check, not a new paid subscription, daemon or independent account. Each run:

1. Read the current \`regional-opportunities.json\`, plus the prior update state; don't overwrite newer branch/source changes blindly.
2. Prioritize imminent deadlines, then check organizer sources for all existing records using official pages or designated application pages. Discover strong **new nationwide** sources via official search. A general artist inquiry is not an announced vacant date. Never invent event dates, pay, contact rights or fees.
3. For still-open verified records, update \`verified_on\` only when the page was actually checked. Update factual summary/deadline if the source changed. Remove or unpublish applications closed, withdrawn, expired, redirected to unrelated content, or without reliable direct source evidence; distinguish broken reachability from an organizer-confirmed closure. For transient errors, do not mark as permanently closed; stop showing stale data until reverified. Preserve stable record IDs.
4. Publish newly discovered **high-confidence public source listings** using the same two categories; the user's ongoing update instruction authorizes editorial directory entries after official verification. No venue-owned booking is created. Avoid duplicates and off-topic listings, and make only minimal-diff feed/site edits.
5. Validate 1) JSON schema and counts, 2) all unique HTTPS URLs, 3) source recency, 4) deadline/event expiry filtering, 5) zero public personal contact info, and 6) compatibility with the existing index page. Read back the current GitHub commit after any change, verify GitHub Pages workflow result where available, and report any failure honestly.
6. In the Morning Start response, give a **short status line** with added, changed, closed and remaining counts when a material difference occurred; don't clutter the release package with a full 47-item repeat. If no material change, one unobtrusive status line is enough. If web or GitHub write access is unavailable, list the precise unverified or pending changes without claiming an update.

The page's browser validation hides expired festival application deadlines and entries with source checks older than 45 days. Ongoing venue inquiries have no invented event date or expiry. If all entries are stale after repeated failed checks, display an empty state rather than misleading performers.

**Privacy/outreach:** The public JSON file stores no email addresses, phone numbers, private notes, applicant data or credentials. Never send invitations or contact venues automatically. Organizer invitations still require approval of each specific recipient/channel and final draft. Respect performer-application-only contact restrictions, opt-outs, and all posted submission rules. No changes to Connect auth/RLS, gig request tables, venue offers, FROG board, or owner-controlled artist showcase publications.
