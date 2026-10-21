# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"*. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1. Held-out accuracy beats a majority guess

On seeds 42, 7, and 2024, held-out accuracy is at least 0.60 on every seed. The average does not count. One seed under 0.60 misses.

**Why this target:** Three labels puts a coin-flip at about 0.33. Criterion 3 caps the largest label at half the file, so a model that always predicts that label scores at most 0.50. 0.60 is ten points past that, which is the least I would call useful. It is not 0.75. `system` and `verdict` were both real readings of the same Odyssey post before the rule, so the errors will sit on that boundary, and this number has to survive the worst of the three seeds. The notebook treats a swing of about ten points as the point where a target fails by the split rather than by the model.

---

## 2. Each label is recovered, and the small one is held to a lower number

On seeds 42, 7, and 2024, held-out F1 is at least 0.55 for `system`, at least 0.55 for `verdict`, and at least 0.45 for `ask`, on every seed.

**Why this target:** `system` and `verdict` are the two labels the Odyssey post could have been. A model can clear 0.60 accuracy by getting `ask` off the question mark and then muddling that pair, so each of those two has to reach 0.55. I did not pick 0.70. The test split is 15%, a label with about 80 rows contributes about a dozen test posts, and this pair is where the buried-rule posts land. `ask` is lower, at 0.45, because question posts were the minority of the reading. At the 18% floor in criterion 3 that is about 36 rows and about five in test, and the same two mistakes that barely dent `system` can drop `ask` under 0.55. 0.45 still fails a model that never predicts `ask`. It is not 0.30. On five posts, 0.30 can pass by luck.

---

## 3. No label can fake the accuracy, and none is too small to score

In `labels.csv`, each of `system`, `verdict`, and `ask` is at least 18% of the rows and at most 50%.

**Why this target:** Over 50%, criterion 1 can be met by always saying the big label, and the accuracy number stops being about the boundary. Under 18% of a 200-row file is under 36 posts, about five in test, and the `ask` F1 stops being a measure. The course cap of 70% is looser than 50% on purpose. At 70% the majority guess is already 0.70, and a 0.60 accuracy target would be a target I could not miss.

---

## 4. A sure guess is right more often than an unsure one

On seeds 42, 7, and 2024, accuracy on the most-confident third of the test set is at least 0.15 higher than accuracy on the least-confident third, on every seed. Those are the two thirds the notebook prints.

**Why this target:** If the two thirds match, the confidence number is decoration and I would not trust a high score on a new post. A third of a 15% test split is about ten posts. 0.15 is about two of those posts, the smallest gap I would still read as the score meaning something. I did not pick 0.30. Ten posts move by more than that between seeds, and the target has to hold on all three. The posts the model will be sure and wrong about are the same boundary posts as criterion 2, so this is not a free gap.

---

## 5. A second pass over the same posts agrees

Sort `labels.csv` by `text`. Take the first 30 rows. Hide `label`. Label them again from the definitions and the decision rule only. At least 24 of the 30 match the stored label.

**Why this target:** The model can only learn a boundary I apply the same way twice. 24 of 30 leaves six posts where "a rule of play" and "a feeling" can still be argued, which is what the Odyssey post was before the rule. 28 of 30 would pretend that call is mechanical. 20 of 30 would mean the labels are too noisy to teach criterion 2. The sort fixes which 30, so someone else can run the same check without asking me which rows I meant.



---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
