# CLAUDE.md — Family Travel Planner

This file tells Claude exactly how to add destinations to either JSON file.

---

## How This Works

| File | Purpose | Edit? |
|------|---------|-------|
| `index.html` | The template | ❌ Never touch |
| `countries.json` | All international destinations | ✅ Only file to edit for international |
| `india.json` | All India domestic destinations | ✅ Only file to edit for India |
| `CLAUDE.md` | This file | ✅ Update when adding new destinations |

Adding a destination = paste a JSON object into the right file → commit to GitHub → 60 seconds later it appears everywhere automatically (nav, home cards, comparison table, all 4 tier list views, its own full page).

---

## PART 1 — INTERNATIONAL (countries.json)

### Standard Continent Names

Always use **exactly** one of these strings in the `"continent"` field:

| String | Countries |
|--------|-----------|
| `"Southeast Asia"` | Singapore, Thailand, Malaysia, Vietnam, Philippines, Indonesia, Cambodia, Laos |
| `"East Asia"` | Japan, South Korea, China, Taiwan |
| `"South Asia"` | Nepal, Sri Lanka, Maldives, Bhutan |
| `"Middle East"` | UAE, Qatar, Oman, Jordan |
| `"Central Asia"` | Kazakhstan, Uzbekistan, Kyrgyzstan |
| `"Caucasus"` | Georgia, Armenia, Azerbaijan |
| `"Europe"` | Turkey, Greece, Italy, France, etc. |
| `"Africa"` | Morocco, Kenya, Tanzania, etc. |
| `"Americas"` | USA, Mexico, Peru, Brazil, etc. |
| `"Oceania"` | Australia, New Zealand, Fiji, etc. |

