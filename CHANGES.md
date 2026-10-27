# Nanny Network — Development Changes Log

Project: **Nanny Network** marketing site
Stack: HTML5, CSS3 (single stylesheet `nanny-network.css`), Vanilla JS (`nanny-network-script.js`)
Files touched: `index.html`, `nanny-network.css`

This document records **what was changed**, **challenges encountered**, and **how each was solved**.

---

## 1. Summary of Work

| #   | Area              | What changed                                                             |
| --- | ----------------- | ------------------------------------------------------------------------ |
| 1   | Hero phone mockup | Replaced the live/CODED phone UI with a real product screenshot image    |
| 2   | Phone nav bar     | Restored the bottom app-nav bar overlaid on the new mockup image         |
| 3   | Font Awesome      | Fixed a broken CDN link and added social media icons in the footer       |
| 4   | Footer social     | Converted plain-text social links ("Facebook", etc.) into icon links     |
| 5   | Brand palette     | Replaced the pastel palette with the official Nanny Network brand colors |
| 6   | Header button     | Recolored the "Login" CTA to Deep Teal (coral on hover)                  |
| 7   | Footer            | Recolored to a Deep Teal → Deep Charcoal gradient with light text        |
| 8   | Site background   | Set the page canvas to Soft Cream `#F8F9FA`                              |
| 9   | Supporting UI     | Aligned logo, badges, hero buttons, and Download CTA to the new palette  |
| 10  | Bug fixes         | Repaired broken CSS (orphaned `.shape` rule) and invalid color variables |

---

## 2. Detailed Changes

### 2.1 Hero Phone Mockup (HTML)

**Before:** The hero used a fully hand-coded "living" phone UI (clock, greeting, mood buttons,
breathing card) with an accompanying bottom nav.

**After:** The coded UI was removed and replaced with the real product screenshot
(`nanny_mockup.jpg`) filling the phone screen, with the app nav bar overlaid on top.

```html
<div class="phone-mockup">
  <div class="phone-screen">
    <img
      src="nanny_mockup.jpg"
      alt="Nanny Network app preview"
      class="phone-mockup-img"
    />
    <div class="phone-nav">
      <div class="phone-nav-item active">🏠</div>
      <div class="phone-nav-item">📝</div>
      <div class="phone-nav-item">🎵</div>
      <div class="phone-nav-item">⚙️</div>
    </div>
  </div>
</div>
```

**CSS added** so the image fills the phone screen and inherits the rounded corners
(via the parent `.phone-screen { overflow: hidden; border-radius: 35px; }`):

```css
.phone-mockup-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top center;
  display: block;
}
```

The `.phone-nav` bar remains absolutely positioned at `bottom: 20px`, so it sits exactly
where the original nav did, layered above the image.

---

### 2.2 Font Awesome (Icons)

**Problem:** The `<head>` link for Font Awesome was incomplete and pointed to a non-existent
file, so no icons loaded:

```html
<!-- BROKEN -->
<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/"
/>
```

**Fix:** Replaced it with the correct, versioned CDN URL:

```html
<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css"
/>
```

**Footer social links** were changed from text to Font Awesome brand icons:

```html
<div class="footer-social">
  <a href="#" class="social-icon" aria-label="Facebook"
    ><i class="fa-brands fa-facebook-f"></i
  ></a>
  <a href="#" class="social-icon" aria-label="Instagram"
    ><i class="fa-brands fa-instagram"></i
  ></a>
  <a href="#" class="social-icon" aria-label="TikTok"
    ><i class="fa-brands fa-tiktok"></i
  ></a>
  <a href="#" class="social-icon" aria-label="X"
    ><i class="fa-brands fa-x-twitter"></i
  ></a>
</div>
```

The existing `.social-icon` rule already centers its content with flexbox, so it needed only
minor tweaks (explicit `color` and `text-decoration: none`) to display the icons cleanly.

---

### 2.3 Brand Palette (`:root`)

The official Nanny Network palette was applied to the CSS variables:

