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
individual HTML file, which had drifted out of sync between pages over
time. It was consolidated into the single `css/styles.css` file
described above.

In September 2026, the site went through a full content and visual
redesign: champsentertainment.com was split from champsdj.com into a
dedicated business-facing brand, several pages were cut, renamed, or
reframed around booking rather than the DJ persona, and the visual
design was overhauled — a real component system replaced ad-hoc
emoji-bulleted text, the color/type/spacing system was formalized, and
the site moved from all-caps everywhere to a deliberate casing rule.
See **Branding Kit** below for the resulting design reference, and
**Website Redesign Project** for what's still open.

## Branding Kit

A reference for colors, type, spacing, and component patterns — built
directly from `css/styles.css`. Use this instead of re-deriving design
decisions from scratch each time. **This documents champsentertainment.com
only.** champsdj.com is being deliberately left alone for now — that
site gets its own pass once the business-site work here is finished.

**Sister brand:** champsdj.com is Champs' separate artist-facing site
(mixes, releases, live sets). The two intentionally share design DNA
(dark backgrounds, a gold accent, a real card system, deliberate type
pairing) without being visually identical — champsdj.com is more
energetic and nightlife-coded; this brand is calmer and more premium.

### Color

Single dark theme — this brand does not have a light mode.

| Token | Value | Usage |
|---|---|---|
| `--bg` | `#0a0a08` | Page background |
| `--bg-raised` | `#131310` | Card/panel background (pricing cards, review cards, FAQ items, contact form, highlight cards) |
| `--gold` | `#C8A700` | Primary accent — headlines, links, active nav, button borders, card borders. **This exact value matches the logo image assets.** Do not substitute champsdj.com's gold (`#d8bb1b`) — they're deliberately different. |
| `--gold-bright` | `#e8c400` | The "premium tier" glow — used on the `.pricing-card.premium` variant (currently the Total Package tier on weddings.html) to make the highest-priced option visually stand out with a glow effect and a "Deluxe" badge, distinct from the plain gold `.featured` badge used for "Most Popular." |
| `--ink` | `#f5f2e6` | Primary text — a soft off-white, not pure `#fff` |
| `--ink-dim` | `#b8b39f` | Secondary/muted text — captions, review locations, form disclaimers |
| `--line` | `#2a2a20` | Borders and section dividers |

A note on why sections don't flash gold anymore: the original site
alternated section backgrounds to solid gold on scroll. That's gone —
sections now use a single consistent `--bg`, separated by a subtle
`--line`-colored top border. If a color accent between sections is
ever wanted again, use `--bg-raised` for a raised-panel feel instead
of a jarring color swap.

### Typography

