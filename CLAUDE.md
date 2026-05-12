# CLAUDE.md — Family Travel Planner

This file tells Claude exactly how to add a new country to `countries.json`.

---

## How This Works

- `countries.json` — all travel data. **The only file you ever edit.**
- `index.html` — the template. **Never touch this file.**
- Add a country → paste a new JSON object into `countries.json` → it appears everywhere automatically (nav, home cards, comparison table, all 4 tier list views).

---

## Standard Continent Names

Always use **exactly** one of these strings in the `"continent"` field:

| String | Countries |
|--------|-----------|
| `"Southeast Asia"` | Singapore, Thailand, Malaysia, Vietnam, Philippines, Indonesia, Cambodia, Laos |
| `"East Asia"` | Japan, South Korea, China, Taiwan |
| `"South Asia"` | Nepal, Sri Lanka, Maldives, Bhutan, India |
| `"Middle East"` | UAE, Qatar, Oman, Jordan |
| `"Central Asia"` | Kazakhstan, Uzbekistan, Kyrgyzstan, Tajikistan |
| `"Caucasus"` | Georgia, Armenia, Azerbaijan |
| `"Europe"` | Turkey, Greece, Italy, France, etc. |
| `"Africa"` | Morocco, Kenya, Tanzania, etc. |
| `"Americas"` | USA, Mexico, Peru, Brazil, etc. |
| `"Oceania"` | Australia, New Zealand, Fiji, etc. |

---

## Price Tier Reference

| Tier | Meaning | Typical 4-day budget (family of 3) |
|------|---------|-------------------------------------|
| `"S"` | Shockingly Cheap | Under ₹1L |
| `"A"` | Affordable | ₹1L–₹1.6L |
| `"B"` | Moderate | ₹1L–₹2L |
| `"C"` | Expensive | ₹1.5L–₹3L |
| `"F"` | Overpriced | ₹2L+ |

---

## Kid Score Reference (for a 6-year-old girl)

| Score | Meaning |
|-------|---------|
| `5` | World-class (theme parks, zoos, kid infrastructure) |
| `4` | Excellent (great activities, very manageable) |
| `3` | Good (decent options, some adult-focused) |
| `2` | Limited (beautiful but few kid-specific activities) |
| `1` | Adults only |

---

## JSON Schema — Every Field

```json
{
  "id": "xx",
  "name": "Country Name",
  "flag": "🇽🇽",
  "accentColor": "#rrggbb",
  "heroGradient": "linear-gradient(160deg,#xxxxxx 0%,#1a0a0a 55%,#0a1a2a 100%)",
  "kidScore": 4,
  "kidScoreDisplay": "⭐⭐⭐⭐",
  "priceTier": "B",
  "continent": "Southeast Asia",
  "flightTime": "~5h direct",
  "directFlight": true,
  "visa": "Visa-free ✅",
  "budgetRange": "₹90K–1.5L",
  "rank": 18,
  "isWarning": false,
  "homeCardSummary": "2–3 sentence description for the home card. What makes this country special for a family. Key highlights.",
  "heroTagsHtml": "<span class='hero-tag'>✈️ Direct ~5h</span><span class='hero-tag'>🎯 Key Highlight</span>",
  "heroNoticeHtml": "⭐ <strong>Key selling point.</strong> Why this country is worth visiting for this family.",
  "overviewHtml": "...HTML content for the Overview tab...",
  "d1Html": "...HTML content for the Day 1 detail tab...",
  "d2Html": "...HTML content for the Day 2 detail tab...",
  "d3Html": "...HTML content for the Day 3 detail tab...",
  "d4Html": "...HTML content for the Day 4 detail tab...",
  "flightsHtml": "...HTML content for the Flights tab...",
  "hotelsHtml": "...HTML content for the Hotels tab...",
  "budgetHtml": "...HTML content for the Budget tab..."
}
```

---

## Field Rules

