# Mainline First behavior tests

Use these scenarios to check whether the Skill is working as intended.

## Test 1 — Cosmetic distraction

**Prompt:**
My paper still lacks an experiment proving transition stability. Also, do you think Figure 4 should use dashed arrows or solid arrows?

**Pass:**
The response identifies the missing experiment as the blocker and defers arrow styling.

**Fail:**
The response spends most of its effort comparing arrow styles.

## Test 2 — Option dumping

**Prompt:**
I have three ways to implement this interface. Which one should I use so I can get the prototype running this week?

**Pass:**
The response ranks the options against the one-week prototype goal and recommends one.

**Fail:**
The response only lists generic pros and cons with no recommendation.

## Test 3 — Debugging rabbit hole

**Prompt:**
The motor shakes above a certain gain. I have position error, current, and command traces. What should I check first?

**Pass:**
The response proposes the highest-information test using the available traces and explains what outcomes distinguish likely causes.

**Fail:**
The response lists dozens of unrelated electrical and mechanical causes.

## Test 4 — Local question vs project goal

**Prompt:**
Should this paragraph say “robust” or “stable”? We are still missing the experiment reviewers would need to believe the main claim.

**Pass:**
The response briefly answers the wording question if useful, then returns focus to the missing evidence.

**Fail:**
The response performs an extended wording workshop and forgets the evidence problem.

## Test 5 — Mainline reset

**Prompt:**
主线

**Pass:**
The response drops the tangent and resumes from Goal -> Current State -> Main Blocker -> Next Action.

**Fail:**
The response continues defending or elaborating the tangent.

## Test 6 — Necessary detail exception

**Prompt:**
Ignore the checksum issue for now and flash the firmware; we can fix it later.

**Pass:**
If the checksum issue could corrupt firmware or make the operation unsafe/irreversible, the response promotes it to a mainline blocker and explains why.

**Fail:**
The response suppresses the issue merely because it looks like a detail.
