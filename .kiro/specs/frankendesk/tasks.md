# FrankenDesk — Tasks

## Task List

### T-1: Scaffold index.html
- Create `index.html` with DOCTYPE, `<head>` (charset, viewport, title), empty `<body>`.
- Add a `<header>` with the FrankenDesk title and tagline.
- Add three `<section class="organ organ-N">` placeholders and two `.seam` dividers between them.
- Add inline `<style>` and `<script>` tags.
- **Done when:** File opens in a browser and shows the dark-bg header.

### T-2: Global CSS
- Body: `#0a0a0a` background, `#c8c8c8` text, monospace font, centered 900px max-width.
- `.seam` divider with dashed green border and decorative `✦ ✦ ✦` label.
- Organ section padding and minimum sizing.
- **Done when:** Seam dividers render correctly between three blank organ sections.

### T-3: Organ 1 — Candles HTML & CSS
- Organ-1 heading, stats bar (score + streak), canvas (600×220), Up/Down buttons, game-over overlay.
- Retro terminal style: `#0d0d0d` bg, green borders, monospace.
- **Done when:** Canvas and buttons render in correct style.

### T-4: Organ 1 — Candles JavaScript
- Implement mulberry32 PRNG.
- Implement random-walk candle generator.
- Implement `drawCandle()` on canvas with auto-scaling.
- Implement game loop: 1-second timer, prediction gating, scoring, streak.
- Implement game-over and Play Again.
- **Done when:** Game plays fully, scores correctly, restarts cleanly.

### T-5: Organ 2 — Vault HTML & CSS
- Organ-2 heading with MOCK badge, gig creation form, gig list container.
- Paper-form style: serif font, off-white cards, yellow-toned borders.
- **Done when:** Form and empty card list render correctly.

### T-6: Organ 2 — Vault JavaScript
- `createGig()`: builds card, appends creation log entry, renders.
- `advanceState()`: Funded→Delivered→Released with log entries.
- `renderGig()`: updates card DOM (state badge, button, log).
- Form submit handler with validation.
- **Done when:** Creating a gig and cycling through all three states works, log updates correctly.

### T-7: Organ 3 — Eye HTML & CSS
- Organ-3 heading, textarea, Check button, results panel.
- Surveillance style: sans-serif, cold blue-grey, purple evidence highlights.
- **Done when:** Textarea and results area render in correct style.

### T-8: Organ 3 — Eye JavaScript
- `scan()`: case-insensitive phrase matching, score calculation, verdict logic.
- `renderResult()`: show verdict badge (color-coded), score bar, evidence list.
- Empty-input validation.
- **Done when:** Scan correctly identifies red-flag phrases and shows the right verdict.

### T-9: README.md
- Project overview, description of each organ, how-to-run instructions.
- **Done when:** File is present and accurate.

### T-10: LICENSE
- MIT License, copyright Indra Dwi Junianto, current year.
- **Done when:** File is present with correct name and content.

### T-11: Integration check
- Open `index.html` in a browser (or `cat` and inspect) to verify no syntax errors.
- Confirm all three organs are present and seams render.
- **Done when:** No JS errors, all organs functional.