```css
:root {
  /* ===== Nanny Network Brand Palette ===== */
  --teal: #2a9d8f; /* Deep Teal - primary brand color */
  --teal-deep: #23817a; /* darker teal (hovers/depth) */
  --coral: #e76f51; /* Warm Coral - accent */
  --coral-hover: #d65a3c; /* coral hover */
  --charcoal: #264653; /* Deep Charcoal */
  --charcoal-deep: #1c343d; /* darker charcoal */
  --cream: #f8f9fa; /* Soft Cream - page background */
  --white: #ffffff;

  /* Soft supporting tints (kept for existing components) */
  --peachy: #fbe3db;
  --peachy-deep: #f6cfc1;
  --mint: #e3f5f1;
  --mint-deep: #c3ebe4;
  --lavender: #e7edef;
  --lavender-deep: #d3dfe2;
  --sage: #8fb29a;

  /* Text */
  --text-dark: #264653;
  --text-light: #5f7580;
}
```

| Role        | Color         | Hex       |
| ----------- | ------------- | --------- |
| Primary     | Deep Teal     | `#2A9D8F` |
| Accent      | Warm Coral    | `#E76F51` |
| Text / dark | Deep Charcoal | `#264653` |
| Background  | Soft Cream    | `#F8F9FA` |

---

### 2.4 Header Button — `.nav-cta` (Login)

```css
.nav-cta {
  background: var(--teal); /* Deep Teal */
  color: var(--white);
  box-shadow: 0 5px 20px rgba(42, 157, 143, 0.35);
}
.nav-cta:hover {
  background: var(--coral); /* Warm Coral */
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(231, 111, 81, 0.45);
}
```

Result: a high-contrast teal pill on the light nav bar, with a coral hover for feedback.

---

### 2.5 Footer

```css
footer {
  background: linear-gradient(180deg, var(--teal) 0%, var(--charcoal) 100%);
  color: var(--white);
}
```

- Footer text, headings, and links switched to **light/white** values for contrast.
- Social icons: translucent white circles, **coral on hover**.
- Footer bottom border and text opacity tuned for the dark background.

---

### 2.6 Site Background — `body`

```css
body {
  background: var(--cream); /* Soft Cream #F8F9FA */
  color: var(--text-dark); /* Deep Charcoal */
}
```

---

### 2.7 Supporting / Consistency Edits

- `.logo` — hardcoded pink `#d97b7b` → **Charcoal** (`var(--charcoal)`).
- `.hero-badge` — pink background/text → **mint** background with **teal** text.
- `.section-badge` — hardcoded green text → **teal-deep**.
- `.btn-primary` (hero "Find a Nanny") — coral with **coral-tinted** shadows.
- `.nav-links a:hover` — coral tint → **mint** background with teal text.
- `.mood-btn.active` — box-shadow updated to coral.
- `.mobile-menu-cta` — switched from coral to **teal** with teal-deep hover.
- `.download-cta` — see bug fix below; text set to white, App Store / Google Play buttons set to **coral**.

---

## 3. Challenges Encountered & How They Were Solved

### Challenge 1 — Broken Font Awesome CDN

**Symptom:** Social icons rendered as blank/nothing.
**Cause:** The stylesheet URL was truncated (`.../font-awesome/`) and had no version or file path.
**Solution:** Used the correct pinned CDN URL for Font Awesome 6.5.1 (`.../6.5.1/css/all.min.css`).

### Challenge 2 — Orphaned CSS rule broke `.shape`

**Symptom:** The floating background shapes lost their base styling.
**Cause:** While inserting the new `.phone-mockup-img` rule, it was placed in the middle of the
`.shape` rule, leaving properties like `border-radius`, `opacity`, and `animation` attached to
nothing.
**Solution:** Restored the `.shape` selector block and moved the phone mockup rules to the
correct location.

### Challenge 3 — Invalid CSS color keywords

**Symptom:** The page background behaved unpredictably.
**Cause:** `body { background: dark teal; }` — `dark teal` is not a valid CSS color keyword,
so browsers ignored it (falling back to white).
**Solution:** Replaced with `background: var(--cream);` (Soft Cream `#F8F9FA`).

### Challenge 4 — Non-existent gradient variables

**Symptom:** The Download CTA section had no visible background.
**Cause:** `background: linear-gradient(180deg, var(--green) 0%, var(--black) 100%);` referenced
`--green` and `--black`, which were never defined in `:root`.
**Solution:** Replaced with a defined brand gradient
(`var(--charcoal)` → `var(--teal)`) and adjusted the section's text to white.

### Challenge 5 — Placeholder image inside a flex layout

**Symptom:** The mockup image rendered at its natural size instead of filling the phone.
**Cause:** The `<img>` was initially placed inside `.phone-clock-wrapper`, a small centered
flex container meant for clock text.
**Solution:** Moved the image to be a direct child of `.phone-screen` and added
`.phone-mockup-img` with `width/height: 100%` and `object-fit: cover`.

