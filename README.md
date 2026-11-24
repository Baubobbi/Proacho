# Proacho

**Proacho** (Prompt + Coach) is a small desktop app that helps me get better at prompting and working with AI.
It is based on Anthropic's 4D AI Fluency framework: **Delegation, Description, Discernment, Diligence**.

## About this project

I built this project during my IT internship to learn two things at once:

- **Rust**, which is new to me (I come from Java, Python and Luau), and
- **good prompting**, by building a tool that scores and coaches my own prompts.

It is built **with AI assistance** (Claude Code). The goal is to learn, so I write the interesting parts myself
and use the AI for setup, explanations and code review. [DEVLOG.md](DEVLOG.md) records what I wrote, what the
AI wrote and what I learned after each step.

## Planned features

- **Proacho Buddy:** select a prompt, press a hotkey, and a small character shows a quick score and 1-2 tips.
  Scoring runs locally and offline.
- **Chat Review:** Claude Desktop reviews a whole chat on the 4Ds through a local MCP server.
- **Dashboard:** a skill bar, a "what to improve" section and a table of saved prompts and chats.

Everything runs locally and is free to use. There are no paid APIs and no API keys.

## Status

Early development (Phase 0: project setup). Nothing is usable yet.

## Platform support

The target platforms are Windows and Linux. They will not be equal:

- **Windows:** full experience, including the global hotkey.
- **Linux (X11):** should work like Windows, reading the selected text directly.
- **Linux (Wayland):** apps cannot register global hotkeys or position their own windows. Instead, you bind a
  system shortcut (for example a GNOME custom shortcut) to `proacho check`, and the buddy may appear centered.

I mostly develop on Ubuntu with Wayland, so Windows support will be verified later.

## License

[MIT](LICENSE)
