# Champs Entertainment Website

Website for Champs Entertainment LLC, a Pittsburgh, PA DJ and event
entertainment business. Live at https://www.champsentertainment.com

## Tech stack

Plain HTML, CSS, and vanilla JS. No build step, no framework, no package
manager. Every page is a static `.html` file that can be opened or deployed
as-is. Hosted on GitHub Pages (see `CNAME`).

## Project structure

```
/
├── index.html              Homepage
├── about.html               
├── contact.html             Booking inquiry form
├── faq.html
├── weddings.html            Wedding packages & pricing
├── events.html              School dances, corporate, community/festival
│                              events (renamed from parties.html, Sept 2026)
├── recordings.html          Recording & livestreaming services
├── rentals.html             Equipment rental services
├── gallery.html             Event Highlights — wedding/corporate/community
│                              video (renamed from a club/rave-heavy "Video
│                              Sets" page, Sept 2026)
├── reviews.html
├── thankyou.html            Post-contact-form confirmation (noindex)
├── 404.html                 Custom error page (noindex)
├── media.html, services.html, parties.html, music.html, presskit.html
│                              Redirect stubs (see below) — kept for old
│                              inbound/bookmarked links, not real pages
├── css/
│   └── styles.css           Single site-wide stylesheet (see below)
├── blog/
│   ├── index.html            Blog landing page (post cards)
│   └── *.html                 Individual blog posts
├── Images/                   All site images (not tracked in some
│                              working copies — see note below)
├── videos/                    Hero background videos
├── files/                    Downloadable assets (e.g. press kit PDF)
├── robots.txt
├── sitemap.xml
└── CNAME                     GitHub Pages custom domain config
```

## How pages are built

There is no templating system. Every page is a full, self-contained HTML
file with its own `<head>` (meta tags, schema.org JSON-LD, title,
description) and repeats the same header/nav/footer markup. This means:

- **Adding or changing a nav link requires editing every page individually.**
  There are currently 18 HTML files with the site nav (11 core pages, `faq.html`
  and `404.html` as special cases with slightly different markup, plus the
  blog landing page and 5 posts). `music.html`, `presskit.html`, and
  `parties.html` are redirect stubs, not real pages, and don't carry nav.
- **Adding a new page** is easiest by copying an existing page closest in
  structure (e.g. copy `weddings.html` for a new service page, or an
  existing blog post for a new post) and editing the `<head>` tags, hero
  text, and body content.
- All shared visual styling lives in `css/styles.css`. Do not add
  page-specific `<style>` blocks in the `<head>`, that's the old pattern
  this site was cleaned up from (see "History" below).

## CSS architecture (`css/styles.css`)

One stylesheet, organized top to bottom as:

1. CSS variables (`:root`) — `--gold` (#C8A700) and `--bg`
2. Base/reset, typography (h1–h3, p, a)
3. Utility classes (`.text-gold`, `.text-muted`, `.mb-10`, etc.) — small,
   reusable one-off style helpers, used instead of inline `style=""`
   attributes
4. Layout (`.container`)
5. Hero/top nav (`.hero`, `.topbar`, `.navbar`, `.brand-logo`, etc.)
6. Content sections (`.alt-section` — the alternating-background content
   blocks used on every page, `.after-hero`)
7. Buttons (`.contact-btn`, `.review-btn`)
8. Contact form styles
9. Media embeds (YouTube/SoundCloud containers, used on gallery/music
   pages)
10. Press kit specific styles (carousel, tabs, booking buttons)
11. Footer
12. Blog landing page (`.blog-grid`, `.blog-card`)
13. Responsive breakpoints at the bottom: desktop (`min-width: 768px`),
    mobile (`max-width: 768px`), and a mid-range tablet breakpoint
    (`769px`–`1100px`) that collapses the nav into a hamburger earlier
    than a typical mobile breakpoint

The nav has a hamburger menu (`.menu-toggle`) toggled by
`toggleMenu()`/`toggleSubmenu()`, defined inline at the bottom of every
page's `<body>`.

## The blog

- `blog/index.html` is the landing page: a card grid pulling from
  `.blog-card` / `.blog-grid` styles in the main stylesheet. Each entire
  card is a click target (an `<a class="blog-card">` wrapping the date,
  title, and excerpt), with "Read More →" shown as a plain-text visual
  cue inside it rather than a separate link.
- Each post is a standalone HTML file in `blog/`, following the same
  header/nav/footer pattern as the rest of the site (with `../` relative
  paths since it's one directory deep), plus an `Article` schema.org
  block in addition to the site's `LocalBusiness` schema.
- **To publish a new post:** uncomment its card in `blog/index.html`
  (posts beyond the first are currently HTML-commented out pending
  rollout), set the real publish date in both the visible "Published"
  line and the `datePublished` field in the post's `Article` schema, and
  add its URL to `sitemap.xml`.
- Posts currently written but not yet live: `wedding-dj-vs-spotify-playlist.html`,
  `questions-to-ask-before-booking-a-dj.html`,
  `best-pittsburgh-wedding-venues.html`,
  `behind-the-scenes-heatsignal-furnace.html`.

## SEO conventions

- Every page has a unique `<title>` and meta description (no duplicates
  across pages).
- Every page has exactly one `<h1>` (the hero title) and uses `<h2>`/`<h3>`
  for section headings below it.
- Every real (indexable) page has a self-referencing `<link
  rel="canonical">`.
- `404.html` and `thankyou.html` carry `<meta name="robots"
  content="noindex">` (thank-you and error pages shouldn't be indexed).
- `sitemap.xml` should be kept in sync manually whenever a page is added,
  removed, or unpublished/republished (there's no automated generation).
- `robots.txt` allows all crawling and points to the sitemap.

## Image assets

Filenames are descriptive on purpose (e.g.
`wedding_reception_cocktail_hour.jpg`, `champs_basic_setup.jpg`) since
alt text and content were written to match. If you add new images, keep
that convention, it makes writing accurate alt text and future content
much easier.

## History

The site originally had CSS duplicated across a `<style>` block in every
individual HTML file (~700–900 lines each), which had drifted out of
sync between pages over time. It was consolidated into the single
`css/styles.css` file described above. The old `css/styles.css` file
(now gone) was an earlier, unrelated proof-of-concept and is not part of
this history.

## Website Redesign Project (planning as of September 2026)

### Why

The site originally had to serve two identities at once: Champs
Entertainment the bookable business, and Champs the DJ/producer. Now
that **champsdj.com** exists as its own site dedicated to the DJ/artist
side (mixes, releases, socials, live sets), champsentertainment.com no
longer needs to carry that weight. The two sites are being repositioned
as **sister sites** with a clean split:

- **champsentertainment.com** — the business. Weddings, corporate/community
  events, rentals, recordings. The goal on every page is "will this help
  someone decide to book."
- **champsdj.com** — the artist. Mixes, releases, live sets, socials,
  club/festival bookings. The goal is showcasing the music and the
  performer.

They should feel like two coordinated sibling brands, not two unrelated
projects. champsdj.com (built later) already has a stronger visual
system than champsentertainment.com currently does — real CSS custom
properties, a disciplined type pairing (Archivo Black / Oswald / Inter),
a consistent card-grid pattern, a scrolling ticker, animated EQ bars.
**The champsentertainment.com visual redesign should use champsdj.com as
a jumping-off point**: borrow the underlying bones (card system, type
discipline, real design tokens) while giving champsentertainment.com its
own more premium/elegant tone, distinct from champsdj.com's more
energetic, nightlife-coded feel.

### champsentertainment.com — content changes

- [x] **Cut the Music/Mixes page entirely.** Someone shopping for a
      wedding DJ is deciding on trust, not taste — they're not
      auditioning tracks the way a club booker would. Fold 1–2 short
      embedded clips directly into the Weddings/Events pages instead
      (as supporting proof, not a destination), and link out to
      champsdj.com for anyone who wants the full music/mix experience.
- [x] **Retool the video/gallery page → rename to "Event Highlights."**
      Populate with wedding/corporate footage only (first dances,
      reception floors, the VegFest gig) — cut club/rave clips
      entirely, that content lives on champsdj.com now. **Blocked on
      the actual set/highlight links/clips being provided to feature**
      — page structure can be built ahead of that, content slotted in
      once provided.
- [x] **Rename Parties → Events.** Broaden framing past "party" to
      include corporate and community work (coffee shop gigs, VegFest),
      not just nightlife-adjacent parties.
- [x] **Retool the About page copy** away from "cool gigs Champs has
      played" and toward "why book Champs Entertainment" — business-
      first framing, not DJ-persona framing. Add a line/section linking
      out to champsdj.com for anyone curious about the club sets and
      original music side (see cross-linking below).
- [x] **Press kit page (`presskit.html`): turn into a redirect, don't
      delete.** It's already indexed by Google. Point the redirect
      directly at the PDF (`files/Champs_PressKit2026.pdf`) rather than
      leaving a dead page. **Note for 2027:** when a new press kit PDF
      is generated, the redirect target (and the direct link from
      champsdj.com's Book section) both need updating to the new
      filename/URL.
- [x] **Reviews page rebuild.** Drop the old Google-auto-import +
      Peerspace/Instagram sections structure. Replace with 3 real,
      hand-picked reviews (sourced below), presented well rather than
      padded to look like more than it is.
- [x] **Cross-link to champsdj.com.** Currently one-directional
      (champsdj.com links to champsentertainment.com, nothing points
      back). Add a line in the About page: something like "Curious
      about Champs' club sets and original music? Visit champsdj.com."
- [ ] **Hero video swap (wedding footage instead of club footage) —
      SHELVED for now**, pending real photo/video being available from an
      actual wedding he's played. Decision made: keep current club
      footage as placeholder in the meantime rather than substitute
      generic stock wedding footage — recognizable stock footage risks
      undercutting the "this is a real professional" trust the rest of
      the site is building. A single strong real photo (not necessarily
      video) is an acceptable lower-effort placeholder once available.

### champsentertainment.com — visual redesign (once content changes above are done)

- [x] Stop center-aligning everything by default (called out
      specifically: the Weddings pricing section currently uses emoji
      as bullet markers, which don't align consistently across
      fonts/OS and reads amateurish).
- [x] **Weddings page: convert pricing from emoji-bulleted text into
      proper pricing panels/cards** — one card per tier (Party Starter /
      People's Choice / Total Package), each with name, price range, and
      a clean feature list. Easier to compare, easier to scan, looks
      intentional instead of accidental.
- [x] **FAQ page: convert from alternating black/gold sections into an
      accordion.** Short Q&A content in the current alternating-section
      layout produces a rapid zebra-stripe effect with nothing to anchor
      the eye. Collapsed-by-default accordion solves the striping and
      makes the page feel shorter/less overwhelming at a glance.
- [x] Pull visual/structural inspiration from champsdj.com's existing
      design system (see "Why" above) rather than starting from zero.

### champsdj.com — changes (lower priority; business site work comes first)

- [ ] **Replace the "Friends" section** (currently EDC Discord
      community content — off-brand once champsdj.com is purely the
      Champs artist brand) **with two new sections**:
  - "Recent Sets" recap feed — short recap items (photo + one line +
    video link) for notable past gigs. Can cross-link to
    champsentertainment.com blog posts that cover the same event (e.g.
    the heatsignal FURNACE recap).
  - "As Heard At" — a compact credibility strip of venues/events played.
- [ ] **Footer copy fix:** currently reads "Reviews, Bookings & Press."
      Once the press kit lives entirely on champsdj.com's own Book
      section (already does — it links to the PDF directly), the
      champsentertainment.com link no longer needs to imply it hosts
      "Press." New footer text: **"Reviews & Bookings."**

### Content already sourced

**Reviews for the rebuilt Reviews page** (real Google reviews for Champs
Entertainment LLC, collected September 2026):

1. **Samantha Kummer** — ★★★★★ — *"Matt set up at a community party
   hosted at a local climbing gym! He was easy to communicate with
   during the coordination of the event. His music selection was fun
   and kept the energy groovin'!"*
2. **Edie G** (Local Guide) — ★★★★★ — *"Champs put together the most
   incredible set for our cocktail hour and wedding reception AND was
   an amazing MC! Professional and easy to work with. The lighting
   really transformed our modestly decorated space and brought a lot of
   energy when we made the transition from Dinner Time to Dancing Time.
   We got a ton of compliments on the music selection throughout the
   event and Champs had me out on the dance floor most of the
   night!!"* — this is the wedding-specific review.
3. **Justice for Animals** — ★★★★★ — *"Matt was awesome! Professional
   and can read the room. We would love to have him back! Thank you
   Matt"* — nonprofit/organizational event.

### Suggested order of operations

1. Content decisions (this list) — **done**
2. champsentertainment.com content changes (cut Music page, retool
   Gallery → Event Highlights structure, rename Parties → Events,
   retool About copy, presskit.html → redirect, add cross-link to
   champsdj.com) — **done, September 2026**
3. Reviews page rebuild using the sourced reviews above — **done,
   September 2026**
4. champsentertainment.com visual redesign (pricing cards, FAQ
   accordion, general de-centering, drawing from champsdj.com's design
   system) — **done, September 2026**
5. Hero video/photo swap — whenever real wedding footage/photos are
   available
6. champsdj.com Friends section replacement + footer copy fix
      (lower priority, business site comes first)

### Notes from executing steps 2 & 3

- `events.html` is a new file (renamed from `parties.html`).
  `parties.html` now redirects to it, matching the existing
  `media.html`/`services.html` redirect-stub pattern, to preserve any
  existing links/SEO equity rather than leaving a dead page.
- `music.html` now redirects to `https://champsdj.com/#mixes` — the
  wedding-appropriate mix embed (SoundCloud playlist) that used to live
  there is now embedded directly in `weddings.html` instead, per the
  "fold 1-2 clips into the Weddings/Events pages" plan.
- `presskit.html` now redirects straight to the PDF, as planned.
- Gallery page ("Event Highlights") kept 5 of its original 11 video
  sections (Yinzers Fake Wedding, Venango Pride, Spigolo, the DJs
  Against Apartheid fundraiser, Colombino) and cut the 6 club/rave/
  DJ-persona ones. This wasn't actually blocked on new content the way
  originally expected — the existing gallery already had enough
  wedding/corporate/community-appropriate material to retool with
  immediately. More clips can still be added later.
- Found and removed a dead `fancybox` lightbox library (CSS + 2 script
  tags) on the old gallery page that was loading but never actually
  used anywhere in the markup.
- The About page rewrite kept the inclusivity statement and the
  wedding-availability messaging near-verbatim (genuinely good content,
  no reason to touch it), and kept the "MY EXPERIENCE" bullet list
  structure, just swapped out the EDC Discord Music Night LIVE / Ibiza
  Stardust Radio residency / Pittsburgh Open Decks bullets for
  business-relevant ones (wedding/event booking history, production
  capabilities).
- Reviews page now uses a real card grid (`.review-card` /
  `.review-grid` in `css/styles.css`) instead of the old plain-text
  layout with manual `</br>` line breaks.

### Notes from executing step 4 (visual redesign)

**The scroll color-flash is completely gone.** `.alt-section` and
`.alt-dark` are still used as class names in the markup (to avoid
touching every page's HTML), but their CSS meaning changed entirely:
sections are now static, with a subtle `var(--line)` top border for
rhythm instead of flashing gold on scroll. This one CSS change fixed
the "black and yellow striping" complaint sitewide, including on
`about.html` and every blog post, without editing those files
individually.

**New design tokens, borrowed from champsdj.com.** `css/styles.css`'s
`:root` now uses the same token *names* as champsdj.com
(`--bg`, `--bg-raised`, `--ink`, `--ink-dim`, `--line`), and the same
*values* for all of them except `--gold`, which stays this site's own
`#C8A700` to match the existing logo image assets rather than
champsdj.com's slightly different gold. This is the actual mechanism
behind "use champsdj.com as a jumping-off point for the redesign" —
shared bones, distinct brand color.

**A real bug this caused, found and fixed:** `.text-dark` (used for a
few bullet-point icons on `about.html` and `rentals.html`) was
originally black-on-black-by-default, meant to only become visible
once the old gold flash triggered. Removing the flash would have made
those icons permanently invisible. Fixed by switching them to
`.text-gold`, matching the identical icon pattern already used
correctly elsewhere (weddings.html, events.html).

**New reusable components added to `css/styles.css`:**
- `.pricing-card` / `.pricing-grid` (with a `.featured` badge variant
  and a `.pricing-grid-2` variant for 2-item layouts) — used on
  weddings, events, recordings, and rentals
- `.check-list` — a plain CSS checkmark list, replacing emoji ✅
  bullets sitewide
- `.faq-item` / `.faq-question` / `.faq-answer` — the FAQ accordion
- `.quote-callout` — the DJ-quote "section divider" treatment on
  index.html
- `.highlight-card` — wraps each entry on the Event Highlights page
- `.contact-card` — wraps the contact form

**Pricing pages (weddings/events/recordings/rentals):** all four
converted from emoji-bulleted text dumps into pricing cards, per your
"these four were basically copy-pasted from weddings.html so keep
that shared vibe" note. Weddings' "People's Choice" tier got the
`.featured` badge since Champs' own copy already calls it the
middle-and-most-popular option. Rentals got the specific
Audio/Speakers, Lighting, and "DJ Gear & Mixers" categories you asked
for (Pioneer DJ controllers landed in the last one since they're DJ
gear, not literally mixers). Also fixed while proofreading: "Audio
Records" → "Audio Recorder" (Zoom H1), a dropped word in rentals.html
("accommodate your any reasonable" → "accommodate any reasonable"),
and two other small grammar fixes on recordings.html.

**Reviews page:** stars went from 15px to 28px with letter-spacing so
they actually read as a rating at a glance, reviewer names went from
plain bold text to 22px/800-weight, and the "Wedding / Community Event
/ Nonprofit Event" category labels are gone entirely — just name, then
location on the line below, as asked. Also added a subtle gold
left-border on the quote text itself for a touch of editorial polish.

**FAQ accordion:** built exactly as described — collapsed by default,
gold border around each item, question background flips to solid gold
with black text when expanded, the answer stays in the collapsed
question's normal dark coloring, and the chevron icon rotates 180° on
open/close. All 11 existing questions carried over with their original
answers untouched.

**About page:** reordered per your note — welcome line, photo, "My
name is Matthew Burns..."/thank-you, *then* the inclusivity and
wedding-availability paragraphs. Content itself wasn't touched, only
the order. Didn't do a full structural rebuild into the literal blog
template (dateline, hero-subtitle tagline, etc.) since the section
color-flash removal already gets most of the way to "reads like a
blog post" on its own — flagging this as an easy follow-up if you want
it to go further once you've seen the current version live.

**Index page quotes:** the four DJ quotes (Carl Cox, Steve Aoki,
Fatboy Slim, Mix Master Mike) were previously marked up as `<h2>`
tags, which is why they looked identical to actual section headings
instead of standing out as dividers. Converted to a proper
`.quote-callout` component: bordered top/bottom, larger italic gold
text, attribution on its own line.

**Event Highlights (gallery.html):** the 5 remaining entries (after
the club/rave cut in step 2) each now sit in their own bordered card
instead of plain stacked text with a jarring alt-section wrapper
around some of them. The old `.alt-section.alt-dark` wrappers on 3 of
the 5 entries were removed entirely in favor of the card treatment,
since a card and a full-bleed section flash don't layer well visually.

**Contact page:** the form now sits inside a `.contact-card` (dark
raised background, bordered, capped width) instead of floating
directly on the page background, consistent with every other card on
the site now.

**404 page:** rewritten with a wedding pun theme per your request —
"LEFT AT THE ALTAR" as the headline, "This page never made it down the
aisle," cold-feet/open-bar jokes, and a "Take Me Back to the Dance
Floor" button home. Title/OG/Twitter meta tags updated to match; the
page is still `noindex` as before.

**thankyou.html:** no changes needed — it never used the alt-section
pattern, so it was already visually consistent with the rest of the
redesign once the CSS foundation changed.

**Blog posts:** no changes needed either. They already used the card
system on the landing page and the same `.alt-section` markup as every
other page in their body content, so the CSS fix alone cleaned them up
completely — verified this directly (grepped all 5 posts + the landing
page for leftover `bottom-cta`/`in-view`/`text-dark` references: zero
found).

**What's still open from the original ask:** the hero video swap
(shelved, waiting on real wedding footage — unrelated to this pass)
and everything on the champsdj.com side (Friends section replacement,
footer copy fix) — both lower priority per your own ordering, and
untouched this session.

### Branding kit

The site now has a real Design System artifact documenting colors,
type, spacing, radius, and every component pattern in production,
built directly from `css/styles.css`. It lives at:

**https://claude.ai/artifact/XCZ6qkvqCjrzPdMpKYMP4e**

This is a live claude.ai artifact, not a file in this repo — open the
link to read it. It's the reference to point at for future design
decisions rather than re-deriving them from scratch each time.

### Notes from executing the typography & alignment follow-up (September 2026)

Before this pass, every page loaded Nunito for both headings and body
text, and paragraphs were force-centered by two separate `@media`
rules in `css/styles.css` (one for desktop, one for mobile) — that
turned out to be the actual mechanism behind the "everything feels
centered" complaint, not something scattered page-by-page.

**Typography, Option C from a 4-way comparison the site owner
reviewed:**
- Headings (`h1`/`h2`/`h3`) → **Bricolage Grotesque** (weights
  600–800)
- Body text → **Public Sans** (weights 400–600)
- Both loaded via a single Google Fonts `<link>`, swapped in across
  all 18 pages
- Chosen over Nunito specifically because Nunito reads bubbly/
  Comic-Sans-adjacent at large bold sizes — the opposite of the
  "premium wedding business" positioning. Chosen over pairings closer
  to champsdj.com's exact Archivo Black/Oswald because the goal was
  shared *design DNA* between the sister sites, not a copy — Bricolage
  Grotesque is a different display face with a similarly confident,
  modern register.

**Alignment:** the rule that's now documented in the Design System —
content-heavy text (paragraphs, FAQ answers, review quotes, list
items) is left-aligned; short copy (hero taglines, the homepage DJ
quote-callouts, CTAs) stays centered. Implemented by changing the base
`p` rule in both media queries from `text-align: center` to
`text-align: left`, then adding explicit `text-align: center` back
onto the specific short elements (`.hero-subtitle`, `.after-hero p`)
that needed to stay centered despite the new default.

**A bug introduced and caught in the same pass:** the font `<link>`
swap was first written with a shell-escaping mistake that put literal
backslashes into the URL (`wght@600;700;800\&family=...` instead of
`\&` → `&`), which would have silently broken font loading on every
page. Caught by grepping the actual file output rather than trusting
the script that wrote it, fixed, and re-verified clean across all 18
files.

**Still outstanding:** the ALL-CAPS heading text itself (e.g. "WEDDING
PACKAGES") is hardcoded directly in each page's HTML, not applied via
CSS `text-transform` — confirmed by checking for `text-transform` in
`css/styles.css` and finding only one unrelated rule (the pricing
card's "MOST POPULAR" badge). Converting to sentence case therefore
means rewriting roughly 80–100 individual heading strings by hand
across all 18 pages, not a CSS-only change. **This includes the FAQ
question text specifically** — currently all-caps inside each
`.faq-question` button, confirmed as in-scope for the same pass rather
than an exception. Deliberately not started in the same session as
the font/alignment work to avoid a half-done conversion if the session
ran out mid-pass — picking this up fresh is the plan.
