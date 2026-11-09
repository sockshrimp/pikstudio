# Source material for the PIK Studio website

Gathered 2026-11-09 from a cloud session using `curl` with a desktop Chrome User-Agent.
Nothing below is invented. Anything that could not be fetched is marked as such.

---

## 1. Instagram posts

### Summary: no captions or images could be retrieved

All six requests (embed page and post page for each of the three posts) returned HTTP 200 with
roughly 511 KB of HTML. Every response turned out to be Instagram's generic logged-out app shell,
not the post itself:

- The page's routing config says `"pageID":"httpErrorPage"`. Instagram served its error page,
  not a post or embed view.
- `<title>` is just `Instagram`.
- No `og:image`, `og:description` or any other `og:` meta tags.
- No caption markup (`Caption` classes or `edge_media_to_caption` data).
- No media CDN image URLs (`scontent*.cdninstagram.com` / `*.fbcdn.net`). The only
  `cdninstagram` URLs are static JS/CSS bundles on `static.cdninstagram.com`.
- The shortcode appears only once, in the requested URL path.

**No hostname was blocked by the network proxy.** `www.instagram.com` was reachable, but Instagram
would not serve post content to an unauthenticated server-side client. No image URL was found, so
there was nothing to download, and `assets/instagram/` contains no images.

| Post | Embed URL result | Post URL result | Caption | Images |
|---|---|---|---|---|
| `DfHSz8rA7sQ` | 200, `httpErrorPage` shell | 200, `httpErrorPage` shell | Not retrieved | None |
| `De6Lls9A18u` | 200, `httpErrorPage` shell | 200, `httpErrorPage` shell | Not retrieved | None |
| `DdfKvCyBme3` | 200, `httpErrorPage` shell | 200, `httpErrorPage` shell | Not retrieved | None |

URLs tried for each `<ID>`:
1. `https://www.instagram.com/p/<ID>/embed/captioned/`
2. `https://www.instagram.com/p/<ID>/`

**Ways to get the real content:**
- Have the account owner copy the captions and export the original photos from the Instagram app,
  then put them in `assets/instagram/<ID>-<n>.jpg`. Originals will also be higher quality than CDN copies.
- Use Instagram's official oEmbed endpoint (`graph.facebook.com/v*/instagram_oembed`), which needs a
  Meta app access token.
- Use the client-side `<blockquote class="instagram-media">` + `embed.js` snippet. This renders in the
  visitor's browser and does not need server-side scraping.

---

## 2. Reference site: Studio Botanic (https://www.studiobotanic.com)

Pages read: Home, About, Weddings (`/weddings-1`), Events (`/events-1`), Wedding Gallery,
Event Portfolio, Shop, Contact. Highlight Reel was not read.
Built on Squarespace. Adelaide (Gilbert Street, city).

### Section structure
- **Nav:** Home · Weddings · Events · Highlight Reel · Shop · About · Contact.
- **Home:** a one-paragraph brand statement, then three image tiles linking to the
  Wedding Gallery, Highlight Reel and Event Gallery, then two "Get in touch" calls to action
  (Wedding Enquiries / Event Enquiries).
- **Global footer on every page:** Wedding Enquiries / Event Enquiries buttons, Location,
  Hours ("By Appointment Only"), contact email.
- **Wedding Gallery / Event Gallery:** a short intro line, then one entry per real job:
  couple or event name, date, a 2–3 sentence description (palette, mood, named flower varieties),
  venue and photographer credits, and a "See the Gallery" link.
- **About:** very short. Designer's name (Nadia Travaglini), the categories they work in
  (weddings / fashion / events), and the same brand paragraph as the homepage.
- **Shop:** directs gifting to a separate sister retail brand ("Bloombar") rather than selling
  on the studio site.

### How they describe weddings / events / gifts
- **Weddings:** told through real weddings. Each entry describes the mood (soft, abundant,
  garden-like, romantic), the palette, and the hero flowers by name, e.g. hydrangeas, Queen Anne's
  lace and garden roses "en masse". The varieties are named specifically, not just "seasonal blooms".
- **Events:** the same case-study format. Each event gets a concept (a 1960s-style birthday, a
  "New York bistro" mood for a sporting-round event), followed by what was done: individually
  designed tables, suspended orchids with exposed roots. The focus is on immersive, sculptural design.
- **Gifts:** spun off to a separate boutique brand, positioned as the studio's artistry applied
  to gifting. It is described as high-end, seasonal and "floral meets fine art".

### Booking / appointments
- Separate **wedding** and **event** enquiry forms. They ask for as much detail as possible so they can quote accurately.
- After the form, the studio contacts the client to talk through details.
- They state the response time up front: replies within 7 business days, check your junk folder.
- The studio is **by appointment only**. There are no walk-in hours.

### Tone of voice
Minimal, editorial and artistic. Brand copy uses fashion-like phrasing ("feast for the senses",
"set the tone") and positions the work as beyond "traditional" floristry. The case-study copy is
descriptive and sensory. Very little copy overall: the photography does most of the work.

---

## 3. Reference site: Studio88flowers (https://studio88flowers.com.au)

