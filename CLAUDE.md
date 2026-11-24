# Proacho – Project Context for Claude

## What Proacho is
Proacho (Prompt + Coach) is a lightweight desktop app in Rust that helps me get better at prompting
and working with AI, using Anthropic's 4D AI Fluency framework:
**Delegation, Description, Discernment, Diligence**.

Two core features:
1. **Proacho Buddy** – I select a prompt anywhere, press a global hotkey, and a small character pops up
   at the bottom of the screen with a speech bubble: a quick score + 1–2 concrete tips.
   Scored instantly and offline by a local rule-based "prompt linter".
2. **Chat Review** – At the end of a chat in Claude Desktop I say "Proacho, review this chat".
   Proacho runs as a local **MCP server**; Claude scores the whole chat on all 4Ds (with evidence quotes)
   and sends the result to Proacho via an MCP tool. No copy-pasting.

Plus a **dashboard**: a central skill bar with a tier label ("We'll get there" / "OK prompter" /
"Good prompter" / "Amazing prompter"), a "what to improve" section, and a table of saved prompts/chats
with their scores.

See `ROADMAP.md` for phases and the scoring rubric.

## Hard constraints
- **100% free to run.** No paid APIs, no API keys. Chat review uses my existing Claude Desktop via MCP.
- **Cross-platform: Linux (Ubuntu, often Wayland) and Windows.** Windows gets the full experience;
  on Linux degrade gracefully (see Platform notes). Never break one platform for the other.
- **Lightweight:** single binary, local SQLite file, no server, no web stack.
- All UI text, code, comments and docs in **English**.
- Never invent the character art. Use a simple placeholder (shapes/emoji); I draw the real sprites myself.

## Tech stack (agreed, change only after asking me)
- UI + buddy overlay: `eframe` / `egui` (transparent, borderless, always-on-top viewport for the buddy)
- Storage: `rusqlite` (bundled feature)
- Clipboard: `arboard` (incl. Wayland data-control / X11 primary selection)
- Hotkey: `global-hotkey` (Windows, X11); simulate Ctrl+C on Windows with `enigo`
- Tray: `tray-icon`
- Serialization: `serde`, `serde_json`
- MCP server: `rmcp` (official Rust MCP SDK), stdio transport
- Single-instance + IPC between CLI modes and the running app: local socket (e.g. `interprocess`)

One binary, several modes:
```
proacho          -> background app: tray, DB, buddy overlay, dashboard window
proacho check    -> trigger the buddy (used by OS shortcuts, e.g. on Wayland)
proacho mcp      -> MCP server started by Claude Desktop
```

## Platform notes
- Wayland: apps cannot register global hotkeys or position their own windows.
  Fallback: user binds a GNOME custom shortcut to `proacho check`; buddy may appear centered.
  Document this honestly in the README.
- Linux X11: read selected text from the PRIMARY selection directly.
- Windows: simulate Ctrl+C, read clipboard, then restore the previous clipboard content.

## HOW WE WORK TOGETHER (most important section)
I'm learning Rust with this project. I'm experienced in **Java, Python and Luau**, but a **Rust beginner**.
The goal is that I understand and co-write the code, not that you finish it alone.

- **Small steps.** One feature or one module at a time. Never implement a whole phase in one go.
  Before each step, tell me briefly what you're about to do and why, then wait for my OK on anything
  non-trivial (new module, new crate, architecture change).
- **I write the interesting parts.** Handle boilerplate and setup yourself, but for core logic
  (especially the prompt linter, scoring, data model decisions) leave a `TODO(human)` with clear
  guidance, explain the trade-offs, and wait for me. Then review my code like a kind but honest senior dev.
- **Explain Rust through what I know.** When a new concept appears (ownership, borrowing, lifetimes,
  `Result`/`?`, `Option`, traits, enums with data, pattern matching, iterators, `Arc<Mutex<_>>`, async),
  give a short comparison to Java/Python and a one-line "why Rust does it this way".
- **Don't hide complexity.** If something is hard or platform-specific, say so. No silent workarounds.
- **Explain compiler errors** instead of just fixing them, at least the first time a kind of error appears.
- **Tests:** every scoring rule gets unit tests. Run `cargo fmt`, `cargo clippy`, `cargo test` before
  saying a step is done.
- **DEVLOG:** after each finished step, append a short entry to `DEVLOG.md`:
  what was built, what *I* wrote vs. what *you* wrote, and what I learned. Keep it honest.
- **Commits:** small, meaningful commits. Suggest a commit message; I commit myself.
- If I say "just do it", you may implement that step fully, but still explain afterwards.

## Repo expectations (it's a portfolio project)
- README states clearly: built with AI assistance (Claude Code) as a Rust learning project,
  and links to `DEVLOG.md`.
- MIT license. Clean structure, no dead code, meaningful names.
