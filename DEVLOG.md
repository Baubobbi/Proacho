# Development Log

An honest record of how Proacho is built. After each finished step: what was built, who wrote what
(**me** = Baubobbi, **Claude** = Claude Code) and what I learned.

## Phase 0: Setup

### 2026-11-24: Project skeleton

**Built**
- Git repository, `.gitignore`, Cargo project (`cargo init`, edition 2024), `LICENSE` (MIT), `README.md`.
- Picked the project name. Earlier candidates were taken or too close to existing names, so I checked
  crates.io and GitHub and settled on "Proacho".

**Who wrote what**
- Me: ran `cargo init`, `cargo run`, `cargo fmt`, `cargo clippy` and `cargo test`. Made the commits, created
  the GitHub repo, fixed the remote and pushed. Chose the name and the project goals.
- Claude: `git init`, `.gitignore`, `LICENSE`, the first draft of `README.md` and this file. Explained the
  generated files and the name checks.

**What I learned** *(draft, edit to match what you actually remember)*
- A Cargo project has `Cargo.toml` (like `pom.xml` or `pyproject.toml`) and `src/main.rs` with `fn main()`.
  `println!` is a macro, not a function, which is why it ends in `!`.
- `cargo fmt` only changes how code looks. `cargo clippy` is a linter: it flags code that compiles but is
  probably wrong or unidiomatic. `cargo test` runs the tests (none yet).
- `Cargo.lock` is committed for applications, to make builds reproducible.
- Git: a commit message needs `-m "..."` in quotes, otherwise git reads the words as file names and the shell
  chokes on characters like `(`. Files must be staged with `git add` first.
- A commit is only local until there is a remote on GitHub and I `git push`. A remote URL is either SSH
  (`git@github.com:user/repo.git`) or HTTPS, never a mix of both, and `git remote set-url` fixes a wrong one.