Pages read: Home, Portfolio (`/weddings-events.html`), Wedding Packages, Event Florals,
About Us, Shop (Signature Collection), Contact.
Built on Floranext (florist e-commerce platform). Hindmarsh, Adelaide.

### Section structure
- **Top banner:** which years they are booking (2027–2028) and a complimentary 1-hour consultation offer.
- **Nav:** Wedding Packages · Portfolio · Event Florals · About (+ Meet Our Team) · Enquire
  (Wedding quote / Event quote / Book consultation) · Shop · Resources (Behind the Design,
  Flower Care, Delivery Locations, Guarantee, Blog, etc.).
- **Home:** a long-scroll sales page:
  1. Hero with the promise "we design, deliver, style and set up" and a "Check my date" button
  2. A horizontal "drag to explore" strip of real wedding images
  3. Four numbered value points (designed for your venue, setup included, upfront pricing,
     limited dates)
  4. Four wedding package tiers with "from" prices
  5. Meet the founder
  6. A short availability form (name, email, phone, date, message)
  7. Press and collaborations
  8. Real weddings (three featured couples)
  9. Event florals summary with a client quote
  10. List of venues they have worked at
  11. Testimonials ("Love Notes")
  12. A final "Check your date" call to action
- **Wedding Packages page:** compares the tiers, lists what each tier includes, has a "your
  wedding doesn't need to fit a box" section, explains what drives the final quote (guest count,
  venue scale, installations, season, setup), and lists what details to send.
- **Event Florals page:** event types (corporate, launches/activations, private celebrations,
  installations), three fixed-price "sets of five" table arrangements, a 4-step enquiry-to-event
  process, and an FAQ.
- **About:** studio philosophy, founder bio, a services list, and their approach (start with the
  venue, one connected floral direction, use scale with purpose).

### How they describe weddings / events / gifts
- **Weddings:** full-service and end to end: design, delivery, styling, on-site setup and pack-down
  ("you carry nothing"). Four named tiers with visible "from" prices. Note the site contradicts
  itself: the homepage and packages page say from $6,000, but the About page says from $8,000.
  They stress that the tiers are starting points, not rigid boxes, and frame planning around the
  question of what the flowers should do for the room.
- **Events:** corporate, brand and private events. Copy talks about working with brand colours,
  entry moments, bars and stages. Offers ready-to-order fixed-price table sets for clients who
  don't need a custom install, and custom quotes for larger events.
- **Gifts:** a small online "Signature Collection" of named arrangements. They describe their
  style as clean lines, refined palettes and sculptural form. Gifting is secondary to
  weddings and events. A separate retail florist the founder also owns handles everyday volume.

### Booking / appointments
- The main call to action everywhere is **"Check my date"**: a short form that asks for the date and a few details.
- Separate wedding and event quote forms (JotForm).
- A **complimentary 1-hour consultation**, booked through Square Appointments.
- A phone number with "Call now" buttons. The studio has a street address and is closed Sundays.
- They list exactly what to send: date, venue, guest count, priority floral moments, inspiration images.
- They create scarcity by saying they take a limited number of dates and the designer is on site for installation.

### Tone of voice
Polished and reassuring, with a sales focus. Confident and plain-spoken: short declarative
headings, numbered steps, roman-numeral lists. Heavy on local SEO ("Adelaide wedding florist"
repeated). The copy is practical (pricing, logistics, what to send) and backed up with testimonials,
press and venue names.

---

## 4. Content ideas for PIK Studio (drawn from both sites)

1. **Real work as short case studies:** name or occasion, date, palette, three or four named
   flower varieties, venue and photographer credit. This works better than a plain gallery.
2. **Separate "Weddings" and "Events" enquiry paths**, each asking for the details needed to
   quote: date, venue, guest count, where flowers matter most, inspiration images.
3. **Set expectations about response:** say how fast you reply and remind people to check spam.
4. **State "by appointment"** clearly in the footer and contact section if it applies.
5. **A "check my date" call to action** is simpler and more inviting than "request a quote".
6. **Optional transparent "from" pricing or tier framing**, presented as starting points rather
   than fixed packages.
7. **A short "how it works" process** (3–4 steps from enquiry to the day, including setup and pack-down if offered).
8. **A small fixed-price gifting or table-set range** as an easy entry point next to custom work.
9. **A venue list and testimonials** for local credibility.
10. **Let photography carry the page.** Keep copy short and sensory. Studio Botanic shows how
    little text is needed when the images are strong.

---

## 5. Fetch log

| URL | Result |
|---|---|
| instagram.com/p/{DfHSz8rA7sQ,De6Lls9A18u,DdfKvCyBme3}/embed/captioned/ | 200, error-page shell, no post data |
| instagram.com/p/{DfHSz8rA7sQ,De6Lls9A18u,DdfKvCyBme3}/ | 200, error-page shell, no post data |
| studiobotanic.com/, /about, /contact, /events-1, /weddings-1, /shop, /eventportfolio, /weddinggallery | 200 |
| studio88flowers.com.au/, /about-us, /event-florist-adelaide, /weddings-events.html, /wedding-flower-packages, /shop-our-signature-collection.html, /contact/, /behind-the-design | 200 |
