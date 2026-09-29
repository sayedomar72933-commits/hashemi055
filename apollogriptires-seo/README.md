# apollogriptires.com — SEO fix kit

Audit date: 2026-09-29. Sources: Hostinger file access, the site's `llms.txt`
(which lists every published page and post), and Google's index. The live site
could not be loaded from the audit environment, so every change below should be
checked in a browser after it is applied.

## Step 1 — Recover the old URLs (highest impact)

The June 2026 rebuild changed the URL structure. Google still ranks the old
URLs below, none of them exist among the current pages, and the Yoast redirect
list is empty. Each one is probably returning a 404.

**Before applying:** open Google Search Console → Indexing → Pages →
"Not found (404)" and confirm these URLs are listed. If an old URL still
loads a real page, remove its line from the redirect file.

| Old URL | Redirect to | Better long-term fix |
|---|---|---|
| /about | /about-us/ | — |
| /brampton | /locations/brampton-location/ | — |
| /flat-tire-repair | /services/flat-tire-repair/ | — |
| /mobile-tire-services | /services/mobile-tires-services/ | — |
| /new-tires-for-sale | /services/tire-sales/ | — |
| /used-tires-for-sale | /services/tire-sales/ | **Rebuild**: used tires is a core offer with no page now |
| /battery-boost | /services/mobile-tires-services/ | **Rebuild** as its own service page |
| /mobile-tire-service-areas | /services/mobile-tires-services/ | **Rebuild** as a hub linking every city page |
| /tire-services-in-toronto | /services/mobile-tires-services/ | **Rebuild at the same URL** |
| /tire-services-north-york | ″ | ″ |
| /tire-services-etobicoke | ″ | ″ |
| /tire-services-in-markham | ″ | ″ |
| /tire-services-in-vaughan | ″ | ″ |
| /tire-services-in-maple | ″ | ″ |
| /mobile-tire-richmond-hill | ″ | ″ |
| /tire-services-newmarket | ″ | ″ |
| /tire-services-king-city | ″ | ″ |
| /tire-services-in-oshawa | ″ | ″ |
| /tire-services-in-whitby | ″ | ″ |

The city pages were your local-search landing pages. Redirecting 11 cities to
one generic page stops the 404s, but Google may treat it as a "soft 404" and
the city rankings will fade. The best fix is to recreate each city page **at
its old URL**, with unique content for that city: response time, streets or
areas covered, local FAQs, and a map. Then delete that city's redirect.
Ajax, Pickering, Aurora, Stouffville, Scarborough and Mississauga are named
in your service area but never had pages. Those are new pages to build.

### How to apply (pick ONE)

- **Yoast Premium (recommended):** WordPress admin → Yoast SEO → Redirects →
  Import/Export → import `redirects-yoast.csv`. Easy to edit or undo later.
- **.htaccess:** paste `redirects.htaccess` above `# BEGIN WordPress` in
  `public_html/.htaccess` (hPanel → File Manager). Back up the file first.

Afterwards: purge the LiteSpeed cache, test 3–4 old URLs in a private window,
then in Search Console use URL Inspection → Request indexing on the targets.

## Step 2 — Tracking cleanup (5 minutes)

WordPress admin → Nexter → Code Snippets:
- Delete **both** "Add Google Analytics Tracking Code" snippets. They load
  `gtag.js?id=YOUR-ID`, a placeholder that was never replaced. Let Site Kit
  handle Analytics.
- The other four snippets are each installed twice. Delete one copy of each:
  Disable Emojis, Limit Post Revisions, Customize Login Logo Link, Disable
  Gutenberg.

## Step 3 — Name, address and phone (NAP) and schema

- Pick one brand spelling ("ApolloGrip Tires") and use it everywhere: site
  title, Google Business Profile, social media, directories. Merge or retire
  one of the two Instagram accounts.
- There are **three real branches**, each with its own Google Business
  Profile. Every place (website, GBP, directories) must show exactly these
  details:

| Branch | Address | Phone | Hours |
|---|---|---|---|
| Brampton | 2080 Steeles Ave E, Unit 4 (Steelcom Business Centre), Brampton, ON L6T 5A5 | 437-898-8595 | Mon–Sat 9–8, Sun 9–6 |
| Mississauga (General Rd) | 5266 General Rd, Unit 8, Mississauga, ON **L4W 1G8** | 437-616-7504 | Daily 9–7 |
| Mississauga (Cawthra Rd) | 2355 Cawthra Rd, Mississauga, ON L5A 2W7 | 437-766-7504 | Mon–Sat 9–8, Sun 10–8 |

