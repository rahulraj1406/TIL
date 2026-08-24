# Running and Understanding Waku Agent Locally

**Date:** 2026-08-24  
**Topic:** AI / Agentic Systems  
**Replicated from:** [ShenSeanChen/waku-agent](https://github.com/ShenSeanChen/waku-agent)

## What I Did

- Cloned the Waku Agent source and created a local Python 3.11 virtual environment with `uv`.
- Installed the project in editable mode so local code changes take effect immediately.
- Read the core loop, app wiring, session, tools, memory, and architecture documentation.
- Established a clean baseline: `615` deterministic tests passed and `60` optional-integration tests skipped.
- Started a living `learning.md` journal in my local Waku project.

## What I Learned

An AI agent is more than one chatbot call. Waku assembles working context, asks an LLM to reason, lets it request typed tools, executes those tools in Python, feeds the results back, and repeats until the model replies. Python controls permissions, persistence, tracing, and iteration limits; the model chooses the next action.

Its four main pillars are **Harness, Loop, Memory, and Eval/LLM-Ops**. Memory is separated into working, semantic, episodic, and procedural forms, while a retrieval gate avoids injecting irrelevant history. Deterministic tests make most of the control flow verifiable without an API key or model cost.

## Resources

- [Waku Agent repository](https://github.com/ShenSeanChen/waku-agent)
- [Waku architecture](https://github.com/ShenSeanChen/waku-agent/blob/main/docs/architecture.md)
- [Waku core agent loop](https://github.com/ShenSeanChen/waku-agent/blob/main/waku/loop/agent.py)
- [20-minute Waku code walkthrough](https://youtu.be/rvRyBhILrls?si=lOKXfuTsUTMRjhr4)

## NVIDIA NIM Extension

I added NVIDIA NIM as an OpenAI-compatible Waku provider without adding another HTTP dependency. The main model is `stepfun-ai/step-3.7-flash`; the lightweight memory gate uses `meta/llama-3.2-3b-instruct`. I also added a direct image-understanding example, provider settings, a dashboard logo, and regression coverage. The updated baseline is `619` tests passed and `60` optional tests skipped.

During live validation, Step 3.7 Flash was too slow for an interactive text turn, so I selected `nvidia/nemotron-3-nano-30b-a3b` locally for the main agent. The gate correctly skipped irrelevant memory, the model responded successfully, SQLite and JSONL tracing recorded the turn, and the dashboard started on `localhost:7777`.

- [NVIDIA Step 3.7 Flash](https://build.nvidia.com/stepfun-ai/step-3.7-flash)
- [NVIDIA hosted NIM API documentation](https://docs.api.nvidia.com/nim/reference/llm-apis)

## Next

Add the NVIDIA key locally, trace a real tool-using turn, then implement one small personalized behavior with a regression test.
