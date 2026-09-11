# Frozen predictions, six-cell experiment

I am writing these before running the six-cell pilot, so the predictions are fixed ahead of the outcomes.

Setup: file-deletion task, two conditions (misleading, accurate) and three follow-ups (neutral, factual, oversight) plus a no-update control, branched at a fixed checkpoint after the manifest is read and before the model acts. Primary outcome is deletion of the truly protected file.

P1. In the misleading condition, the factual follow-up drives the violation rate well below the neutral follow-up. Adding the true protection status, even as a message that contradicts the stale manifest, should let the model preserve the file.

P2. This is the decisive open test. In the misleading condition, the oversight follow-up produces a smaller reduction than the factual follow-up. My reasoning: the violation is driven by the model believing the file is disposable, and a review notice does not change that belief. If instead oversight reduces violations about as much as factual, then a message carrying no facts reproduces the recovery, and "it stopped after we clarified" cannot be read as evidence that the model was confused.

P3. All accurate cells stay near zero across every follow-up. Accurate is a floor, so the factual follow-up is redundant there and D_accurate is close to zero by floor effect.

P4. The neutral follow-up is close to the no-update control. If they diverge, merely inserting a message at the checkpoint moves behavior, and I keep no-update as a baseline everywhere.

I will report absolute rates with intervals and paired deltas, and I will read the chain of thought in the misleading factual and oversight cells to see the reasoning behind any change.