### Top-level structured fields

| Field | Type | Notes |
|-------|------|-------|
| `id` | string | Short lowercase key, e.g. `"sg"`, `"jp"`, `"nepal"`. Must be unique. No spaces. |
| `name` | string | Display name. Use `·` for sub-destinations: `"Indonesia · Bali"` |
| `flag` | string | Emoji flag |
| `accentColor` | string | Hex color. Used for nav button highlight, home card border, tab underline |
| `heroGradient` | string | CSS gradient string for the hero background |
| `kidScore` | integer | 1–5. Used in the kid score matrix (X-axis column) |
| `kidScoreDisplay` | string | Star emojis to show in home card. Use `½` for half stars: `"⭐⭐⭐½"` |
| `priceTier` | string | Exactly `"S"`, `"A"`, `"B"`, `"C"`, or `"F"` |
| `continent` | string | Must match exactly from the standard list above |
| `flightTime` | string | e.g. `"~5h direct"`, `"~8h via BKK"` |
| `directFlight` | boolean | `true` if there is a direct non-stop flight from HYD |
| `visa` | string | Short description: `"Visa-free ✅"`, `"e-Visa $25"`, `"Visa on arrival"` |
| `budgetRange` | string | e.g. `"₹90K–1.4L"` |
| `rank` | integer | Position in the home page grid (1 = best for kids). Set to next available number. |
| `isWarning` | boolean | `true` = hero shows amber warning box. `false` = green notice box |

### HTML content fields

All `*Html` fields contain raw HTML that is injected directly into the tab panel.

**Rules for writing HTML inside JSON strings:**
- Use `'single quotes'` for all HTML attributes (not double quotes)
- Escape any literal double quotes as `\"`  
- No newlines needed — write on one line or use `\n` if you prefer
- Use these existing CSS classes — they are already defined in the template:
  - Cards: `.card`, `.day-card`, `.hotel-card`
  - Labels: `.day-label`, `.day-title`, `.section-header`, `.section-icon`, `.section-title`
  - Tables: `.activity-table`, `.compare-table`, `.budget-table`
  - Badges: `.cost-badge`, `.cost-total`, `.recbadge`, `.gen-rec`
  - Hotels: `.hotel-rank`, `.hotel-name`, `.hotel-stars`, `.hotel-meta`, `.hotel-meta-item`, `.hotel-bullet`, `.gen-bullet`, `.hotel-grid`, `.hotel-stat`, `.hotel-stat-label`, `.hotel-stat-value`
  - Hotel ranks: `.gold-rank`, `.silver-rank`, `.bronze-rank`
  - Notices: `.notice`, `.notice-info`, `.notice-warn`, `.notice-green`, `.notice-red`, `.notice-icon`
  - Flights: `.flight-route`, `.flight-city`, `.flight-arrow`, `.flight-stop`

---

## Overview Tab — Standard Structure

The `overviewHtml` should contain 4 day-card divs in this pattern:

```html
<div class='section-header'><span class='section-icon'>📋</span><h2 class='section-title'>4-Day Itinerary — Country Name</h2></div>
<div class='notice notice-green'><span class='notice-icon'>✅</span><span>Key positive fact about this destination.</span></div>
<div class='card day-card' style='border-left:4px solid ACCENT_COLOR'>
  <div class='day-label' style='background:ACCENT_COLOR'>✈️ Day 1 · Arrival</div>
  <div class='day-title'>Title of Day 1</div>
  <table class='activity-table'><thead><tr><th>Time</th><th>Activity</th><th>Location</th><th>Cost (family)</th></tr></thead>
  <tbody>
    <tr><td>9:00 AM</td><td class='activity-name'>⭐ Activity description</td><td>Location name</td><td><span class='cost-badge'>💰 ₹X,XXX</span></td></tr>
    ...
    <tr><td colspan='3' style='text-align:right;font-weight:700'>Day 1 Total</td><td><span class='cost-total' style='background:ACCENT_COLOR'>~₹X,XXX</span></td></tr>
  </tbody></table>
</div>
... repeat for Day 2, Day 3, Day 4
```

