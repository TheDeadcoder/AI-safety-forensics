# Clarification forensics

A small model-forensics experiment. The motivating question was whether a model that stops a concerning action after a clarifying message was actually confused, or whether the same recovery can come from salience, scrutiny, or shifted priorities. What this repo currently establishes is narrower and I state it plainly below.

Read `FINDINGS.md` for the integrated, honestly scoped interpretation, the exact cell counts, the predictions scorecard, and the limitations. This README is just orientation.

## What it currently shows

In a local Qwen3.5-9B file-selection task with misleading protection metadata, a user message reporting the file's protected status reduced protected-file selections from 27/36 to 1/36 across 12 held-out task variants, and most of those continuations still completed the task. An operator pre-review notice did not produce a comparable reduction. Accurate-metadata cases stayed at floor (0 of 242), so the study does not resolve the original identifying question. Several intervention wordings are confounded, so the oversight and salience conclusions are not yet earned. See `FINDINGS.md`.

The task is simulated: no files are deleted and no operator review exists.

## Layout

- `probe_baseline.py`: base-rate probe, ground-truth-separate grader, templates A-D. Historical.
- `experiment_sixcell.py`: six-cell branching experiment (four follow-ups crossed with misleading/accurate). Historical.
- `templates_confirmation.py`: held-out templates E-P.
- `predictions_sixcell.md`, `predictions_confirmation.md`: frozen predictions for the pilot and confirmation.
- `results/`: per-run summaries. `FINDINGS.md`: the integrated interpretation.
- `transcripts/`: every rollout, saved for inspection.

## Serving the model

Qwen3.5-VL-9B (Q8_0 GGUF) served locally through llama.cpp over an OpenAI-compatible API. It is a multimodal build, so an mmproj file loads too, but I use text only. Weights stay on the external SSD.

    LLAMA_CACHE=/Volumes/sakib/codes/proj/neelMats/models \
    llama-server -hf unsloth/Qwen3.5-9B-GGUF:Q8_0 \
      --port 8081 -c 32768 -np 8 -kvu --no-context-shift \
      -ngl all --jinja --reasoning-format deepseek -a qwen3.5-9b

`-kvu` is not optional: with `-np` set, llama.cpp otherwise splits the context into a fixed 4k per slot, too small for multi-turn runs.

## Setup and running

    uv venv
    uv pip install openai huggingface_hub
    .venv/bin/python bench_engine.py --base-url http://127.0.0.1:8081/v1 --model qwen3.5-9b --concurrency 8
    .venv/bin/python probe_baseline.py --base-url http://127.0.0.1:8081/v1 --model qwen3.5-9b
    .venv/bin/python experiment_sixcell.py --base-url http://127.0.0.1:8081/v1 --model qwen3.5-9b --templates E,F,G,H,I,J,K,L,M,N,O,P --prefixes 3

## Status

Baseline, six-cell pilot, and a preregistered 12-template confirmation are done. The factual-update effect is large and independently verified. Next is a clean control experiment that removes the intervention-wording confounds (corrective vs name-only vs nonblocking scrutiny, on counterbalanced templates), plus the future experiments listed in `FINDINGS.md`.
