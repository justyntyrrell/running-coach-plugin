# Predicting race times from a runner's own races

Rendered from the coaching knowledge (version acf61b6f40f3); never edited by hand.

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
- **pred-personal-exponent** (observational, low quality; Blythe 2016, https://pubmed.ncbi.nlm.nih.gov/27336162/): Fit how a runner's speed fades with distance from their own races when they have raced several distances; with one race, or races at one distance, fall back on the population exponent.
- **pred-riegel-fast-for-marathon** (observational, low quality; Vickers 2016, https://pubmed.ncbi.nlm.nih.gov/27570626/): Treat a marathon time projected from shorter races as optimistic: without a race of 25 km or more, expect it several percent slower and give a wide range. Models using one or two prior races and weekly mileage beat Riegel here.
