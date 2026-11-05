# Check-ins

A check-in is the athlete's own report for a day. It sits beside sleep, recovery trends and recent execution, and pain or illness in it outweighs them (rule 3).

## Where a check-in comes from

- **What they told you:** `memory.checkins` from `get_athlete_profile`, newer than the files. A check-in in `memory.checkins.today` that answers pain covers `MISSING_SUBJECTIVE`, even while the file still shows the flag.
- **`readiness_inputs.subjective_checkin`:** this merges what they told you, the optional Notion database and the subjective wellness they log in Intervals. Its `sources` names each one.
- **`get_wellness` for today.**

## The scales

- **Intervals' own scales:** soreness, fatigue, stress, mood, motivation and injury run from 1 to 4, and 1 is the good end of each.
  - Soreness, fatigue and stress run from low (1) to extreme (4).
  - Mood and motivation run from excellent (1) to poor (4).
  - Injury runs from excellent (1), through niggle (2) and poor (3), to injured (4).

  Never compare these with the check-in's own scales.
- **An Intervals injury of 2 or more:** the files don't count it as pain yet, so ask about it. Hold `taper-shape` until the athlete answers.
- **RPE and feel** on an activity, or told to you about a run, describe that session, not today's readiness. Intervals' feel runs from strong (1) to weak (5).

## When to ask for one

Ask only in these cases:

- before a key workout;
- when signals disagree, for example low sleep beside a fresh HRV;
- after an abnormal response;
- with pain or illness in the last 7 days;
- before a meaningful change to the schedule;
- when the athlete asks.

**How to ask:**
- At most once a chat, in one line, with the scales spelled out: legs 1–5 (1 dead, 5 fresh), soreness 0–10, any pain 0–10 and where, sleep 1–5, and anything else.
- A message that already says how they feel is the check-in.
- Never ask for what they logged today.
- If they skip it, coach without it, mark readiness provisional, and don't ask again in this chat.

## Recording it

With `save_coach_memory`, save the values they gave, on the tool's scales, in that reply's one save (`references/memory.md`). Ask for a number rather than infer one.
