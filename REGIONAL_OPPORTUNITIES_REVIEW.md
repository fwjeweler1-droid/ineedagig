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
