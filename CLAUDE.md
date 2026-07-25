# CLAUDE.md — merely-made.github Repository

This is the special `.github` repo for the Merely Made GitHub org: it holds
only `profile/README.md`, rendered as the org profile page. No build, no
source tree beyond that one file.

## Workspace Tooling: sem & weave

Two non-authoritative structural tools from Ataraxy Labs are wired into this
repo (mainly relevant to `*.md` here). Both read code structure via
tree-sitter, not program semantics.

**weave** (entity-level git merge driver). `.gitattributes` maps ~46 file
types, including `*.md`, to `merge=weave`; ordinary `git merge` resolves
false conflicts where independent edits touch different sections of the
same file. The merge-driver binary path is machine-local, not committed. It
is wired via `git config --global merge.weave.driver` on this machine,
which covers every repo including fresh clones, so no per-repo setup is
needed here. On a new machine, install with `cargo install --git
https://github.com/Ataraxy-Labs/weave weave-cli weave-driver`, then either
repeat the global `git config --global merge.weave.*` setup or run `weave
setup` in each repo.

**sem** (semantic version control): entity-level diff/context queries on
top of Git. Installed via `cargo install --git
https://github.com/Ataraxy-Labs/sem sem-cli` and registered as a
user-scoped Claude Code MCP server (`sem_diff`, `sem_context`, `sem_impact`,
`sem_entities`, `sem_blame`, `sem_log`; call these directly as tools). CLI
fallback: `sem diff --format plain`.
