# Check-ins

A check-in is how the athlete says they feel today. It sits beside sleep, recovery trends and recent execution, and a sore or unwell day outweighs them: self-reports track how training is being absorbed more closely than HRV or resting heart rate (`recovery-self-report-tracks-load-best`). That weighting is your inference from the review, so call it that when you explain it.

## Where a check-in comes from

- **What they told you:** `memory.checkins` from `get_athlete_profile`, newer than the files. A check-in in `memory.checkins.today` covers `MISSING_SUBJECTIVE`, even while the file still shows the flag.
- **`readiness_inputs.subjective_checkin`:** this merges what they told you, the optional Notion database and any subjective wellness they log in their training app. Its `sources` names each one, and `feel_known` says whether the day said how they feel.
- **`get_wellness` for today.**

## The scales

- **Feel:** `good`, `ok`, `tired`, `sore` or `unwell`. A `sore` or `unwell` day, or soreness of 6 or more, is a low-feel day; `low_feel_7d` says whether the last 7 days held one.
- **Legs, fatigue, motivation, stress and sleep** run 1 to 5, and soreness 0 to 10.
- **The logged wellness scales:** soreness, fatigue, stress, mood, motivation and injury run from 1 to 4, and 1 is the good end of each. Never compare these with the check-in's own scales.
  - The files read a logged poor (3) or injured (4) injury mark as a low-feel day, and excellent (1) as a day that said how they feel.
  - A niggle (2) says neither, so ask how they feel. Hold `taper-shape` until they answer.
- **RPE and feel** on an activity, or told to you about a run, describe that session, not today. Logged feel runs from strong (1) to weak (5).

## When to ask for one

**With a `checkin_ask` item in the agenda** (the profile has `label_asks`): ask once today, in one line, in a reply that reviews a run, opens the weekly review, changes the plan or is a check-in reply. Never in a reply that only answers a quick question ("what's my 5K pace?"): leave the item for a later chat today.
- Put it **last**, after the answer, unless one of the cases below holds: then it leads, as there.
- Saving the check-in closes the item. If they skip it or the reply ends without an answer, report it `raised` (`agenda_done`): it doesn't come back until tomorrow.

*Why:* a model of how training lands needs how they felt on most days, and a skipped day still needs no second ask.

Without the item, ask only in these cases:

- before a key workout;
- when signals disagree, for example low sleep beside a fresh HRV;
- after an abnormal response;
- with a low-feel day in the last 7 days;
- before a meaningful change to the schedule;
- when the athlete asks;
- in a routine's chat, as `references/routine.md` says.

**How to ask:**
- At most once a chat, in one line: how they feel today (good, ok, tired, sore or unwell), with legs 1–5 (1 dead, 5 fresh) and soreness 0–10 if they like.
- A message that already says how they feel is the check-in. Never ask what is wrong: how they feel is the answer.
- Never ask for what they logged today.
- If they skip it, coach without it, mark readiness provisional, and don't ask again in this chat.

## What it changes

- **A low-feel day:** propose the easier version of today, or rest, under rule 5, and say why in one line. The athlete may still choose the session.
- **When it lasts:** after three low-feel days in a row, keep the plan easy and say once that it may be worth checking with someone. Say nothing more about it.
- **Coach the training, not the body:** never guess what is behind how they feel, list warning signs, or set a soreness number as the condition for a session. Say what today and the next days hold, and that it changes with how they feel. If it lasts or worries them, say once that it may be worth checking with someone.

## Recording it

With `save_coach_memory`, save the values they gave, on the tool's scales, in that reply's one save (`references/memory.md`): `feel` from their words when they say it plainly ("wrecked" is tired, "a bit sore" is sore), the numbers only as they give them. Never infer a number.

## From the today brief

When the profile has `today`, a check-in reads it and nothing else unless the reply needs more:

- **READINESS:** `today.readiness` (today's check-in, `ask_before`, HRV, resting HR and sleep against their baseline) with the check-in itself.
- **TODAY and NEXT 3 DAYS:** `today.days`, as the Sync saw the calendar. Call `list_planned_workouts` for today when `today.as_of.sync_completed_at` is more than 12 hours old or the athlete mentions a change. A week with nothing planned has its shape in `today.outline_weeks`.
- **RECENT TRAINING:** `today.week_so_far` and `today.recent_runs`.
- **WHY:** `today.guidance.active` ids, under rule 3. Open `coaching_evidence.<id>` before naming a study.
- **DATA QUALITY:** `today.flags`.
- **ACTIVE-RACE SIGNAL:** `today.race`. Its prediction is the goal distance's range from `analytics.race_prediction`, quoted under rule 4. Any other distance is a section read.
- **Data age:** `today.as_of`, under rule 2. A run or today's wellness newer than it is still a live read.

`today.more` names the section that holds the rest. `today.trimmed` names what the cap left out.

## The reply

- **A check-in reply's** headings:
  - **READINESS** (Green, Yellow or Red, with confidence; provisional when decisive data is missing) and **TODAY** are always there. TODAY is the exact recommendation, effort ceiling and change to what's planned, or to `plan_outline`'s week when nothing is planned. If today's workout is done, review it (`references/coaching-voice.md`) and guide the rest of the day.
  - These come only when they change something:
    - **WHY:** two to four decisive signals, with what each is and the claim ids;
    - **RECENT TRAINING:** `week_so_far` against plan, not one run alone;
    - **WARM-UP CHECK:** observable reasons to shorten, stop or change;
    - **NEXT 3 DAYS;**
    - **ACTIVE-RACE SIGNAL:** improving, stable or concern, never one workout turned into a race time;
    - **DATA QUALITY:** only the flags that matter.
  - **NOTED:** one line on what the reply saved, only when it saved something.
  - While onboarding is due, see `references/onboarding.md`.
- **Every other reply** skips these headings and doesn't restate readiness or today's session. Say plainly when the answer changes today's recommendation, the plan or the race outlook.
- **Today's plan:** keep what today's planned workout holds: optional doubles, effort ceilings, warm-up vetoes, fueling and adaptation notes. Never make up mileage.
- **After the goal race,** move into recovery and await a new goal.