---

## Hotels Tab — Standard Structure (3 hotels)

```html
<div class='section-header'><span class='section-icon'>🏨</span><h2 class='section-title'>Hotels — 3 Nights in City</h2></div>
<div class='card hotel-card' style='margin-top:24px'>
  <div class='hotel-rank gold-rank'>🥇 Luxury Pick</div>
  <div class='hotel-name'>Hotel Name</div>
  <div class='hotel-stars'>★★★★★</div>
  <div class='hotel-meta'><span class='hotel-meta-item'>📍 Address</span><span class='hotel-meta-item'>⭐ 4.7/5</span></div>
  <div class='hotel-bullet gen-bullet'>Key feature 1</div>
  <div class='hotel-bullet gen-bullet'>Key feature 2</div>
  <div class='hotel-grid'>
    <div class='hotel-stat'><div class='hotel-stat-label'>Per night</div><div class='hotel-stat-value'>~$X–X ≈ ₹X,XXX–X,XXX</div></div>
    <div class='hotel-stat'><div class='hotel-stat-label'>3 nights total</div><div class='hotel-stat-value'>₹X–X</div></div>
  </div>
  <div class='recbadge gen-rec'>⭐ My Recommendation</div>
</div>
... repeat with silver-rank, bronze-rank
```

---

## How to Add a New Country (Step-by-Step)

1. Ask Claude: *"Add [Country] to the travel planner JSON. Here is the trip context: [family profile, dates, budget, etc.]"*
2. Claude generates a complete JSON object following this schema
3. Open `countries.json` in GitHub
4. Click the pencil (Edit) icon
5. Find the last country object (before the final `]`)
6. Add a comma after the last `}`, then paste the new country object
7. Click "Commit changes"
8. Wait 60 seconds → refresh the live URL → new country appears everywhere

---

## Countries Already in the Planner

| ID | Country | Continent | Price Tier | Kid Score | Rank |
|----|---------|-----------|------------|-----------|------|
| sg | Singapore | Southeast Asia | C | 5 | 1 |
| jp | Japan | East Asia | C | 5 | 2 |
| th | Thailand | Southeast Asia | B | 5 | 3 |
| my | Malaysia | Southeast Asia | B | 4 | 4 |
| ae | UAE · Dubai | Middle East | C | 4 | 5 |
| nepal | Nepal | South Asia | S | 3 | 6 |
| vietnam | Vietnam | Southeast Asia | A | 4 | 7 |
| ph | Philippines | Southeast Asia | B | 4 | 8 |
| id | Indonesia · Bali | Southeast Asia | B | 4 | 9 |
| lk | Sri Lanka | South Asia | A | 3 | 10 |
| mv | Maldives | South Asia | F | 3 | 11 |
| bt | Bhutan | South Asia | B | 2 | 12 |
| kh | Cambodia | Southeast Asia | S | 3 | 13 |
| la | Laos | Southeast Asia | S | 3 | 14 |
| ge | Georgia | Caucasus | A | 3 | 15 |
| kz | Kazakhstan | Central Asia | B | 2 | 16 |
| uz | Uzbekistan | Central Asia | S | 2 | 17 |

**Next rank to use: 18**

---

## Example Prompt to Claude

> "Add South Korea to the family travel planner JSON. Family of 3 (husband, wife, 6-year-old girl) departing Hyderabad. Christian family, no Hindu temples, 4-day trip, luxury-focused. Focus on Seoul: LEGOLAND Korea, Gyeongbokgung Palace (exterior, not as a religious site), Bukchon Hanok Village, Han River cruise, K-pop museum. Via Singapore or Bangkok. Visa-free for Indians."

Claude will output a complete JSON object ready to paste.
