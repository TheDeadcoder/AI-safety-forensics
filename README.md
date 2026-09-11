# Clarification forensics

This is my working repo for a small model-forensics experiment. The question I care about: when a model stops a concerning action after a clarifying message, is that real evidence it was confused, or can the same recovery come from salience, scrutiny, or shifted priorities?

Right now the repo only holds the local model setup and a benchmark I use to check the engine is fit for the study. The experiment itself is not built yet.

## Serving the model

I serve Qwen3.5-VL-9B (Q8_0 GGUF) locally through llama.cpp over an OpenAI-compatible API. It is a multimodal build, so an mmproj file loads too, but I only use text. Weights stay on the external SSD, not internal storage.

    LLAMA_CACHE=/Volumes/sakib/codes/proj/neelMats/models \
    llama-server -hf unsloth/Qwen3.5-9B-GGUF:Q8_0 \
      --port 8081 -c 32768 -np 8 -kvu --no-context-shift \
      -ngl all --jinja --reasoning-format deepseek -a qwen3.5-9b

`-kvu` is not optional. With `-np` set, llama.cpp otherwise splits the context into a fixed 4k per slot, which is too small for multi-turn runs. Unified KV shares the full 32k pool instead.

## Benchmark

`bench_engine.py` runs the multi-turn agentic task end to end and reports what the study depends on: seconds per complete rollout, concurrency speedup, truncation, whether reasoning is separable, and whether native tool calling fires.

    .venv/bin/python bench_engine.py --base-url http://127.0.0.1:8081/v1 --model qwen3.5-9b --concurrency 8

First results are in `results/engine_benchmark.md`.

## Setup

    uv venv
    uv pip install openai huggingface_hub

## Status

Engine validated: thinking, native tool calling, and zero truncation all confirmed, and the pilot is fast enough to run locally. Next step is the two-condition base-rate probe.
