# The Marketing Attribution Bible — Code Companion

Working Python code for the technical chapters of *The Marketing Attribution Bible*.

Every script runs standalone, generates its own synthetic data, and recovers a **known ground truth** — so you can check that an estimator actually works before you trust it on data where you will never find out.

No API keys, no credentials, no proprietary data. Clone it and run it.

---

## Quick start

```bash
git clone https://github.com/fgraysmith-16/attribution-bible-code.git
cd attribution-bible-code
pip install -r requirements.txt

python ch12-experiments/01_power_and_mde.py
```

Python 3.10 or later.

---

## What's here

### `ch12-experiments/` — Evaluating a controlled experiment

| Script | What it covers |
|---|---|
| `01_power_and_mde.py` | Minimum detectable effect; the detectable-vs-plausible comparison that decides whether a test is worth running |
| `02_difference_in_differences.py` | DiD by hand, by regression with fixed effects, cluster-robust standard errors, and randomisation inference |
| `03_synthetic_control.py` | Weighted donor pools, why you aggregate treated markets, pre-period fit diagnostics, placebo inference |
| `04_cuped.py` | Variance reduction from pre-period data — the precision of a 1.25x larger experiment, free |
| `05_peeking_problem.py` | Why "stop when significant" quadruples your false positive rate, and two corrections that fix it |

### `ch13-mta/`, `ch14-mmm/`, `ch15-identity-resolution/`

Placeholders. Code lands as each chapter publishes.

### `shared/synthetic_data.py`

Data generators used across chapters. Each returns `(dataframe, truth_dict)` where `truth_dict` contains the real parameter values.

The generators are deliberately realistic in the ways that matter for the methods being demonstrated:

- **AR(1) noise within each market.** Real weekly sales are autocorrelated, which is exactly why standard errors must be clustered. Independent noise would make clustering look unnecessary.
- **Latent common factors with market-specific loadings.** This is what makes some markets genuinely resemble others, which is what synthetic control exploits. Set `n_factors=0` and watch synthetic control stop working.
- **Seasonal ramp in the post period.** So the naive pre/post comparison is actively misleading, not merely imprecise.
- **Zero-inflated, right-skewed revenue.** Real revenue is not normally distributed, and some estimators behave differently when it isn't.

---

## A note on the numbers

Results are printed with the true value alongside the estimate, so you can see how close each method gets.

They do not match exactly, and that's the point. These estimators are unbiased, not psychic. A single run lands a couple of points either side of the truth, and the confidence intervals are there to tell you how far. If you want to see this directly, change the `seed` argument and run again.

Where a script's commentary quotes a specific number from its own output, that number comes from the default seed.

---

## Chapters

| # | Chapter | Code |
|---|---|---|
| 12 | Evaluating a Controlled Experiment | `ch12-experiments/` |
| 13 | Implementing a Multi-Touch Attribution Model | `ch13-mta/` |
| 14 | Implementing an MMM | `ch14-mmm/` |
| 15 | Implementing Identity Resolution | `ch15-identity-resolution/` |

The full series is on [LinkedIn](https://www.linkedin.com/in/frasergraysmith/).

---

## Licence

MIT. Use it, adapt it, ship it. Attribution appreciated but not required.