- ⚠️ **Postal code mismatch:** Google Maps has General Rd as **L4W 1G8**,
  but the website and Google's index show **L4W 1Z7**. Check which one Canada
  Post uses for 5266 General Rd, then correct the other one.
- All three GBPs link only to the homepage. Point each profile's "Website"
  link at its own location page:
  - Brampton → `/locations/brampton-location/`
  - General Rd → `/locations/mississauga-location/`
  - Cawthra → `/tire-shop-cawthra-road-mississauga/`
- The Cawthra page sits outside `/locations/`. Keep its URL, but link it
  from the `/locations/` overview page, the footer, and the Contact page.
- Each location page needs: the NAP above, hours, a click-to-call phone
  link, an embedded Google map, and a link to that branch's reviews.
- **Schema:** paste the matching `schema-*.html` file into that page. In
  Elementor, use an HTML widget; in Yoast Local, enter the same details under
  Locations. Use one method, not both, to avoid duplicate markup. After
  publishing, test each page at https://search.google.com/test/rich-results.
  If the site doesn't really do TPMS service, remove it from `makesOffer`.
- Fix the tagline in Settings → General. It shows as "Ontario&#039;s #1 Tire
  Shop" in `llms.txt`; use a plain apostrophe and drop the unverifiable "#1".

## Step 4 — Make pages match the real business

The current page descriptions claim a full mechanical garage, laser alignment,
computerized diagnostics, and an online catalogue
of "thousands of treads". The shop pages (/shop/, /shop/by-size/,
/shop/by-vehicle/) have no store behind them, because WooCommerce isn't
installed. Rewrite them around what you actually offer: new and used tires,
rims, balancing, seasonal swaps, flat repair, 24/7 mobile service, battery
boosts and fuel delivery. Turn the shop pages into quote-request forms.

## Step 5 — Blog consolidation

Merge each group into one post and 301 the others to it:
- Brampton "best/top tire shop" (3 posts)
- Mississauga "best/top tire store" (3 posts)
- Michelin (3 posts)

Delete or redirect "Top All-Terrain Vehicles for Adventurous Driving", which
is off-topic. Move "Same-Day Tire Installation" into a service page. Rewrite
the remaining posts with real local detail: prices, how long jobs take,
seasonal timing in Peel, and quotes from your technicians.

## Step 6 — Media

Replace the Getty stock photos with real shop, van and team photos, using
descriptive filenames and alt text. Delete the theme-demo leftovers
(`food-table-delicious-meal…`, `talkiai-hero-section…`, `placeholder.png`,
`blog-thumb-single*`, `author-thumb-1*`). Convert the 450–715 KB hash-named
PNGs to WebP. In the site root, remove `default.php`, `.htaccess.bk`,
`.htaccess_original` and `readme.html`.

## Applied in Elementor (2026-09-29)

Done through the Elementor MCP connection and published:
- **Location pages** (Brampton #40, General Rd #42, Cawthra #1478): new
  "Visit ApolloGrip Tires …" section above the map with address, hours,
  click-to-call phone, and Directions / Google reviews buttons.
- **Locations overview** (#38) and **Contact** (#35): new "three branches"
  section with each branch's NAP and hours, linking all three location pages
  (Cawthra Rd included).
- **Main Footer** (#330): "Our locations" line linking all three branches.
- The live site shows General Rd as L4W 1G8 on every page checked.

Not possible through this connection, so these still need to be done by hand:
- **Schema (Step 3):** there is no atomic HTML widget, and Custom Code
  snippets can't be edited through the connector. Paste each `schema-*.html`
  into an HTML widget on its location page in the Elementor editor.
- **Legacy (V3) widgets are read-only through the connector**: the existing
  page text, FAQ accordions, icon boxes and forms. That covers the Step 4
  rewrites (garage and "thousands of treads" claims) and turning the /shop/
  pages into quote forms.
- Everything outside Elementor: redirects (Step 1), Nexter snippets (Step 2),
  the tagline (Settings → General), blog consolidation (Step 5) and media
  cleanup (Step 6).
