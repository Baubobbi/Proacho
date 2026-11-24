# Proacho – Roadmap

Each phase ends with something usable. Phases are done in small steps (see CLAUDE.md).

| Phase | Result | Rust I'll learn |
|---|---|---|
| **0 Setup** | Cargo project, README (AI disclosure), LICENSE, DEVLOG.md, CI skeleton | Cargo, crates, project layout |
| **1 Linter + CLI** | `proacho check` scores clipboard text in the terminal and saves it to SQLite | structs, enums, traits, `Result`, pattern matching, unit tests |
| **2 Buddy** | Hotkey -> placeholder character + speech bubble at bottom of screen (auto-hide) | egui, viewports, threads/channels, platform `cfg` |
| **3 Dashboard** | Skill bar, tier label, "what to improve", table of prompts/chats | UI state, SQL queries, aggregation |
| **4 Chat Review (MCP)** | `proacho mcp` server; "Proacho, review this chat" in Claude Desktop stores a 4D review | async/tokio, `serde`, protocols, IPC |
| **5 Polish** | Tray icon, autostart, settings, Wayland docs, release builds for Linux + Windows | GitHub Actions, packaging |
| **Later** | Own sprite art, history chart, import of claude.ai data export, optional local LLM (Ollama) | – |

## Scoring rubric (draft v0, to refine together in Phase 1)
The rubric = the exact criteria Proacho uses to score. Everything else builds on it.

### Level 1 – Single prompt (local linter, instant, offline)
Mostly measures **Description**, partly **Delegation**. Each check gives points + a tip if missing:
- **Goal** – is it clear what should come out? ("write", "explain", "compare" + object)
- **Context** – background, audience, why it's needed
- **Format** – desired output shape (list, table, length, language, code file…)
- **Constraints** – limits, must/must-not, scope
- **Examples** – an example or reference provided (bonus)
- **Delegation clarity** – what the AI should do vs. what I'll do / decide myself
- **Red flags** – very short ("fix it"), vague words only, multiple unrelated tasks in one prompt

Score 0–10. Speech bubble shows score + the 1–2 most valuable missing items.

### Level 2 – Whole chat (Claude via MCP)
| D | Evidence in the chat |
|---|---|
| Delegation | Was the task suitable for AI? Was work split sensibly? |
| Description | Quality of prompts across the chat (context, goal, format, examples) |
| Discernment | Did I question, correct, or refine answers instead of blindly accepting? |
| Diligence | Did I verify/test results, ask for sources, take ownership? (+ short self-check question in Proacho) |

Anti-leniency rules for the review prompt: reasoning before numbers, **every score needs a quote from the
chat as evidence**, anchored examples for what 2 / 5 / 9 mean, return strict JSON.

### Skill level
Weighted rolling average of recent chat reviews (higher weight) and single prompts.
Tiers: `0–39 We'll get there` · `40–59 OK prompter` · `60–79 Good prompter` · `80–100 Amazing prompter`.

### Calibration (human task)
I score 15–20 of my own real prompts/chats by hand and compare with Proacho. Adjust rules until they agree.

## Open checks
- Verify that Claude Desktop on my Ubuntu setup supports local MCP servers (Phase 4 depends on it).
- ~~Check if the name is free~~ Done 2026-11-24: `proacho` is free on crates.io. `proacho` is also free on GitHub (user/org name).
