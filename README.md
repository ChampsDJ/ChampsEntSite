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
  There are currently 19 HTML files with the site nav (12 core pages, `faq.html`
  and `404.html` as special cases with slightly different markup, plus the
  blog landing page and posts).
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
  `.blog-card` / `.blog-grid` styles in the main stylesheet. Only the
  card title, excerpt, and "Read More" link are shown — the whole card is
  intentionally **not** a click target, only "Read More" is.
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
