# 🧟 FrankenDesk

> Three organs. One monster. No warranty.

FrankenDesk is a single-page web app stitched together from three independent mini-apps called **organs**. Each organ has a deliberately different visual style — a retro trading terminal, a bureaucratic paper form, and a cold surveillance panel — separated by green dashed "stitched seam" dividers on a dark laboratory background.

---

## Organs

### Organ I — Candles

A 60-second candlestick calling game.

- A live candlestick chart draws one candle per second from a seeded random walk.
- Before each candle appears, call **▲ UP** or **▼ DOWN**.
- A correct call earns **100 points** plus a streak bonus (10 × streak level, capped at 80).
- An incorrect call resets your streak.
- After 60 candles the final score is shown and you can play again with a new seed.

### Organ II — Vault

A mock escrow desk. **No real money is involved** — this is a UI demonstration only.

- Post a gig with a title and an amount.
- Each gig card moves through three states: **Funded → Delivered → Released**.
- Every state change is recorded in a timestamped receipt log on the card.
- State lives in memory; refreshing the page resets everything.

### Organ III — Eye

A scam message screener.

- Paste any suspicious text into the textarea and click **🔍 Check**.
- The screener scans for red-flag phrases: *urgent transfer*, *gift card*, *seed phrase*, *guaranteed profit*, *double your money*, *off-platform payment*, *verify your wallet*.
- Matched phrases are listed as evidence.
- A risk score (0–100) drives a verdict of **CLEAR**, **CAUTION**, or **HIGH RISK**.

---

## How to Run

No build step, no server, no dependencies.

1. Clone or download this repository.
2. Open `index.html` in any modern browser:

   ```
   # macOS
   open index.html

   # Linux
   xdg-open index.html

   # Windows
   start index.html
   ```

   Or just drag `index.html` into a browser window.

That's it. Everything runs locally in the browser.

---

## Project Structure

```
frankendesk/
├── index.html          # The entire app: markup, styles, and scripts
├── README.md           # This file
├── LICENSE             # MIT
└── .kiro/
    └── specs/
        └── frankendesk/
            ├── requirements.md
            ├── design.md
            └── tasks.md
```

---

## License

MIT — see [LICENSE](LICENSE).
