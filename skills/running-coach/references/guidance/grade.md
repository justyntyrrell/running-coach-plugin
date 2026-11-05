# Running on grades: uphill and downhill cost

Rendered from the coaching knowledge (version acf61b6f40f3); never edited by hand.

## Rules

### hilly-goal-course

**Guidance:** The goal course climbs more than 15 m per km. Climbs cost more time than descents give back, so a course like this is usually slower than flat. When the race prediction prices the goal, analytics.race_prediction.goal.adjustments_s.course says what its course adjustment adds; for a goal it does not price, no amount is published. Pace climbs by effort.

**Purpose:** Set expectations and pacing for a course that climbs.

**Uncertainty:** The pacing studies are small: 11 runners racing a treadmill course of +5% and -5% stages, and 8 runners in an outdoor time trial; neither tested a course that climbs much more or less than it descends. 15 m per km is the race prediction's line for a hilly race (HILLY_M_PER_KM, which it applies to the climb), a design choice and no evidence threshold; the climb is the gain the athlete gave, over the goal's distance, and none when they gave only a descent.

**Alternatives:**

- Below the line a course can still cost time: when the race prediction prices the goal, analytics.race_prediction.goal.adjustments_s.course says how much.

**Claims:** grade-hilly-course-slower-than-flat, grade-overground-downhill-underused, grade-minetti-cost-curve.

### downhill-goal-course

**Guidance:** The goal course descends more than 15 m per km. For long or steep descents, add progressive downhill running in the weeks before, the first session well clear of race week, and expect a few days of lost leg strength after it: a first bout of downhill running costs the legs more than later ones.

**Purpose:** Prepare the legs for the course's descents.

**Uncertainty:** The downhill-damage evidence comes mostly from people unused to descents on steep treadmill slopes, and the repeated-bout meta-analysis pooled multi-joint muscle-damaging exercise, not downhill running alone. 15 m per km is the race prediction's line for a hilly race (HILLY_M_PER_KM), applied here to the descent: a design choice and no evidence threshold. The descent is the loss the athlete gave, over the goal's distance, or the gain when they gave only a climb, as the race prediction reads a loop.

**Alternatives:**

- When the athlete already runs long descents in training, they may already have the protection a first bout gives: ask before adding sessions.

**Claims:** grade-downhill-muscle-damage-economy, grade-repeated-bout-protects.

## Claims

Each with its evidence type, quality, source and link, then what it means in practice.

- **grade-downhill-muscle-damage-economy** (narrative_review, low quality; Bontemps 2020, https://pubmed.ncbi.nlm.nih.gov/33037592/): Before a race with long or steep descents, add progressive downhill running in the preceding weeks. After a descent-heavy run, expect a few days of lost strength and economy and keep them easy.
- **grade-hilly-course-slower-than-flat** (observational, low quality; Staab 1992, https://pubmed.ncbi.nlm.nih.gov/1548986/): Expect a course with as much descent as climb to be slower than flat. Do not assume descents give back what climbs cost: a grade model that credits descents with their full metabolic saving will overstate how fast a hilly race can be run.
- **grade-minetti-cost-curve** (observational, low quality; Minetti 2002, https://pubmed.ncbi.nlm.nih.gov/12183501/): Use this curve as the default shape for grade-adjusted pace on climbs and moderate descents at a steady effort. Read its downhill side as a metabolic saving, not as the speed a runner can gain on a descent, which is smaller in races.
- **grade-overground-downhill-underused** (observational, low quality; Townshend 2010, https://pubmed.ncbi.nlm.nih.gov/20010117/): On hilly runs, judge climbs by effort and expect descents to be run well below flat effort. The authors suggest the most time can be gained on the level sections after hills: level speed took about 78 s to settle after an uphill but about 24 s after a downhill.
- **grade-repeated-bout-protects** (meta_analysis, low quality; Doma 2023, https://pubmed.ncbi.nlm.nih.gov/38015738/): One or two downhill sessions ahead of a descent-heavy race may blunt the damage it causes (the abstract does not say how long protection lasts). The first exposure is the costly one, so keep it well clear of the race.
