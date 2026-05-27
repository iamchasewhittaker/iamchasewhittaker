# Conventions for Claude sessions

Chase is **new to git/GitHub**. When guiding him:

- Explain in **plain, beginner language with analogies** (git = video-game save points,
  GitHub = the cloud save, etc.). Give a short primer up front, then re-explain each
  concept the moment it's first used.
- **Learn-by-doing:** give the exact copy-paste command plus a one-line "what this does
  and why," then let Chase run it and paste the output back to decode together.
- Keep a **learning log** (glossary + dated journal + cheat-sheet) — its permanent home
  is Chase's private Obsidian notes vault (a separate private repo), not this repo.

## Workflow rules (see WORKFLOW.md for the full runbook)

- **GitHub is the source of truth — never a laptop.**
- **Hybrid, cloud-first:** web/TypeScript projects in cloud sessions; iOS/Swift local
  in Xcode under `~/Developer`.
- **Secrets live in 1Password**, never in git. Every repo gitignores `.env*`
  (use `.gitignore.template`).
- Local code root is `~/Developer` — never `~/Documents`/`~/Desktop` (iCloud sync
  breaks build folders).
