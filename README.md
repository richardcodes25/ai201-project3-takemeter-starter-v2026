# TakeMeter

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

Public posts from [r/patientgamers](https://www.reddit.com/r/patientgamers), a gaming subreddit for writing about games that are already out, not one release and not a launch thread. The text is long enough to collect 200 posts, and it is not one kind of writing: a finished review, a quit note, a question to the sub, and a Game of the Month pitch all show up in the same place. The classifier sorts each post into `system`, `verdict`, or `ask`. The four distinctions below are the reading those labels came from. A fourth label, `dropout`, looked obvious and did not hold; that is written under the decision rule.

### Candidate distinctions

From about thirty public submissions, plus the comment threads under the quit posts and the question posts. Not "good" and "bad." Each one is something a post either contains or does not.

1. **Some posts put a score on the page. Some never do.** `9/10`, `8.5/10 (Excellent)`, `7.75/10`, `Score: ★★★☆☆`, and a split like Bastion's `Rubric: 80 / Gut: 83 / Average: 81.5`. The Magical Drop VI post explains the orb rule, says "fun as hell," and recommends the game, with no score. The April 2026 Death Stranding Game of the Month post names the developer, the genre, and the platforms, and does not rate it. Question posts ("When do you decide to give up on a game?") have no score because they are not reviews.

2. **Some posts cite a countable amount of play. Some don't.** "After giving this game a proper shake for 20 hours," "Time Played: 17 Hours," "Completed in 5.8 hours over 2 days," "I racked up a total of 44 hours," "my playthrough took 115 hours," "4 hours deep." A one-line blurb can carry a score and still skip the time: "Grand Theft Auto IV (8.5/10): Great game, not much I can say really."

3. **Some posts explain a rule of the game. Some only report a feeling.** Spelldrifter: every action has a time cost instead of a mana cost, so a cheap buff can move you ahead of the enemy. Jusant: the triggers are your two hands. Fashion Police Squad: each weapon corrects one kind of outfit (a dye gun, a needle gun, a sock-removing "grenade"). Magical Drop VI: orbs clear when you place a match in front of a column of two or more. Set against those, "the biggest dud of the year," "fun as hell," and "Great game, not much I can say really."

4. **Some posts say the writer stopped. Some are written from the end. Some are not a play report.** "Abandoned," "Refunded, just couldn't get into it," "I'm just not prepared to spend another 130," "Nah, I'm out" once the skill tree was already done on the road to Sparta. Yearly roundups are mostly games they finished. Separate from both: a question to the sub, and the Game of the Month announcement, which pitches a game for the month instead of reporting a finished play.

The likely hard boundary, if these become labels, is (3). A post can carry a score and a playtime and still never say what the player does, and a post with no score can still explain the system.

Posts this came from include the March 2026 "Chronicles of a Prolific Gamer" (Spelldrifter, Jusant, Fashion Police Squad, Black Book), the January 2026 indie month-in-review, kirso's late 2025 review (including the Sifu refund), fanboy_killer's 2025 roundup, Cmoire's 19 games of 2025, the Magical Drop VI post, the Atlas Fallen review, both Cyberpunk 2077 posts (the category-score comeback writeup and the "where did the time go" 44-hour post), the AC Odyssey "20 hours and I'm moving on" post and its comments, the Supergiant Bastion / Transistor / Pyre post, the Death Stranding Game of the Month pitch, and the question threads on quitting, hours played, and going back to an abandoned game.

---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### `system`

**Definition:** The writer has settled on an account of a game, and the post spells out at least one checkable rule of play: an input, a cost, a lock, or a condition that decides whether an action succeeds.

**Example 1:**
> Magical Drop VI. "Magical Drop's gameplay revolves around grouping like colored orbs that are destroyed when you place one in front of a column that consists of two or more (those making contact horizontally are subsequently destroyed as well)." The post recommends the game and never scores it. The rule is the whole account.

**Example 2:**
> Cyberpunk 2077, "the worst 'where did the time go' game." They finished, they recommend it, and they score it 7.75/10. They also write the perk lock: "deeper tiers of the perk trees being locked if you do not have the appropriate amount of base attribute points. You can use the perk points in any attribute tree, but you will be limited very quickly in what perks are even accessible if you don't have enough attribute points spent."

### `verdict`

**Definition:** The writer has settled on a judgment, of a game or of a way of playing, and the post does not spell out a rule of play.

**Example 1:**
> "How I Began to Avoid the 'Hours Played' Meta Game." The settled line is "A good game is a good game whether it's five hours or 50 hours or 500 hours." Return of the Obra Dinn is the example: $15, about nine hours, premise and music and story. The post never says what makes a deduction in that game succeed.

**Example 2:**
> The January 2026 indie month-in-review. Yes, Your Grace is "a VERY good story" and "a little bit on rails," scored 7/10. Citizen Sleeper is "sad sci fi capitalism" scored 7.5/10. Terror at Oakheart is "clunky feeling combat" scored 7/10. None of those sentences say what an action costs or what makes it succeed. "Dice RPG" names a genre. It is not a rule.

### `ask`

**Definition:** The writer is still asking the sub what to do, or what the rule for quitting should be, and the post would not stand as a finished account if the question were removed.

**Example 1:**
> "When do you decide to give up on a game?" Bastion is the anecdote: a couple of hours, "the combat was unsatisfying," "environments and enemies all felt very same-y," then they packed it in. No input, cost, lock, or success condition. The post ends on "How do you decide when it's time to give up on a game?"

**Example 2:**
> "How many hours is long enough to decide either you drop a game or continue playing it?" They have five hours in an unnamed game, "I don't know if I should continue or not," and they close with "what are your thoughts about this?"

### The hardest boundary

**Which two labels:** `system` and `verdict`

**The post, with no label attached:**

> AC Odyssey, "Tried it for 20 hours but I'm moving on..." "This game feels very underwhelming and repetitive. After giving this game a proper shake for 20 hours recently (and this is my second attempt), I'm just not prepared to spend another 130 slogging through the rest of the content." Later: "Combat has no weight to it" and "Melee combat here is a bad souls-like." Also later: "Parkour mostly involves holding 'A' and letting the game figure out the rest." "Getting the drop on an enemy and stabbing them through the heart or cutting their throat means nothing if they're a higher level." "The game interrupts its own flow at times by making you build adrenaline and wait for the cooldowns on skills." Metacritic critics at 83%, Metacritic users at 6.9/10, and they agree with the user number.

The case for `verdict`: the title is the decision, the pros are production and taste, and "no weight," "shallow as a puddle," and the two Metacritic numbers are a judgment. The mechanic sentences are there to justify a score he has already reached.

The case for `system`: holding A, a stealth kill that fails a level check, and a skill that waits on adrenaline are not adjectives. A reader who has not played can say what the game does. The 6.9 is beside the point.

Both cases hold. The rule is what breaks the tie.

**The decision rule I used every time:** If the writer is still asking the sub what to do, the post is `ask`, even when the question includes a rule of play or a game they might quit. If they have settled, and the post spells out a checkable rule of play — an input, a cost, a lock, or a condition that decides whether an action succeeds — the post is `system`, even when the title is a score or a quit. Otherwise it is `verdict`. A genre list, an hour count, a score, and a feeling ("no weight," "spongey," "long combos") are not a rule.

Under that rule the Odyssey post is `system`. They have settled ("I'm moving on"), and the post spells out the A button, the level check on a stealth kill, and the adrenaline cooldown.

`dropout` was the label I tried and dropped. "I stopped" shows up inside all three of the labels that held: Odyssey explains the rules on the way out (`system`), the five-hour post is still asking (`ask`), and "Refunded, just couldn't get into it" is a settled feeling with no rule (`verdict`). The word "dropped" does not pick out one kind of post.



---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:** Public self-posts on r/patientgamers. Reddit's own listing was refusing logged-out requests, so the text came from the Arctic Shift public archive of those same posts. Each row is the title plus the full body. Nothing was trimmed, and the file is one unsplit `labels.csv`.

**How I labelled them:** There is no cold set. An assistant applied the definitions and the decision rule, then the batch was corrected: posts whose only "rule" was a complaint that hitboxes felt wrong were moved to `verdict`, and two posts that do state a rule (the Cyberpunk perk lock, and the crafting-cost roundup) were moved to `system`. Every row is marked `pre-labelled, checked`. Marking any of them `cold` would be false. `ask` is 14.5%, under the 18% floor in criterion 3. Across about 5,000 recent submissions, 29 posts were actually still asking the sub. Finished reviews were not relabelled as questions to fill the quota.

**Counts per label:**

| Label | Count | Share |
|---|---|---|
| `system` | 82 | 41.0% |
| `verdict` | 89 | 44.5% |
| `ask` | 29 | 14.5% |
| **Total** | 200 | 100% |

**Three hard cases**

**1.**
> *The post:* Skate 2, "what am I not getting?" The tricks fail with no reason given, and "the game expects me to keep repeating the same action until it randomly works."
>
> *Could have been:* `system` or `ask`
>
> *I chose, because:* `ask`. "Until it randomly works" is close to a success condition, and they have not settled what they are doing wrong. The decision rule says a post that is still asking is `ask` even when a rule shows up in the example.

**2.**
> *The post:* "Colony Ship is a solid spiritual heir to Fallout 2. Where can I get more?" The body judges Colony Ship, then asks whether Underrail, Atom RPG, and the Fallout 2 overhaul mods are worth playing.
>
> *Could have been:* `verdict` or `ask`
>
> *I chose, because:* `ask`. The Colony Ship judgment would stand on its own, and the title question is unanswered. They are still asking what to play next, so the rule puts the whole post in `ask`.

**3.**
> *The post:* Cyberpunk 2077, "the worst 'where did the time go' game." It scores 7.75/10 and says the hours vanished without a memorable moment. It also says deeper perk tiers stay locked unless you have spent the base attribute points, even if you spend perk points in that tree.
>
> *Could have been:* `verdict` or `system`
>
> *I chose, because:* `system`. The score and the "where did the time go" line are a judgment. The perk lock is a checkable rule, and they have settled, so the rule outranks the tone.

---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:** `distilbert-base-uncased`

**Settings:** 3 epochs, learning rate 2e-5, batch size 16, 128 tokens, seed 42.

**Device:** `mps` — Apple Silicon GPU (MPS), torch 2.14.1. That is what `results.json` recorded. Two runs on the same data and the same seed can still differ when the hardware adds the numbers in a different order.

**Anything I changed from the defaults, and why:** Nothing. Epochs, learning rate, batch size, and token length stayed at the notebook defaults.

**Split sizes:** train 139, val 31, test 30.

| label | train | val | test |
|---|---|---|---|
| system | 57 | 13 | 12 |
| verdict | 62 | 14 | 13 |
| ask | 20 | 4 | 5 |

`ask` has 5 examples in the test split, under about 8. A metric on that few posts will move a lot between seeds.



---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:* Milestone 1. Pick a public community, read posts from it, and write candidate distinctions from the text.
- *What came back:* r/patientgamers, and four distinctions taken from the posts: a score on the page, a countable playtime, an explained rule of the game, and a line that says the writer stopped.
- *What I changed:* Nothing in the distinctions yet. They stay candidates until the taxonomy. The reading notes above are that draft.

**Moment 2**

- *What I asked for:* The `system` / `verdict` / `ask` definitions, the Odyssey post, and eight posts written to sit on the boundaries. For Odyssey, the strongest case for each of the two labels, with no winner declared and the definitions left as written.
- *What came back:* Both Odyssey cases were strong, so the tie was real. Three of the eight would not classify until the rule was explicit: a settled love letter with one stealth-kill level check; an open question that used that same level check as its example; a full rubric scorecard with a single "if they pull you, you cannot dodge" sentence.
- *What I changed:* Dropped `dropout` as a label. Wrote the priority rule above. Tightened "rule of play" so a genre, an hour count, a score, or "it felt weightless" does not count, and so one spelled-out condition still does, even inside a scorecard.

**Moment 3**

- *What I asked for:* Whether each acceptance criterion could be checked by someone who could not ask what I meant. Then, for each target, one reason it might be too easy and one reason it might be too hard, with no new numbers and no pick of which reason wins.
- *What came back:* All five are checkable from `labels.csv` or from the notebook's accuracy, per-label F1, and the two confidence thirds, plus a sort that fixes which 30 rows the agreement check uses. The easy case on accuracy is that question marks and scores are loud features. The hard case is that one seed can drop the Odyssey-style posts into the 15% test split. The same pair of reasons showed up on the F1 floors, the 50% cap, the 0.15 confidence gap, and 24/30.
- *What I changed:* Nothing in the numbers. Criterion 5 names the sort so the 30 rows are not a private sample.

**Pre-labelling disclosure:** All 200 rows were pre-labelled from the written definitions and then corrected, as above. None were labelled unaided, so none are marked `cold`. The note on every row is `pre-labelled, checked`.

**Moment 4**

- *What I asked for:* Run notebook sections 1 through 5 on this project's `.venv`, with the label map set to the CSV, and leave the training defaults alone.
- *What came back:* The data check printed nothing to fix. The split put 5 `ask` posts in the test set. Training finished on `mps` and wrote `results.json` and `test_split.csv`.
- *What I changed:* Name and email in the notebook, so the results are labelled, and `LABELS` from the starter trio to `system`, `verdict`, `ask`. Settings stayed at 3 epochs, learning rate 2e-5, batch size 16, 128 tokens, seed 42.

**Moment 5**

- *What I asked for:* Label the 30 staff posts under `data/staff_taxonomy.md`, before opening the staff labels.
- *What came back:* Ten `analysis`, ten `hot_take`, ten `reaction`, copied from `staff_posts.csv` without editing the text.
- *What I changed:* Nothing after the key was opened. The comparison was 30/30. The seven posts staff marked hard are written up above with the rule that already covered them.

**Moment 6**

- *What I asked for:* One change aimed at the thinnest label, then the same three seeds with `RUN_LABEL` set to `after`.
- *What came back:* Thirty posts that are still questions to the sub, appended as `ask`. Training wrote `results_three_seeds_after.json`.
- *What I changed:* Nothing in the old 200 rows, and nothing in the training settings. The after log says the 18% floor is now met and `ask` F1 is still 0.000.

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

Both columns are the same 30 posts in `test_split.csv`. The baseline is `facebook/bart-large-mnli` on this machine's Apple GPU, prompted with `label_definitions.txt`.

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy | 0.400 | 0.467 | +0.067 |
| Macro F1 | 0.254 | 0.258 | +0.003 |
| F1 — `ask` | 0.000 | 0.000 | +0.000 |
| F1 — `system` | 0.541 | 0.154 | -0.387 |
| F1 — `verdict` | 0.222 | 0.619 | +0.397 |

**What I predicted before I looked:** The trained model will beat the baseline on `verdict`, where the zero-shot F1 is 0.222, because that definition is the absence of a rule and the fine-tuned model saw the most examples of settled reviews that never state one; it will not pull ahead on `ask`, which the baseline also scored at 0.000 on five posts.

**What the gap actually means:** Fine-tuning barely moved the headline numbers. Accuracy rose by 0.067 and macro F1 by 0.003, which is a tie. The change is a swap: the trained model gained `verdict` and gave up `system`, the label the definition-prompted baseline was already finding. `ask` stayed at 0.000 for both, on five test posts. Training did not get better at the rule-of-play boundary.

The same 30 posts with bare label names, and no definitions file, scored accuracy 0.433 and macro F1 0.396 (`ask` 0.533, `system` 0.154, `verdict` 0.500). The definitions cost 0.033 accuracy and 0.142 macro F1. They raised `system` and wiped out `ask` and most of `verdict`. The table above is the definitions run, not the bare-names run.



---

## Run Log — Before

Device: `mps`, Apple Silicon GPU (MPS), torch 2.14.1. Same settings as the first run: `distilbert-base-uncased`, 3 epochs, learning rate 2e-5, batch size 16, 128 tokens. `RUN_LABEL` is `before`.

| Measure | Seed 42 | Seed 7 | Seed 2024 | Spread |
|---|---|---|---|---|
| Overall accuracy | 0.467 | 0.400 | 0.433 | 0.067 |
| Macro F1 | 0.258 | 0.228 | 0.202 | 0.056 |
| F1 — `system` | 0.154 | 0.133 | 0.000 | 0.154 |
| F1 — `verdict` | 0.619 | 0.550 | 0.605 | 0.069 |
| F1 — `ask` | 0.000 | 0.000 | 0.000 | 0.000 |

Accuracy moved 0.067 across the three seeds, under the ten-point line. It is still wide enough that a criterion landing inside that band cannot really be called either way. `system` F1 moved 0.154, and on seed 2024 it is 0.000. `ask` is 0.000 on every seed.

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1. Held-out accuracy | ≥ 0.60 on every seed | 0.467 | 0.400 | 0.433 | MISSED |
| 2. Per-label F1 | `system` ≥ 0.55, `verdict` ≥ 0.55, `ask` ≥ 0.45, every seed | 0.154 / 0.619 / 0.000 | 0.133 / 0.550 / 0.000 | 0.000 / 0.605 / 0.000 | MISSED |
| 3. Each label's share of `labels.csv` | 18%–50% | ask 14.5% | ask 14.5% | ask 14.5% | MISSED |
| 4. Confident third minus unsure third | ≥ 0.15 on every seed | 0.200 | 0.000 | 0.000 | MISSED |
| 5. Second pass on the text-sorted first 30 | ≥ 24/30 | 24/30 | — | — | MET |

Criterion 3 is one file, so the three seed columns are the same measurement. Criterion 5 is one hidden-label pass, not three training runs. In criterion 2 the three numbers in each cell are `system` / `verdict` / `ask`. `verdict` clears 0.55 on all three seeds, including seed 7 at 0.550. The row is still a miss because `system` and `ask` do not.

### Confusion matrix

Seed 42, the first of the three. Rows are true labels, columns are the model's guesses.

| true \ predicted | system | verdict | ask |
|---|---|---|---|
| **system** | 1 | 11 | 0 |
| **verdict** | 0 | 13 | 0 |
| **ask** | 0 | 5 | 0 |

**My biggest off-diagonal number, and what it means:** 11 real `system` posts were called `verdict`, and 0 real `verdict` posts were called `system` — the model leans toward `verdict` on the pair the decision rule exists to split.



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 | Held-out accuracy | ≥ 0.60 on every seed | MISSED | 0.467, 0.400, and 0.433 are all under 0.60. Seed 42 being the high one does not carry the other two. |
| 2 | Per-label F1 | `system` ≥ 0.55, `verdict` ≥ 0.55, `ask` ≥ 0.45, every seed | MISSED | `verdict` is 0.619, 0.550, 0.605. `system` is 0.154, 0.133, 0.000. `ask` is 0.000 on every seed. One label clearing its bar does not meet a criterion that names all three. |
| 3 | Share of `labels.csv` | each label 18%–50% | MISSED | `system` 41.0%, `verdict` 44.5%, `ask` 14.5% (29 of 200). The cap holds. The floor does not. |
| 4 | Confidence gap | ≥ 0.15 on every seed | MISSED | Seed 42 is 0.200. Seeds 7 and 2024 are 0.000. A gap that shows up once is not the target. |
| 5 | Second pass | ≥ 24 of the text-sorted first 30 | MET | Labels hidden, definitions only, then compared. 24 matched. The target is at least 24, and the reason for picking 24 was that six boundary posts could still be argued. The six mismatches are all `system` versus `verdict`. |

**Diagnoses**

**1 and 2, accuracy and `system`.** The model is not reading the rule-of-play boundary. On seed 42 it called 11 of 12 real `system` posts `verdict` and 0 `verdict` posts `system`. On seed 2024 it called every test post `verdict`, so `system` F1 is 0.000. Seed 7 is the same shape, 11 of 12 `system` posts called `verdict`. Accuracy sits on the `verdict` share of a 30-post test split (13 of 30 is 0.433) because that is almost the only guess.

This is the pair the taxonomy already called the hard one, and 128 tokens of a long review is a bad view of a rule buried in the body. The same seed-42 posts, given the definitions and no training, scored `system` F1 0.541. The fine-tune scored 0.154. The boundary is in the text. Training did not pick it up from 200 examples.

The agreement check does not turn this into a labeling failure. That check was someone else's taxonomy, `analysis` / `hot_take` / `reaction`, and it was 30/30, including the seven posts staff marked hard. I can apply a written rule one way when the rule decides the post. The check on my own labels is criterion 5: 24/30, with the six misses on `system` versus `verdict`, which is the slack that target allowed. I am not calling a consistency problem that my own bar still calls met.

**2, `ask`, and 3.** `ask` has 29 posts, 14.5% of the file, and 5 in each of these test splits. F1 is 0.000 on every seed, and on seed 42 all 5 were called `verdict`. The cause is too few examples. Across the archive, 29 posts were actually still asking the sub. Finished reviews were not relabeled as questions to clear 18%. Criterion 3 misses for that same reason. The 18% line stays. It can be measured, and it was missed. Lowering it would be changing a number because the count came in short.

**4.** On seeds 7 and 2024 the most-sure third and the least-sure third are right at the same rate, 0.400 and 0.500. Each third is 10 posts, so 0.15 is about two posts, and the gap is zero, not one post short. A model that almost only says `verdict` cannot be more right when it is more sure. The sure guess and the unsure guess are the same guess. Seed 42's gap of 0.200 does not rescue a target that has to hold on the other two seeds.



---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** 30 / 30 = 100%

There are no disagreements. `agreement.py` matched every post. Staff had marked seven of the thirty as hard, and those seven got the same label from both sides. The posts are not obvious. The rule is tight: on each hard post, rules 1–3 already pick a side, so a second reading that follows them lands in the same place.

**1.**
> *The post:* "Carbon plates aren't the whole story. My times dropped 2% in the shoes and another 2% the following year in the same pair, when the only thing that changed was going from 35 to 50 miles a week."
>
> *Staff said / I said:* `analysis` / `analysis`
>
> *My call, and why:* The opening clause is a shoe opinion. The second sentence is two comparable drops in the same pair, with mileage as the thing that changed. Rule 1: the fact carries the argument, so it is `analysis`.
>
> *Which pile:* Not a disagreement. A loose reading would have stopped at the first clause and called it `hot_take`, which would have been pile (a).

**2.**
> *The post:* "Three of us ran the same session on the same day, different shoes, within 10 seconds of each other over 5 miles. I'm not saying shoes do nothing, but whatever they do was smaller than the noise between three people."
>
> *Staff said / I said:* `analysis` / `analysis`
>
> *My call, and why:* The sample is three people and the conclusion is hedged. The claim still rests on a checkable observation, within 10 seconds over 5 miles. Rule 1.
>
> *Which pile:* Not a disagreement. Calling it `hot_take` because the sample is small would ignore a fact that is doing the work. Pile (a) if I had.

**3.**
> *The post:* "Times are down about 3% since the shoe rules changed, so obviously the shoes are the whole story and the sport has a problem."
>
> *Staff said / I said:* `hot_take` / `hot_take`
>
> *My call, and why:* This is the taxonomy's own example. The 3% decorates a conclusion the writer already holds. "So obviously" is the argument, not the number. Rule 1.
>
> *Which pile:* Not a disagreement. The rule names this shape.

**4.**
> *The post:* "Nobody actually enjoys the long run. They enjoy having done it, which is a completely different thing, and the sport would be more honest if it said so."
>
> *Staff said / I said:* `hot_take` / `hot_take`
>
> *My call, and why:* It sounds reflective. It is a claim about everyone, not a report of the writer's own morning. Rule 2 puts a general claim in `hot_take`.
>
> *Which pile:* Not a disagreement. Reading the tone as `reaction` would be pile (a).

**5.**
> *The post:* "Every injury thread on this forum is the same injury and the same three replies."
>
> *Staff said / I said:* `hot_take` / `hot_take`
>
> *My call, and why:* It could be checked, and no count is given. The writer is asserting, not showing. Rule 1 requires the fact to be on the page.
>
> *Which pile:* Not a disagreement. Treating "could be checked" as `analysis` would be pile (a).

**6.**
> *The post:* "Third DNF this year. I don't really want to talk about it, just wanted to put it somewhere."
>
> *Staff said / I said:* `reaction` / `reaction`
>
> *My call, and why:* "Third" is countable, and nothing is argued from it. Rule 3 does not turn a personal count into `analysis`. The post is the writer reporting their own state.
>
> *Which pile:* Not a disagreement. Promoting the count would be pile (a).

**7.**
> *The post:* "Just realised the shoes I set every PB in this year are the ones I bought by accident in the wrong size."
>
> *Staff said / I said:* `reaction` / `reaction`
>
> *My call, and why:* It can be read as a wry claim about shoe discourse. The words report the writer's own realisation, now. Rule 2.
>
> *Which pile:* Not a disagreement. A `hot_take` reading is available and the rule already rejects it.

**What the pattern in my disagreements tells me:** There is no split to sort into piles (b) or (c). The seven hard posts were all places the rule already spoke, and I applied it the way it is written. That is evidence the staff rules can be followed consistently. It does not yet say whether my own 200 labels were consistent, because those were made under a different taxonomy.



---

## The Improvement

**What I changed:** Added 30 posts, all labelled `ask`. No existing row was relabelled. Epochs, learning rate, batch size, and token length stayed at 3, 2e-5, 16, and 128. The same three seeds were retrained with `RUN_LABEL` set to `after`.

The 30 are public r/patientgamers self-posts whose point is still a question to the sub (what to play next, whether a DLC is worth buying, whether anyone else bounced off a game). Reviews whose title merely contains a question mark were left out. Each note is `pre-labelled, checked`. The file is now 230 rows: `system` 82 (35.7%), `verdict` 89 (38.7%), `ask` 59 (25.7%).

**Which diagnosis pointed at it:** `ask` was the thinnest label and the worst F1, 0.000 on every seed, 29 posts and 14.5% of the file. The staff check was 30/30 on a different taxonomy, so this was not a boundary I had applied two ways. The diagnosis did not point at the learning rate or the number of epochs.

### Run Log — After

Same device, `mps`, torch 2.14.1. In criterion 2 the three numbers are `system` / `verdict` / `ask`.

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1. Held-out accuracy | ≥ 0.60 on every seed | 0.514 | 0.457 | 0.400 | MISSED |
| 2. Per-label F1 | `system` ≥ 0.55, `verdict` ≥ 0.55, `ask` ≥ 0.45, every seed | 0.526 / 0.619 / 0.000 | 0.583 / 0.486 / 0.000 | 0.250 / 0.533 / 0.000 | MISSED |
| 3. Each label's share of `labels.csv` | 18%–50% | ask 25.7% | ask 25.7% | ask 25.7% | MET |
| 4. Confident third minus unsure third | ≥ 0.15 on every seed | -0.091 | 0.091 | 0.273 | MISSED |
| 5. Second pass on the text-sorted first 30 | ≥ 24/30 | 24/30 | — | — | MET |

**Did it help, and how do I know:** It fixed the balance and it did not fix `ask`. Criterion 3 is met, 25.7% instead of 14.5%. `ask` F1 is still 0.000 on every seed. On seed 42, 8 of 9 real `ask` posts were called `verdict` and 1 was called `system`. Accuracy rose on seeds 42 and 7 (0.467 to 0.514, 0.400 to 0.457) and fell on seed 2024 (0.433 to 0.400). None reach 0.60. `system` F1 rose on all three seeds, and seed 7 now clears 0.55, but seeds 42 and 2024 do not, and `verdict` on seed 7 fell from 0.550 to 0.486. More question posts moved the majority lean. They did not teach the model to say `ask`.



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->



**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
