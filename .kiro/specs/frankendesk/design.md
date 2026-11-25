# FrankenDesk — Design

## File Structure

```
frankendesk/
├── index.html          # Everything: markup, inline <style>, inline <script>
├── README.md
├── LICENSE
└── .kiro/
    └── specs/
        └── frankendesk/
            ├── requirements.md
            ├── design.md
            └── tasks.md
```

All HTML, CSS, and JavaScript live in `index.html`. No separate asset files are needed.

---

## Page Layout

```
┌────────────────────────────────────────┐
│  🧟 FrankenDesk  — header              │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤  ← stitched seam divider
│  Organ 1 — Candles                     │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤  ← stitched seam divider
│  Organ 2 — Vault                       │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤  ← stitched seam divider
│  Organ 3 — Eye                         │
└────────────────────────────────────────┘
```

Each organ is wrapped in a `<section class="organ organ-N">` element. Seam dividers are `<div class="seam">` elements placed between sections.

---

## Global Visual Theme

| Token | Value |
|-------|-------|
| Body background | `#0a0a0a` |
| Body text | `#c8c8c8` |
| Accent (stitching green) | `#00ff88` |
| Danger red | `#ff4444` |
| Warning amber | `#ffaa00` |
| Font (body) | system monospace stack: `'Courier New', Courier, monospace` |
| Max content width | `900px`, centered |

### Stitched Seam Divider

```css
.seam {
  border: none;
  border-top: 3px dashed #00ff88;
  margin: 2rem 0;
  position: relative;
}
.seam::before {
  content: '✦ ✦ ✦';
  position: absolute;
  top: -0.75em;
  left: 50%;
  transform: translateX(-50%);
  background: #0a0a0a;
  padding: 0 1rem;
  color: #00ff88;
  font-size: 0.85rem;
  letter-spacing: 0.5em;
}
```

---

## Organ 1 — Candles: Visual Style

**Style identity:** Retro terminal / trading desk. Monospace font, green-on-black palette, pixel-sharp borders.

- Background: `#0d0d0d`
- Border: `2px solid #00ff88`
- Accent: `#00ff88` (bullish candle), `#ff4444` (bearish candle)
- Buttons: flat, border `1px solid #00ff88`, green text, black bg; hover inverts colors

### Canvas Layout (600 × 220 px)

The chart draws candles left-to-right. The viewport scrolls to show the latest ~20 candles. Each candle occupies a fixed slot width of `28px` (body `12px` wide, centered). Price is auto-scaled to fill the canvas height with 10px padding top and bottom.

### Candle Rendering

Each candle is defined by: `open`, `high`, `low`, `close` (all floats).

- Bullish (close ≥ open): body filled `#00ff88`
- Bearish (close < open): body filled `#ff4444`
- Wick: 1px line in the same color as the body, from low to high

### PRNG

Mulberry32 — a fast, seedable 32-bit PRNG:

```js
function mulberry32(seed) {
  return function() {
    seed |= 0; seed = seed + 0x6D2B79F5 | 0;
    let t = Math.imul(seed ^ seed >>> 15, 1 | seed);
    t = t + Math.imul(t ^ t >>> 7, 61 | t) ^ t;
    return ((t ^ t >>> 14) >>> 0) / 4294967296;
  };
}
```

### Random Walk

Starting price: 100. Each candle:
1. `open` = previous `close`
2. `close` = `open + (rand() - 0.5) * 10`  (range ±5)
3. `high` = `max(open, close) + rand() * 3`
4. `low`  = `min(open, close) - rand() * 3`

Seed for a new game: `Date.now() & 0xFFFFFFFF`.

### Scoring

```
bonus = min(streak * 10, 80)
points = 100 + bonus
```

---

## Organ 2 — Vault: Visual Style

**Style identity:** Bureaucratic paper form. Serif font, off-white card on dark background, rubber-stamp aesthetics.

- Organ background: `#111108`
- Card background: `#1a1a10`
- Card border: `1px solid #888840`
- Font: `Georgia, 'Times New Roman', serif`
- State badge colors:
  - Funded: background `#1a3a1a`, text `#00ff88`
  - Delivered: background `#1a2a3a`, text `#4488ff`
  - Released: background `#2a2a2a`, text `#aaaaaa`
- Buttons: solid fill matching state color, dark text

### Gig Card HTML Structure

```html
<article class="gig-card" data-id="...">
  <header>
    <span class="gig-title">…</span>
    <span class="gig-amount">$…</span>
    <span class="gig-state state-funded">FUNDED</span>
  </header>
  <div class="receipt-log"><pre>…</pre></div>
  <footer>
    <button class="btn-action">Mark Delivered</button>
  </footer>
</article>
```

---

## Organ 3 — Eye: Visual Style

**Style identity:** Surveillance / intelligence file. Sans-serif font, cold blue-grey tones, clinical layout.

- Organ background: `#080810`
- Border: `1px solid #334`
- Font: `'Arial', 'Helvetica Neue', sans-serif`
- Verdict colors:
  - CLEAR: `#00ff88`
  - CAUTION: `#ffaa00`
  - HIGH RISK: `#ff4444`
- Evidence list: monospace, `#cc88ff` (purple highlight for matched phrase)

### Scan Logic

```js
const RED_FLAGS = [
  'urgent transfer', 'gift card', 'seed phrase',
  'guaranteed profit', 'double your money',
  'off-platform payment', 'verify your wallet'
];

function scan(text) {
  const lower = text.toLowerCase();
  const hits = RED_FLAGS.filter(f => lower.includes(f));
  const score = Math.min(100, hits.length * 15);
  const verdict = score >= 60 ? 'HIGH RISK' : score >= 20 ? 'CAUTION' : 'CLEAR';
  return { hits, score, verdict };
}
```

---

## JavaScript Architecture

All JS is inline in a single `<script>` tag at the bottom of `<body>`. Three namespaced IIFE blocks keep organ logic separate:

```
Candles  — object with init(), newGame(), makePrediction(), drawCandle(), render()
Vault    — object with init(), createGig(), advanceState(), renderGig()
Eye      — object with init(), scan(), renderResult()
```

No global state leaks between organs. Event listeners are attached in each organ's `init()` call. All `init()` calls fire on `DOMContentLoaded`.
