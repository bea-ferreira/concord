# Concord

**Rater calibration & data quality console**: a single-page prototype showing how I'd audit a human-annotation batch, find what's wrong with it, fix it, and explain it to the customer.

The scenario: a fictional customer, Northwind AI, sent 240 model responses to be rated by 6 raters on a 4-dimension rubric (correctness, instruction following, helpfulness, tone). Concord computes reliability, flags problems with documented rules, recomputes the numbers after the fixes, and drafts a send-ready findings memo.

## Synthetic data

Everything is **synthetic demo data**, generated in the browser with a seeded PRNG (mulberry32, seed 42), so every load shows the same numbers. Three problems are planted on purpose and stated openly in the Methodology tab:

- **R4 drifts**: lenient by +0.9 from item 131 on.
- **R6 rushes**: about 9 s per item, scores that are mostly noise.
- **The `tone` guideline is ambiguous**: raters split into two camps on whose context counts.

The detection rules don't know about these settings. They only see the ratings.

## What's inside

- Krippendorff's alpha (interval, handles missing data), quadratic-weighted Cohen's kappa, leave-one-out consensus correlation, gold accuracy and MAE, rolling drift with change-point detection, and speed vs accuracy.
- `selfTest()` checks alpha against a hand-computed example and the published example in Krippendorff (2011). It runs on load and logs PASS/FAIL to the browser console; you can call it again from the console.
- Five views: Data health, Raters, Rubric, Customer summary (copy as text or print to one page), Methodology.

## Run it

Open `index.html` in any modern browser. There's no build step, no dependencies and no network calls: all CSS, JS and SVG charts are inline.

---

Prototype by Beatriz Ferreira. Independent work, not affiliated with any company.