### Challenge 6 — Dark footer text on dark footer background

**Symptom:** After the footer became a teal→charcoal gradient, dark text became unreadable.
**Cause:** Footer text variables were still dark (`--text-dark`).
**Solution:** Switched all footer text/links to white / translucent-white values and lighter
hover accents.

---

## 4. Known Outstanding Item (Recommend Follow-up)

**Features section — stray/misplaced markup around the 6th card.**
In `index.html`, the sixth feature card ("Tailored Family Matching") has a commented-out
opening `<div class="feature-card reveal">` but a live, un-commented block for
`habits-screenshot` and its closing structure. This leaves an unbalanced/misplaced closing
`</div>` and the card wrapper is not correctly applied.

**Recommended fix:** Re-wrap the sixth card cleanly, e.g.:

```html
<div class="feature-card reveal">
  <div class="feature-image">
    <div class="feature-image-inner">
      <div class="feature-screenshot habits-screenshot">
        <div class="habits-title">🎯 Match Criteria: 98%</div>
        <div class="habits-list">
          <!-- habit-items ... -->
        </div>
      </div>
    </div>
  </div>
  <div class="feature-content">
    <h3>Tailored Family Matching</h3>
    <p>...</p>
    <span class="feature-tag">Smart Match Technology</span>
  </div>
</div>
```

---

## 5. How to Reuse / Edit Colors Going Forward

Two approaches are supported:

1. **Global edit (recommended for brand-wide changes):** change a value once in `:root`
   (e.g., set `--teal` to a new hex) and every element that references it updates automatically.

2. **Per-section edit:** replace `var(--x)` inside a specific rule with a literal hex
   (e.g., `background: #ffffff;`) so that section/ card can be tuned independently without
   affecting others. Great for one-off card tints.

### Suggested brand-consistent values

| Purpose                            | Use                                              |
| ---------------------------------- | ------------------------------------------------ |
| Primary actions (Login, links)     | `--teal` / `--teal-deep`                         |
| Accents / highlights (hover, tags) | `--coral` / `--coral-hover`                      |
| Headings & body text               | `--charcoal` / `--text-dark`                     |
| Page background                    | `--cream`                                        |
| Dark sections (footer, CTA)        | `--teal` → `--charcoal` gradient with white text |

---

## 6. Files Changed

- `index.html`
  - Fixed Font Awesome CDN link.
  - Replaced hero phone mockup with image + restored `.phone-nav`.
  - Converted footer social links to Font Awesome icons.
- `nanny-network.css`
  - New brand `:root` palette.
  - `body` background set to Soft Cream.
  - `.nav-cta` (header button) → Deep Teal / coral hover.
  - `footer` → teal→charcoal gradient with light text.
  - `.download-cta` fixed gradient + white text + coral app buttons.
  - Consistency edits: `.logo`, `.hero-badge`, `.section-badge`, `.btn-primary`,
    `.nav-links a:hover`, `.mood-btn.active`, `.mobile-menu-cta`, `.social-icon`.
  - Bug fixes: restored `.shape` rule; removed invalid color values.

---

# Part 2 — Content, Imagery & Video Pass

Follow-up work after the brand-color pass above. Only **new** changes and **new** challenges are listed here.

## 7. Header & Navigation

- **Logo path verified:** `src="nanny_network.jpg"` confirmed as the correct relative path for both header and footer logos.
- **Brand styling pointers:** identified the exact CSS lines to tweak the navbar background, brand teal text (`#1d4e5f`), and the Login CTA button (`#f1705a`).

## 8. Hero Background Video

- **HTML:** added a background video to the hero — `<video autoplay muted loop playsinline class="hero-bg-video">` pointing to `video/hero_background_video.mp4`.
- **Containment:** added `overflow: hidden;` and `position: relative;` to `.hero` so the video stays confined to the hero and never bleeds into the nav or sections below.
- **Legibility:** added `.hero-overlay` (`rgba(253, 251, 247, 0.78)` + `backdrop-filter: blur(1px)`) and raised the content to `z-index: 2`, keeping headings, buttons, and the mockup crisp over moving video.

## 9. Feature Section — Real Photography

All 6 cards now use real photos, with the original template markup kept as comments. Each emoji/mockup was replaced:

