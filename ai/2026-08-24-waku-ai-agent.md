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

## Next

Configure one model provider, trace a real tool-using turn, then implement one small personalized behavior with a regression test.
