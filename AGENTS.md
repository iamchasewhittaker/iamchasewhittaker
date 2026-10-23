<!-- Shared rules v2 · source: github.com/iamchasewhittaker/project-template -->
## Shared rules (Claude, Grok, Cursor, any agent)

Every agent works from the files in this repo. GitHub is the shared view.

1. **Before you start:** read [HANDOFF.md](HANDOFF.md) and run `gh pr list --state open`. Open draft PRs are work in progress by another agent.
2. **When you start:** this repo's own git rules come first (later in this file, if any). Within them:
   - **If you may push:** push a branch (Grok uses `grok/*` when this repo says so) and open a draft PR right away. Its description says who you are (Claude, Grok, Cursor), the task, and the plan.
   - **If you may not run git or push here:** add a line under `## In flight` in HANDOFF.md: `- YYYY-MM-DD <agent>: <task>`. Whoever commits next (for example `/sync-end`) pushes it. Remove the line when the work lands.
3. **When you finish:** update [HANDOFF.md](HANDOFF.md) in that same PR or commit. If you push straight to main, update HANDOFF.md in that push.
4. **Never commit** secrets (`.env`, tokens, keys; those live in 1Password), money figures, account numbers, contact info, or salary numbers.
5. Dated decisions go in [docs/decisions.md](docs/decisions.md). Pasted Claude artifact code goes in [artifacts/](artifacts/).
<!-- end Shared rules v2 -->

# Project notes

Profile README repo
