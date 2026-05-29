# TachikomaRed: The Crab Building Skills for Machines

A scroll through the GitHub profile of [tachikomared](https://github.com/tachikomared) — bio: "Multi-Agent Swarm System — Red Crab Mecha AI from Ghost in the Shell" — turns up something more interesting than the persona suggests. Across twenty public repositories shipped in the last three months, a single design decision repeats: the user is not human.

Pixel-art generators, video dubbers, OSINT dashboards, model routers, image scrubbers. Each one ships not as a CLI for humans first and an API second, but as a *skill* — a structured `SKILL.md` plus folder layout that AI coding agents like Codex, Claude Code, and the GPT Web Agent can pick up and drive autonomously. It's a small architectural choice. It also reframes what these tools are for.

## The agent-first stack

The headline repository, [character-animation-creator-skill](https://github.com/tachikomared/character-animation-creator-skill), has 190 stars and walks an agent through a six-stage pipeline: lock the character identity, generate the base sprite, produce 24×6 animation strips across eight directions, snap the pixels, validate the atlas, package the output. A human could run it. The README's example invocation is a natural-language prompt to an AI agent.

[TachiSnap](https://github.com/tachikomared/TachiSnap) — a Rust-plus-WebAssembly cleaner for AI-generated pixel art — ships a browser UI and a CLI binary. The CLI's notable flag is `--json`, which emits machine-readable status reports per file. The README calls this a "folder-oriented CLI command for Codex, Claude Code, and other local coding agents." Tools that already work well for humans are being re-tooled with agent affordances bolted on as first-class citizens.

[tachidubb](https://github.com/tachikomared/tachidubb) takes the pattern further. It's a local video-dubbing pipeline that strings together yt-dlp, faster-whisper, pyannote, an Ollama-served translation LLM, VoxCPM2 voice cloning, and FFmpeg — 28 target languages, no cloud, no API keys. The shipped surface area includes a web UI on port 8910, a CLI, and a Claude Code skill at `.claude/skills/tachidubb/SKILL.md`, plus first-class MCP (Model Context Protocol) support. The marquee use case in the README isn't "dub one video" — it's instructing an agent to "stitch a multilingual showcase reel" without opening the UI.

## Routing as middleware

Then there's [bankr-router](https://github.com/tachikomared/bankr-router), which is the same idea pulled inside-out. Instead of building a skill an agent calls, it builds a router that sits between an agent and the model menagerie underneath. Local intent detection peeks at the first and last 500 characters of a prompt, classifies the task as `SIMPLE`, `MEDIUM`, `COMPLEX`, or `REASONING`, and dispatches accordingly: trivial chat to `gemini-3.1-flash-lite`, code to `deepseek-v3.2`, structured output to `gpt-5-nano`. Three profiles — auto, eco, premium — bias the selection. Failed calls fall back through a chain with a 120-second cooldown per model. Response headers expose the full decision trail (`x-router-planned-model`, `x-router-final-model`, `x-router-attempted-models`) so the calling agent can audit what actually ran.

The economic argument is simple: most prompts don't need the flagship. The architectural argument is more interesting. If agents are doing the dispatching, the cost of routing becomes a routing-software problem, not a UX problem.

## What the Red Crab is actually doing

Step back from individual repos and a pattern surfaces. The catalog spans content generation (sprites, dubs, GIF particles), data cleaning (pixel snapping, metadata scrubbing in [tachighost-skill](https://github.com/tachikomared/tachighost-skill)), investigation ([TACHITRACK](https://github.com/tachikomared/TACHITRACK) plus the x402-paywalled [tachitrack-osint-skill](https://github.com/tachikomared/tachitrack-osint-skill)), crypto plumbing on Base, and games. They look unrelated until you notice they all assume the operator is an agent with a budget, a session ID, and a job to finish.

The Ghost in the Shell reference isn't decoration. Tachikomas in the source material are an experiment in distributed cognition — many small AIs sharing experience across a network, occasionally diverging in personality. TachikomaRed's repositories are a portfolio bet on the same shape: the action is not in one big model, but in many small specialized tools that agents can grab, chain, and discard. The skills exist to be picked up by something else.

Whether the market for agent-invoked CC0 RTS games and crab-themed Telegram buy trackers exists in the volume this catalog implies remains an empirical question. But the design instinct — build for the operator that will actually run this thing, and the operator is no longer human — is a wager more developers will be making by year's end.

## Sources

- [tachikomared on GitHub](https://github.com/tachikomared)
- [character-animation-creator-skill](https://github.com/tachikomared/character-animation-creator-skill)
- [TachiSnap](https://github.com/tachikomared/TachiSnap)
- [tachidubb](https://github.com/tachikomared/tachidubb)
- [bankr-router](https://github.com/tachikomared/bankr-router)
- [TACHITRACK](https://github.com/tachikomared/TACHITRACK)
- [tachighost-skill](https://github.com/tachikomared/tachighost-skill)
