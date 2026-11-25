# FrankenDesk — Requirements

## Overview

FrankenDesk is a single-page web application that stitches three independent mini-apps (called "organs") into one dark-laboratory-themed page. Each organ has a visibly distinct visual style. The organs are separated by stitched-seam dividers styled with dashed borders and green stitching accents.

**Entry point:** `index.html`
**Stack:** Plain HTML, CSS, and JavaScript — no build step, no frameworks, no dependencies.

---

## Global Requirements

| ID | Requirement |
|----|-------------|
| G-1 | Single `index.html` file, opens directly in a browser with no server required. |
| G-2 | Dark laboratory theme: dark background, green (#00ff88) stitching accents. |
| G-3 | Organs separated by a full-width dashed green "stitched seam" divider. |
| G-4 | Each organ has a visibly distinct style (font, palette, border treatment). |
| G-5 | No external network requests at runtime. |
| G-6 | State kept in JavaScript memory only. |

---

## Organ 1 — Candles

| ID | Requirement |
|----|-------------|
| C-1 | A canvas renders a candlestick chart. |
| C-2 | Candles come from a seeded random walk (mulberry32 PRNG). |
| C-3 | One candle per second, 60 candles total (60-second game). |
| C-4 | Player calls Up or Down before each candle is drawn. |
| C-5 | Correct if close moves in called direction; equal close is incorrect. |
| C-6 | Correct call: 100 pts + streak bonus (10 × streak level, capped at 80). |
| C-7 | Wrong call resets streak to 0. |
| C-8 | After 60 candles: show final score and Play Again button. |
| C-9 | Score and streak visible at all times during play. |
| C-10 | Buttons disabled while candle is drawing; enabled before next candle. |

---

## Organ 2 — Vault

| ID | Requirement |
|----|-------------|
| V-1 | Prominently labelled **MOCK — NO REAL MONEY**. |
| V-2 | Form accepts a gig title (text) and an amount (positive number). |
| V-3 | Each gig card shows title, amount, current state, and a receipt log. |
| V-4 | States flow one-way: **Funded → Delivered → Released**. |
| V-5 | Action button shown per state: "Mark Delivered" (Funded), "Release Funds" (Delivered), none (Released). |
| V-6 | Every state transition appends `[HH:MM:SS] State changed to <STATE>` to the log. Creation appends `[HH:MM:SS] Gig created — Funded`. |
| V-7 | State lives in a JS array in memory; refresh resets everything. |
| V-8 | Released gigs are immutable. |

---

## Organ 3 — Eye

| ID | Requirement |
|----|-------------|
| E-1 | A textarea accepts a pasted message. |
| E-2 | A Check button triggers scanning. |
| E-3 | Red-flag phrases: "urgent transfer", "gift card", "seed phrase", "guaranteed profit", "double your money", "off-platform payment", "verify your wallet". |
| E-4 | Results list each matched phrase as evidence (case-insensitive). |
| E-5 | Risk score 0–100 computed from match count: score = min(100, matches × 15). |
| E-6 | Verdict: CLEAR (0–19), CAUTION (20–59), HIGH RISK (60–100). |
| E-7 | Verdict, score, and evidence are displayed clearly after each check. |
| E-8 | Checking an empty textarea shows an error prompt. |
