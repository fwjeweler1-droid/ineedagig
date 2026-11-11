# Nationwide external artist booking-source directory (November 11, 2026)

Status: owner-authorized public-source directory, separate from Connect member-owned artist pages. This is not a member import, not a booking transaction, not a consent to marketing, and not a claim that an external artist endorses IneedaGig.

## Sources and architecture
- \`external-performers.json\` is a manually curated, minimal factual catalog of 49 public performer-booking URLs found in a nationwide search. Mostly direct individual GigSalad and The Bash performer profiles, plus a few official artist booking sites.
- \`external-performers.html\` displays two grouped, green-and-gold searchable public tables: bands/ensembles versus soloists, duos and flexible lineups.
- The homepage and owner-approved Connect artist directory link to the separate external directory. **Do not merge** this catalog with the authenticated Connect \`musician_profiles\` or owner-approved \`artist_pages\`, and never create a Connect account or artist page for someone else.
- An external listing is a **public lead pointing to an existing professional booking page**. It is not an open date, payment quote, endorsement or affiliation. The original platform or artist handles inquiries and may charge fees; do not copy reviews, photos, profiles, contact details or commercial text.
- The public feed contains stage/act names, advertised location/genre, concise independently written descriptions, professional public source URL and date of source review. **No personal contact details or follower/engagement data.** Public artist names are not user account information.
- Keep \`artists.html\` strictly limited to Connect members who explicitly published their profiles. If an externally listed artist later joins Connect, never silently merge their account with an external listing: ask for ownership proof and publication consent first. Honor a verified owner's request to correct or remove a directory source entry.

## Morning update checks — part of existing Morning Start
The existing daily 8:00 AM (America/Indiana/Indianapolis) **Morning Start** workflow checks the venue and external performer directories together, after priority music-release tasks:
1. Read current GitHub main \`external-performers.json\` and record version before editing. Protect other people's changes and stable IDs.
2. Check performers' official or professional public booking pages for continued availability of the **booking-inquiry route** and accuracy of stage name, location, act type and genres. Verify actual source rather than blindly advancing \`reviewed_on\`.
3. Independently discover quality nationwide performers who publicly offer booking inquiries, prioritizing musicians not already represented. Choose a useful range of geographies and music styles. Reject vague, expired, unauthorized, adult-only or broken links, and deduplicate by source URL and artist name.
4. Remove/disable listings whose owner requests removal, whose page clearly has closed, which redirect to unrelated services or cannot be verified before the 45-day stale-source limit. A transient access error alone is not proof the artist retired; mark as unverified, then revisit. The browser automatically hides listings last actually reviewed more than 45 days ago.
5. Publish minimal changes to GitHub source only when justified, read back file and commit, verify URL uniqueness, JSON shape, safe HTTPS links, zero contact data and the separate private/public member boundary. Check GitHub Pages build and HTTPS where available. If no data has actually been rechecked, do not claim it was.
6. Report only material added/removed/updated counts, with concise source-verified examples, in the Morning Start after release obligations. Do not let site search displace music promotion, and never promise a background website updater independent of this schedule.

## Outreach gate
The user previously approved **considering personalized invitations** using public business booking/general inquiry contact channels where appropriate; this does not authorize outreach to each new artist automatically. Any invitation to join Connect must be reviewed by Charlie for the exact recipient, final message and channel. No bulk scraping, mass marketing, auto-DMs, emails, booking requests, applications or account creation. Never use a performance-booking or quote-only form to send promotional pitches when restricted.

## Test acceptance
- 49 unique HTTPS individual public booking URLs at initial publication.
- Table-group counts equal total, and filter/category changes do not mix member-owned data.
- XSS-safe text using DOM \`textContent\`, HTTPS-only links, \`noopener noreferrer\` for new windows.
- Stale/invalid data is not shown; malformed JSON failure is honest.
- Phone and desktop mobile scroll/table navigation, text contrast, and keyboard access; public GitHub Pages deploy and HTTPS must be checked independently.
- If a verified original source requires sign-in or quotes, say so; do not claim external platform bookings are free or executed inside IneedaGig.


## Canada expansion checkpoint — November 11, 2026

The public external performer search now covers **United States and Canada**. Eighteen original Canadian artist booking-source entries were added from official public booking pages, spanning Ontario, Québec, British Columbia, Manitoba and Nova Scotia. The feed now contains **67 entries (49 prior U.S. + 18 Canada)**. One pre-existing U.S. entry marked `review_required` remains excluded by the browser, so the current visible directory contains **66** source links. This is a deliberate review gate, not missing data. The newly added Canadian entries are visible by searching `Canada`.

Continue the existing Morning Start checking and discovery in **both countries**, preserving original URLs, no duplicate artist identities, no presumed availability, no invitations without explicit review, and no changes to Connect members' private profiles. If an artist requests correction/removal, honor the verified ownership request. Canadian provincial and cross-border booking conditions must not be presented as verified by this catalog.
