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
├── parties.html             Parties & events (clubs, corporate, etc.)
├── recordings.html          Recording & livestreaming services
├── rentals.html             Equipment rental services
├── gallery.html             Video sets
├── music.html                Music & mixes
├── reviews.html
├── presskit.html            Interactive press kit
├── thankyou.html            Post-contact-form confirmation (noindex)
├── 404.html                 Custom error page (noindex)
├── media.html, services.html  Legacy redirect stubs (redirect to
│                              gallery.html / weddings.html — kept for old
│                              inbound/bookmarked links)
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
  There are currently 20 HTML files with the site nav (12 core pages, `faq.html`
  and `404.html` as special cases with slightly different markup, plus the
  blog landing page and 5 posts).
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

- [ ] **Cut the Music/Mixes page entirely.** Someone shopping for a
      wedding DJ is deciding on trust, not taste — they're not
      auditioning tracks the way a club booker would. Fold 1–2 short
      embedded clips directly into the Weddings/Events pages instead
      (as supporting proof, not a destination), and link out to
      champsdj.com for anyone who wants the full music/mix experience.
- [ ] **Retool the video/gallery page → rename to "Event Highlights."**
      Populate with wedding/corporate footage only (first dances,
      reception floors, the VegFest gig) — cut club/rave clips
      entirely, that content lives on champsdj.com now. **Blocked on
      the actual set/highlight links/clips being provided to feature**
      — page structure can be built ahead of that, content slotted in
      once provided.
- [ ] **Rename Parties → Events.** Broaden framing past "party" to
      include corporate and community work (coffee shop gigs, VegFest),
      not just nightlife-adjacent parties.
- [ ] **Retool the About page copy** away from "cool gigs Champs has
      played" and toward "why book Champs Entertainment" — business-
      first framing, not DJ-persona framing. Add a line/section linking
      out to champsdj.com for anyone curious about the club sets and
      original music side (see cross-linking below).
- [ ] **Press kit page (`presskit.html`): turn into a redirect, don't
      delete.** It's already indexed by Google. Point the redirect
      directly at the PDF (`files/Champs_PressKit2026.pdf`) rather than
      leaving a dead page. **Note for 2027:** when a new press kit PDF
      is generated, the redirect target (and the direct link from
      champsdj.com's Book section) both need updating to the new
      filename/URL.
- [ ] **Reviews page rebuild.** Drop the old Google-auto-import +
      Peerspace/Instagram sections structure. Replace with 3 real,
      hand-picked reviews (sourced below), presented well rather than
      padded to look like more than it is.
- [ ] **Cross-link to champsdj.com.** Currently one-directional
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

- [ ] Stop center-aligning everything by default (called out
      specifically: the Weddings pricing section currently uses emoji
      as bullet markers, which don't align consistently across
      fonts/OS and reads amateurish).
- [ ] **Weddings page: convert pricing from emoji-bulleted text into
      proper pricing panels/cards** — one card per tier (Party Starter /
      People's Choice / Total Package), each with name, price range, and
      a clean feature list. Easier to compare, easier to scan, looks
      intentional instead of accidental.
- [ ] **FAQ page: convert from alternating black/gold sections into an
      accordion.** Short Q&A content in the current alternating-section
      layout produces a rapid zebra-stripe effect with nothing to anchor
      the eye. Collapsed-by-default accordion solves the striping and
      makes the page feel shorter/less overwhelming at a glance.
- [ ] Pull visual/structural inspiration from champsdj.com's existing
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
   champsdj.com)
3. Reviews page rebuild using the sourced reviews above
4. champsentertainment.com visual redesign (pricing cards, FAQ
   accordion, general de-centering, drawing from champsdj.com's design
   system)
5. Hero video/photo swap — whenever real wedding footage/photos are
   available
6. champsdj.com Friends section replacement + footer copy fix
      (lower priority, business site comes first)