| Card | Title                      | New asset                           |
| ---- | -------------------------- | ----------------------------------- |
| 1    | Vetted Care-givers         | `images/vetted_care_asset.jpg`      |
| 2    | On Demand & Recurring Care | `images/nanny_card_assets.jpg`      |
| 3    | Real Time Care Updates     | `images/realtime_asset.jpg`         |
| 4    | Trusted Community Ratings  | `images/nanny_community_asset.jpg`  |
| 5    | Direct Chat & Seamless Pay | `images/seamless_payment_asset.jpg` |
| 6    | Tailored Family Matching   | `images/tailoredagency_asset.jpg`   |

## 10. Card Background Tints & High-Contrast Typography

- **Per-card tints:** Card 1 `#fdf5f2`, Card 2 `#eef8f5`, Card 3 `#f2f5f9`, Card 4 `#fdf8ef`, Card 5 `#fff6ee`, Card 6 `#edf7f6`.
- **Text contrast (WCAG AAA):** headings (`h3`) darkened to `#1c343d` (~12:1); paragraphs (`p`) darkened to `#37474f` (~8.5:1); `.feature-tag` pills set to solid white with teal text (`#23817a`) and a subtle shadow.
- **Asset styling:** added `.feature-asset-img` with `object-fit: cover; border-radius: 24px;` and a soft hover zoom (`transform: scale(1.05)`).

## 11. App Preview — Childcare Screens

- Commented out the old mindfulness/breathing phone screens and built 3 childcare preview screens:
  1. **Caregiver Profile** — top match "Sarah M.", CPR/Verified badges, 4.9 rating, "Available Today".
  2. **Live Care Feed** — daily routine timeline (Snack, Nap Time, Sensory Play).
  3. **Daily Care Log** — real-time parent note signed by the nanny.
- Matching styles added to `nanny-network.css`.

## 12. Testimonials

- Replaced the cartoon emojis with client photos: Uche K. → `images/review_uche.jpg`, Alexander Agidi → `images/review_alexander.jpg`, Idowu A. → `images/review_idowu.jpg`.
- Added `.testimonial-avatar-img` (70px circular frame, white border, drop shadow).

## 13. Download CTA Store Buttons

- Replaced the temporary `🍎` / `🤖` emojis with Font Awesome 6 vectors: `<i class="fa-brands fa-apple"></i>` and `<i class="fa-brands fa-google-play"></i>`.

---

## 14. New Challenges & Solutions (Part 2)

| #   | Challenge                                        | Root cause                                                                                                                                             | Solution                                                                                                                                                                 |
| --- | ------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | **Broken Card 6 layout**                         | Opening wrappers were accidentally caught inside a comment tag while their closing `</div>`s stayed active, breaking the grid                          | Audited the DOM, restored the outer card/image wrappers, verified grid alignment                                                                                         |
| 2   | **Special-character filename**                   | Image on disk was `nanny_card_assets (2).jpg` (spaces + parentheses), risking URL-encoding/404 issues                                                  | Saved a clean copy `nanny_card_assets.jpg` so the path works reliably                                                                                                    |
| 3   | **Video spilling past the hero**                 | Absolutely-positioned full-screen video can overflow its parent, pushing later sections / covering the header; text over moving video was hard to read | `overflow: hidden` on `.hero` as a clipping mask, centered the video with `transform: translate(-50%, -50%)`, and layered a translucent cream overlay with backdrop blur |
| 4   | **Template vs. Nanny Network content confusion** | Original "Mochi Space" template was a wellness app; two separate sections still showed mindfulness mockups ("Breathe in...", "Morning coffee...")      | Updated the Features grid with real assets and rebuilt the App Preview mockups with childcare UI                                                                         |
| 5   | **Text contrast on tinted cards**                | Light gray body text on near-white backgrounds became washed out once colored tints were added                                                         | Applied WCAG AAA checks: headings `#1c343d`, body `#37474f`, solid white tag pills with dark teal text                                                                   |
| 6   | **Preserving prior code**                        | Needed every change to be instantly reversible without breaking the DOM                                                                                | Wrapped every replaced block in `<!-- PREVIOUS CODE (COMMENTED OUT) ... -->` and CSS `/* ... */` comments                                                                |

> Note: the item previously flagged in **Section 4** above (the Card 6 markup) is now resolved — see Challenge 1 in this table.

---

_Document generated to accompany the Nanny Network site build on 13th October, 2026._