### International JSON Schema

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
  "homeCardSummary": "2–3 sentences for the home card.",
  "heroTagsHtml": "<span class='hero-tag'>✈️ Direct ~5h</span>",
  "heroNoticeHtml": "⭐ <strong>Key point.</strong> Why visit.",
  "overviewHtml": "...HTML...",
  "d1Html": "...HTML...",
  "d2Html": "...HTML...",
  "d3Html": "...HTML...",
  "d4Html": "...HTML...",
  "flightsHtml": "...HTML...",
  "hotelsHtml": "...HTML...",
  "budgetHtml": "...HTML..."
}
```

### International Field Rules

| Field | Type | Notes |
|-------|------|-------|
| `id` | string | Short lowercase, e.g. `"sg"`, `"jp"`. Unique. No spaces. |
| `name` | string | Display name. Use `·` for sub-destinations: `"Indonesia · Bali"` |
| `flag` | string | Emoji flag |
| `accentColor` | string | Hex color for nav/card/tab highlight |
| `heroGradient` | string | CSS gradient for hero background |
| `kidScore` | integer | 1–5 |
| `kidScoreDisplay` | string | Stars, e.g. `"⭐⭐⭐½"` |
| `priceTier` | string | Exactly `"S"`, `"A"`, `"B"`, `"C"`, or `"F"` |
| `continent` | string | Must match standard list exactly |
| `flightTime` | string | e.g. `"~5h direct"`, `"~8h via BKK"` |
| `directFlight` | boolean | `true` if non-stop from HYD |
| `visa` | string | e.g. `"Visa-free ✅"`, `"e-Visa $25"` |
| `budgetRange` | string | e.g. `"₹90K–1.4L"` |
| `rank` | integer | Position in home grid. Next available: **18** |
| `isWarning` | boolean | `true` = amber hero box, `false` = green hero box |

---

## PART 2 — INDIA DOMESTIC (india.json)

### Standard Region Names

Always use **exactly** one of these strings in the `"region"` field:

| String | States |
|--------|--------|
| `"North India"` | Ladakh, Kashmir, Himachal Pradesh, Uttarakhand, Rajasthan |
| `"Northeast India"` | Meghalaya, Nagaland, Arunachal Pradesh, Assam, Sikkim |
| `"South India"` | Karnataka, Kerala, Tamil Nadu, Andhra Pradesh, Telangana |
| `"West India"` | Goa, Maharashtra, Gujarat |
| `"Central India"` | Madhya Pradesh, Chhattisgarh |
| `"East India"` | Odisha, West Bengal, Jharkhand |

### India Domestic JSON Schema

```json
{
  "id": "gokarna",
  "name": "Gokarna",
  "region": "South India",
  "subtitle": "Gokarna, Karnataka",
  "flag": "🌊",
  "accentColor": "#1a6a8a",
  "heroGradient": "linear-gradient(160deg,#0a2a3a 0%,#0a1a1a 55%,#001a3a 100%)",
  "kidScore": 4,
  "kidScoreDisplay": "⭐⭐⭐⭐",
  "priceTier": "A",
  "flightTime": "~1.5h to GOA + 2h drive",
  "directFlight": true,
  "flightRoute": "HYD → GOX/GOI (Goa) → 2h drive",
  "airlines": "IndiGo / Air India / Akasa",
  "flightPrice": "₹3,500–8,000/adult",
  "flightTotal": "₹10,500–24,000 (3 pax)",
  "budgetRange": "₹54K–79K",
  "rank": 1,
  "isWarning": false,
  "minDaysRecommended": 4,
  "bestMonths": "November–March",
  "homeCardSummary": "2–3 sentences for the home card.",
  "heroTagsHtml": "<span class='hero-tag'>✈️ HYD→GOA direct ~1.5h</span>",
  "heroNoticeHtml": "⭐ <strong>Key point.</strong> Why visit.",
  "overviewHtml": "...HTML...",
  "d1Html": "...HTML...",
  "d2Html": "...HTML...",
  "d3Html": "...HTML...",
  "d4Html": "...HTML...",
  "travelHtml": "...HTML...",
  "hotelsHtml": "...HTML...",
  "budgetHtml": "...HTML..."
}
```

### India vs International — Key Differences

| Field | International | India Domestic |
|-------|--------------|----------------|
| `continent` | ✅ Required | ❌ Not used |
| `region` | ❌ Not used | ✅ Required |
| `subtitle` | ❌ Not used | ✅ Required — e.g. `"Gokarna, Karnataka"` |
| `visa` | ✅ Required | ❌ Not used |
| `flightsHtml` | ✅ Required | ❌ Not used |
| `travelHtml` | ❌ Not used | ✅ Required — replaces flightsHtml |
| `flightRoute` | ❌ Not used | ✅ Required — e.g. `"HYD → GOX → 2h drive"` |
| `airlines` | ❌ Not used | ✅ Required |
| `flightPrice` | ❌ Not used | ✅ Required — per adult return |
| `flightTotal` | ❌ Not used | ✅ Required — for 3 pax |
| `minDaysRecommended` | ❌ Not used | ✅ Required — if > 4, amber warning shows on hero |
| `bestMonths` | ❌ Not used | ✅ Required — shown on home card and hero |

### Special India Notes

**`minDaysRecommended`** — set to `4` if 4 days is fine. If set to `5` or `6` (e.g. Ladakh), an amber banner automatically appears on the hero: "⚠️ Minimum X days recommended."

**`bestMonths`** — use `·` to add festival info: `"October–May · Hornbill Festival Dec 1–10"`

**`travelHtml`** — the Travel tab for domestic. Include: flight route diagram, price table per adult and 3 pax, airport transfer info, permit warnings if applicable (ILP for Arunachal, Nagaland etc).

**`region`** → In tier lists, India destinations appear under `"🇮🇳 " + region` so they group separately from international continents.

---

## Price Tier Reference

| Tier | Meaning | Typical 4-day budget (family of 3) |
|------|---------|-------------------------------------|
| `"S"` | Shockingly Cheap | Under ₹60K |
| `"A"` | Affordable | ₹60K–₹1L |
| `"B"` | Moderate | ₹1L–₹1.5L |
| `"C"` | Expensive | ₹1.5L–₹2.5L |
| `"F"` | Overpriced | ₹2.5L+ |

---

## Kid Score Reference (for a 6-year-old girl)

| Score | Meaning |
|-------|---------|
| `5` | World-class (theme parks, zoos, snow play, dedicated kid infrastructure) |
| `4` | Excellent (great activities, very manageable for a child) |
| `3` | Good (decent options, some adult-focused moments) |
| `2` | Limited (beautiful but few kid-specific activities) |
| `1` | Adults only |

---

## HTML Content Rules

- Use `'single quotes'` for all HTML attributes inside JSON strings
- Available CSS classes: `.card`, `.day-card`, `.hotel-card`, `.notice`, `.notice-info`, `.notice-warn`, `.notice-green`, `.notice-red`, `.section-header`, `.section-icon`, `.section-title`, `.activity-table`, `.compare-table`, `.budget-table`, `.cost-badge`, `.cost-total`, `.hotel-rank`, `.hotel-name`, `.hotel-stars`, `.hotel-meta`, `.hotel-meta-item`, `.hotel-bullet`, `.gen-bullet`, `.hotel-grid`, `.hotel-stat`, `.hotel-stat-label`, `.hotel-stat-value`, `.recbadge`, `.gen-rec`, `.gold-rank`, `.silver-rank`, `.bronze-rank`, `.flight-route`, `.flight-city`, `.flight-arrow`, `.flight-stop`

---

## Destinations Already in the Planner

### 🌏 International (countries.json) — next rank: 18

| ID | Country | Continent | Tier | Kids | Rank |
|----|---------|-----------|------|------|------|
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

### 🇮🇳 India Domestic (india.json) — next rank: 10

| ID | Destination | Region | Tier | Kids | Rank |
|----|------------|--------|------|------|------|
| gokarna | Gokarna | South India | A | 4 | 1 |
| nagaland | Nagaland | Northeast India | A | 3 | 2 |
| kashmir | Kashmir | North India | B | 4 | 3 |
| ladakh | Ladakh | North India | B | 3 | 4 |
| mussoorie | Mussoorie | North India | A | 4 | 5 |
| meghalaya | Meghalaya | Northeast India | A | 4 | 6 |
| himachal | Himachal Pradesh (Manali) | North India | B | 4 | 7 |
| ziro | Ziro Valley | Northeast India | A | 3 | 8 |
| andaman | Andaman Islands | East India | B | 5 | 9 |

---

## Example Prompts

**Adding international:**
> "Add South Korea to countries.json. Family of 3 departing Hyderabad, Christian, 4-day trip. LEGOLAND Korea, N Seoul Tower, Han River cruise, Bukchon Hanok Village. Via Singapore. Visa-free for Indians. Use rank 18."

**Adding India domestic:**
> "Add Kashmir to india.json. Family of 3 departing Hyderabad, Christian, 4-day trip. Dal Lake shikara, Gulmarg gondola (snow in June!), Pahalgam horse safari, houseboat stay. Direct IndiGo HYD→SXR ~2.5h. Flight ₹7,000–12,000/adult return. Best months April–October. minDaysRecommended: 4. No ILP required for Srinagar. Kid score 4, Price tier B. Region: North India. Use rank 3."