Two typefaces, both loaded from Google Fonts (see the single `<link>`
in every page's `<head>`):

- **Bricolage Grotesque** (weights 600–800) — the display face. Used
  for `h1`, `h2`, `h3`, and short punchy UI moments (pricing card
  names, quote-callout text).
- **Public Sans** (weights 400–600) — the body face. Used for
  paragraphs, list items, form fields, review quotes, FAQ answers —
  anything meant to be read rather than glanced at.

Why this pairing: Bricolage Grotesque has real character and
confidence without being playful (unlike the old Nunito, which read
soft and bubbly at large bold sizes — close enough to Comic Sans MS
that it undermined the "premium wedding business" positioning). Public
Sans is clean and highly legible at paragraph size without being a
generic default. Together they lean toward the same confident-modern
register as champsdj.com's Archivo Black/Oswald pairing, using
entirely different actual typefaces — the two sites read as siblings,
not clones.

**Casing:** headlines are sentence case, not ALL CAPS — "Wedding
packages," not "WEDDING PACKAGES." All-caps is reserved for small
structural UI text where it adds crispness without hurting legibility:
nav links, buttons, eyebrow/label text (e.g. a pricing card's "MOST
POPULAR" badge). At headline size, all-caps just shouts and is
measurably slower to read (capital letters remove the
ascender/descender shape cues your brain uses for fast word
recognition). *(Site-wide headline casing conversion, including FAQ
question text, is still pending — see Website Redesign Project
below.)*

**Type scale:**

| Style | Font | Size | Weight |
|---|---|---|---|
| Hero headline (h1) | Bricolage Grotesque | 50px | 800 |
| Section headline (h2) | Bricolage Grotesque | 32px | 700 |
| Subsection (h3) | Bricolage Grotesque | 24px | 700 |
| Paragraph | Public Sans | 18px | 400 |
| Small/caption | Public Sans | 14px | 400 |
| Eyebrow label | Public Sans | 13px | 600 |

### Alignment

The rule: **content-heavy text is left-aligned; short copy stays
centered.**

- Left-align: paragraphs of prose (About page narrative, service
  descriptions), FAQ answers, review quotes, list items.
- Stay centered: hero taglines, the homepage's DJ quote-callouts,
  short CTAs/buttons, card names inside a centered card grid.

A consistent left edge is what your eye anchors to across multiple
lines — centered paragraphs make your eye hunt for the start of each
new line, which gets fatiguing past a sentence or two. Short, punchy
text (a headline, a button, a pull-quote) doesn't have that problem,
and centering it is a legitimate way to create visual focus rather
than a default applied out of habit everywhere.

### Spacing & radius

A small, deliberate scale rather than one-off pixel values:

| Token | Value | Usage |
|---|---|---|
| `space-1` | 8px | Tight internal gaps (icon-to-text, list item padding) |
| `space-2` | 16px | Component-internal spacing (card gaps, form field gaps) |
| `space-3` | 24px | Card padding, grid gaps between cards |
| `space-4` | 40px | Spacing between related content blocks within a section |
| `space-5` | 56px | Section padding (top/bottom) — the rhythm between major page sections |

| Token | Value | Usage |
|---|---|---|
| `radius-sm` | 8px | Buttons, FAQ accordion items |
| `radius-md` | 12px | Cards: pricing cards, review cards, blog cards, highlight cards, contact form card |

### Component patterns

All defined in `css/styles.css`, all built on the tokens above:

- **Pricing card** (`.pricing-card` / `.pricing-grid`) — name, price,
  feature checklist, CTA. Supports a `.featured` variant (plain gold
  border + "Most Popular" badge) and a `.premium` variant (glowing
  `--gold-bright` border + "Deluxe" badge, for the highest-priced tier),
  plus a `.pricing-grid-2` variant for 2-item layouts.
- **Review card** (`.review-card` / `.review-grid`) — large gold star
  rating, name, location, quote with a gold left-border accent.
- **FAQ accordion** (`.faq-item` / `.faq-question` / `.faq-answer`) —
  gold-bordered, question background flips to solid gold with black
  text when expanded, answer stays in the card's normal dark coloring,
  chevron rotates 180° on open/close.
- **Quote callout** (`.quote-callout`) — bordered top/bottom divider
  for the homepage's DJ quotes.
- **Blog card** (`.blog-card` / `.blog-grid`) — the blog landing
  page's post cards.
- **Check list** (`.check-list`) — plain checkmark list, replacing
  emoji ✅ bullets.
- **Highlight card** (`.highlight-card`) — wraps each Event Highlights
  entry.
- **Contact card** (`.contact-card`) — wraps the contact form.

### Assets

Logo images live in `Images/` in this repo
(`Champs_Ent_Logo_Gold_social2_transparent.png` and variants). No
separate asset library exists yet — this is the single source.

### Icons

Font Awesome, loaded via CDN — not a custom/owned icon set. Decided:
staying with Font Awesome. It's the standard, low-cost choice for a
business at this scale; commissioning custom icons would add real
cost and complexity for very little practical benefit here.

## Website Redesign Project (planning as of September 2026)

Everything below is what's still open. Settled work is summarized in
**History** above and reflected in **Branding Kit**; this list only
shows unfinished checklist items, unresolved questions, and anything
still undecided.

### champsentertainment.com — content changes

- [ ] **Hero video swap (wedding footage instead of club footage) —
      SHELVED for now**, pending real photo/video being available from an
      actual wedding he's played. Decision made: keep current club
      footage as placeholder in the meantime rather than substitute
      generic stock wedding footage — recognizable stock footage risks
      undercutting the "this is a real professional" trust the rest of
      the site is building. A single strong real photo (not necessarily
      video) is an acceptable lower-effort placeholder once available.

### Remaining order of operations

1. Hero video/photo swap — whenever real wedding footage/photos are
   available

### Outstanding notes and open questions

- **2027 reminder:** when a new press kit PDF is generated,
  `presskit.html`'s redirect target (and the direct link from
  champsdj.com's Book section) both need updating to the new
  filename/URL.

