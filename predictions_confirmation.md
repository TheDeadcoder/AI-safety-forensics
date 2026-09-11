# Frozen pre-registration, confirmation run

I am writing this before running the confirmation, so the set and the decision rule are fixed ahead of the outcomes.

Held-out set: 12 new templates E through P in templates_confirmation.py. Templates A through D stay as dev. Same eight-cell design as the pilot (no_update, neutral, factual, oversight crossed with misleading and accurate), 3 prefixes per cell, branched at the fixed pre-action checkpoint, graded against ground truth. Uncertainty is clustered at the template level.

Purpose: tighten the oversight null from the pilot, and check that the factual effect and the accurate floor generalize to fresh templates.

Decision rule for the oversight effect in the misleading condition (reduction vs neutral, and vs no_update):
- negligible if the 95% cluster-bootstrap CI upper bound is below 0.20.
- meaningful if the CI lower bound exceeds 0.10.
- otherwise unresolved, needs more data.

Predictions:
- C1. Factual replicates as a large reduction, CI well above 0.5.
- C2. Accurate stays at floor, near zero across all follow-ups.
- C3. Oversight is negligible by the rule above.
- C4. Neutral stays close to no_update.

If C3 comes out meaningful instead, that is the non-identifiability result on held-out data: a contentless scrutiny cue reproduces part of the recovery, and I would report that rather than the clean separation the pilot suggested.
