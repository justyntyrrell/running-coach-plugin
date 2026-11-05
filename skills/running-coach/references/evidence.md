# Grounding advice in the evidence

A meaningful recommendation is a workout change, a taper or build decision, or a load warning. It rests on `coach_context.json`'s `coaching_guidance`.

## The rules that apply today

- **What `active` holds:** the reviewed rules that apply today. Each comes by `id` and `domain`, with:
  - `why_now`: the state values that triggered it;
  - `purpose`;
  - its claims, with their evidence type, quality, effect and population;
  - `personal_evidence`;
  - `uncertainty`.
- **The rule's own text:** its guidance and alternatives are in `references/guidance.md`, by id, and the domain's file there. Base the advice on that text, adapt it to the athlete, and offer an alternative where it fits better.
- **Undetermined rules** couldn't be checked, so never assume they wouldn't apply:
  - `reason: missing_input`: data was missing, and `missing` names the inputs;
  - `rule_error`: the rule itself failed. That's a fault to report, not a finding about the athlete.

## Personal evidence

`personal_evidence` is kind `personal`: the athlete's own history, N=1, descriptive and not causal. It is never a claim. Its `source` says where it was computed:

- **`taper-shape` and `taper-plan`:** their confirmed races, each residual beside its taper (`analytics.race_history`). Discuss it race by race.
- **`heat-response`:** their own heart-rate cost of heat (`analytics.heat`), and the race day's weather as the prediction priced it. Quote it as theirs only when its `verdict` is `supported`.
- **The weekly jump:** `pain_after_volume_jump`.
- **Hard days and recovery deviations:** `hrv_after_hard_day`. Both come from `athlete_model.learned_hypotheses`.

Read its `note`. With `available: false`, `reason` says why there is none yet, and a hypothesis's `learning_status` says what sample it still needs.

**How much it counts:** it may change your confidence, or the alternative you prefer. It never overturns a claim, the pain rule (rule 3) or the athlete's report.

## Patterns from the athlete's records

- **What they are:**
  - `athlete_model.learned_hypotheses` are patterns the Sync computed from the athlete's records (`source: computed`), each with its evidence, sample size and confidence, plus any set at setup;
  - `athlete_model.learning_status` says which still lack data;
  - `athlete_model.block_outcomes` sets each completed week, and further back each four-week block, beside its load, check-ins and plan decision.
- **How to cite them:** as the athlete's own history. That means N=1, descriptive and confounded, never above moderate confidence, and never as facts.
- **What they can't do:**
  - A pattern may change your confidence or the alternative you prefer. It never changes a claim, the pain rule or the athlete's report.
  - Keep reported facts apart from hypotheses, and never turn a correlation into a fact.
  - You never write a hypothesis. A pattern you suspect is a follow-up to check (`references/memory.md`).

## Counter-evidence and conflicts

- An evidence item with `role: counter` is evidence against the rule's trigger, shown so that you weigh it.
- `strongest_evidence` grades only the claims the rule rests on.
- A claim's `conflicts` are the claims that disagree with it. Weigh them, and name them when they bear on the advice.

## Population

- **What each evidence item carries:** its claim's `population` (caliber on McKay 2022's six tiers, whether the subjects were runners, sex, age group) and its `match` to the athlete: `same`, `adjacent`, `distant` or `unknown`.
- **The athlete's level:** `athlete_population` gives it, as their own volume and performance place it. Its thresholds are design inference.
  - **`sex`** is the athlete's own answer when they gave female or male. Otherwise it's `unknown`, and the level spans the men's and women's lines.
  - **`age_group`** comes from the birth year they gave, from an age worked out from the year alone, so it can be a year high. It's `unknown` without a birth year.
  - **From 40 the level is age-graded** (`basis.performance.age_graded`): their 10K-equivalent times the WMA/USATF 2025 road 10 km factor. Say so when it matters.
- **Ordering:** evidence is ordered by quality, then match, and nothing is left out. A mismatch never cancels a rule or changes its quality.
- **A distant population:** when `population_match.strongest_support` is `distant`, say in a few words that the advice rests on a different population, and which way that likely cuts. Never say by how much.
  - Effects measured in less-trained people are usually smaller in trained runners.
  - Elite practice assumes more volume and recovery than an amateur has.
  - Findings from another sport, or from one sex only, may not transfer in size.
  - Measurement and mechanism claims transfer better than training-response or injury-risk ones.

  Call that direction your inference, unless a claim or its applicability states it.
- **An unknown match:** mention it only if the advice turns on it.

## A rule for women

A rule whose `why_now` holds `reported_sex` applies because the athlete told you she is female. It may prompt one question: about her periods, hormonal contraception, an iron test, eating, or a past bone injury.

- **When to ask:** only when the question bears on today's advice, or when she reports something related (unusual fatigue or a plateau, a bony pain, a change in her periods or weight).
- **How:** at most one such question a chat, plainly, with one sentence on why.
- **If she declines:** never press. Never infer any of these, or a pregnancy, from her training.
- **What to keep:** nothing of what she answers, unless she asks you to keep it.

## Citing a claim

- **To yourself:** cite claim ids.
- **To the athlete:** give a claim's source, evidence type and quality, for example "Bosquet 2007, meta-analysis, moderate quality".
- **The link and what it means in practice** are in the domain's file in `references/guidance.md`. Give the link when the athlete asks.
- **The plan outline's defaults:** a `why` of `default:<key>` names one, with its value and basis in `references/plan-defaults.md`.
