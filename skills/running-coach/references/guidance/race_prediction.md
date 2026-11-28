# Predicting race times from a runner's own races

Rendered from the coaching knowledge (version a596fb349f63); never edited by hand.

## Rules

### race-prediction-ranges

**Guidance:** Give a race time only as the range analytics.race_prediction publishes, with the odds of the goal time from its quantiles, never a single time. Say in words that the range should be wider for a marathon without a race of 25 km or more, a hilly course or warm weather, and say what it assumes.

**Purpose:** Race-time predictions miss by more than a single number suggests, most of all for the marathon, so a calibrated range keeps pacing and goal decisions honest.

**Uncertainty:** The marathon shift and its spread come from one survey cohort, and the athlete's own backtest rests on few races at first; the published range leans on the prior until about four races have been predicted.

**Alternatives:**

- Without a published range (no confirmed race in three years), set training paces from critical speed and ask about the race candidates instead of estimating a time.

**Claims:** pred-riegel-fast-for-marathon, pred-personal-exponent, pred-big-data-in-sample-not-width, pred-no-single-marathon-equation.

## Claims

Each with its evidence type, quality, source and link, then what it means in practice.

- **pred-big-data-in-sample-not-width** (observational, low quality; Emig 2020, https://pubmed.ncbi.nlm.nih.gov/33024098/): A fit to the races it was made from says little about how wide a prediction should be: judge a range by how well the method predicted races it had not seen, and keep a marathon projected from shorter races wide.
- **pred-no-single-marathon-equation** (systematic_review, low quality; Keogh 2019, https://pubmed.ncbi.nlm.nih.gov/31575820/): Give a marathon prediction as a range, say which course and weather it assumes, and never present one equation's number as the answer.
- **pred-pacing-10k-fast-start-individual** (rct, low quality; do Carmo 2016, https://pubmed.ncbi.nlm.nih.gov/26641740/): For a 10 km, a modestly fast first km is not reliably costly or helpful: the average effect was nil and the response split runners about in half. The coach should not prescribe a fast start, and can keep the opening km close to target pace. It does not identify in advance who tolerates a fast start, and says nothing about the half or full marathon.
- **pred-pacing-early-pace-above-94-cs** (observational, low quality; Smyth 2020, https://pubmed.ncbi.nlm.nih.gov/32472926/): A start-line check can compare the planned early marathon pace with the runner's critical speed: an early pace above about 94% of it marks a higher risk of a severe late slowdown. It is a risk marker from observational data, not a proven target; it does not show that holding back below 94% makes a given runner faster, and most runners who crossed it did not collapse.
- **pred-pacing-hitting-the-wall-share-and-cost** (observational, low quality; Smyth 2021, https://pubmed.ncbi.nlm.nih.gov/34010308/): Severe late slowing is common in recreational marathoners, more so in men and when chasing a personal best, and it costs a lot of time when it happens. That is a reason to plan the marathon cautiously and evenly. It does not show what caused the slowdowns (pacing, fuelling, heat or fitness), nor that an even or negative plan prevents them.
- **pred-pacing-marathons-mostly-positive-split** (systematic_review, low quality; Sha 2024, https://pubmed.ncbi.nlm.nih.gov/39281580/): Slowing in the second half is the norm in road marathons, and almost no field of runners shows a negative split. The review is descriptive; it does not show that a negative split is faster than an even one for amateurs, so it supports avoiding a fast start rather than prescribing a negative split.
- **pred-pacing-no-imposed-strategy-beats-self-pacing** (meta_analysis, low quality; Ramos-Campo 2026, https://pubmed.ncbi.nlm.nih.gov/41313565/): There is no trial evidence that prescribing a negative split, an even split or a fast start improves a time over the runner pacing themselves; the clearest signal is that starting slow for too long costs time. A coach can offer even effort as a sensible default, but should not present a negative split as proven faster. The studies are short laboratory time trials, not road marathons.
- **pred-pacing-realistic-target-time** (observational, very_low quality; Keogh 2020, https://pubmed.ncbi.nlm.nih.gov/32922647/): Setting the race target from the runner's actual training and recent races, rather than a hoped-for time, is associated with a better marathon, alongside steadier pacing. The coach can flag a target well ahead of the prediction. This is a single-race cross-sectional association; it does not show that lowering an ambitious target causes a faster time.
- **pred-personal-exponent** (observational, low quality; Blythe 2016, https://pubmed.ncbi.nlm.nih.gov/27336162/): Fit how a runner's speed fades with distance from their own races when they have raced several distances; with one race, or races at one distance, fall back on the population exponent.
- **pred-riegel-fast-for-marathon** (observational, low quality; Vickers 2016, https://pubmed.ncbi.nlm.nih.gov/27570626/): Treat a marathon time projected from shorter races as optimistic: without a race of 25 km or more, expect it several percent slower and give a wide range. Models using one or two prior races and weekly mileage beat Riegel here.
