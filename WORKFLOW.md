# My GitHub-First Workflow

This is my personal runbook for working from GitHub instead of from one specific
laptop. If I'm ever on a new/borrowed machine, I follow this top to bottom.

**The one rule:** *GitHub is the source of truth — never a laptop.* Any computer is
just a temporary window into my code. If I lose the laptop, I lose nothing.

---

## Tiny glossary (plain language)

- **git** — like *save points in a video game*. You make a save point whenever you
  reach a good spot.
- **GitHub** — *the cloud* those save points upload to, so they're safe and you can
  load them on any machine.
- **repo** (repository) — *one project's save folder*.
- **commit** — *making a save point* (with a short note about what changed).
- **push** — *uploading* your save points to GitHub.
- **pull** — *downloading* the latest save points from GitHub.
- **clone** — *making a fresh copy* of a GitHub repo onto a computer.
- **branch** — *a parallel save file* where you can experiment without touching the
  main one.
- **`.gitignore`** — a list of files git should *ignore* (never upload), like secrets
  and giant build folders.

---

## How I work (hybrid, cloud-first)

- **Web/TypeScript projects** (`shipyard-os`, `moving-the-needle`, `clarityos-money`):
  work in **Claude Code on the web** (cloud sessions). Nothing lives on a laptop.
- **iOS / Swift** (`unnamed-ios`): must be **local in Xcode**. Clone into `~/Developer`,
  commit + push often.
- **Every session:** start with `git pull` (get the latest), end with commit + push
  (save my work to the cloud).

---

## Setting up a Mac from scratch

1. **My own macOS user account** (don't work inside someone else's). Sign in with my
   own Apple ID / iCloud.
2. **Code folder:** `mkdir ~/Developer` — one folder per project, named like the repo.
   - ⚠️ Never keep code in `~/Documents` or `~/Desktop`: iCloud tries to sync
     `node_modules`/`.git`/build files and breaks things. `~/Developer` is safe.
3. **Install:** Xcode, Node (via `nvm` or Homebrew), git, GitHub sign-in
   (`gh auth login` or an SSH key), 1Password, Obsidian, Claude Code.
4. **Tell git who I am:**
   ```bash
   git config --global user.name "Chase Whittaker"
   git config --global user.email "chase.t.whittaker@gmail.com"
   ```

---

## Checking GitHub really has everything (the audit)

When restoring from a backup (e.g. Backblaze), extract it to **one staging folder**
`~/backblaze-restore/` (NOT the original paths). Then for each project folder:

```bash
cd ~/backblaze-restore/<project>
git status                                     # any uncommitted/untracked files?
git log --branches --not --remotes --oneline   # any commits never pushed?
git stash list                                 # any stashed work?
git remote -v                                  # does it point at my GitHub repo?
```

- All quiet + remote set → ✅ it's fully on GitHub.
- Unpushed/uncommitted work → ⚠️ `git push` it.
- No remote / no `.git` folder → ❌ it was never on GitHub; create a repo and push it.

Find files that only existed locally (assets, notes, `.env`) by comparing to a fresh
copy from GitHub:
```bash
cd /tmp && git clone <repo-url> <project>-fresh
diff -rq ~/backblaze-restore/<project> /tmp/<project>-fresh | grep -v '\.git'
```
Anything listed as only-in-backup is local-only — decide where it belongs (see table).

Once a project is ✅, get my **working copy fresh from GitHub**, not from the backup:
```bash
cd ~/Developer && git clone <repo-url>
```

---

## Secrets / API keys → 1Password

- Secrets **never** go in git. Every repo's `.gitignore` includes `.env*`.
- **Master copies of all keys live in 1Password** — including the Apple `.p8` push key
  and any `.mobileprovision` (these can't be casually regenerated).
- A repo's `.env` file is always **reproducible** from 1Password or the provider
  dashboard (Vercel / Supabase), so losing it is no big deal.
- Find leftover secrets in a backup:
  ```bash
  cd ~/backblaze-restore
  find . -name '.env*' -not -path '*/node_modules/*'
  find . \( -name '*.pem' -o -name '*.key' -o -name '*.p8' -o -name '*.mobileprovision' \) -not -path '*/node_modules/*'
  ```
- Cloud sessions get secrets via the environment's config, not a checked-in file:
  https://code.claude.com/docs/en/claude-code-on-the-web

---

## What goes where

| Goes IN GitHub | Stays OUT of git (lives in…) |
|---|---|
| Source code, configs, schema/migrations | Secrets / `.env` / signing keys → **1Password** |
| Docs, READMEs, small notes | Large media / design / video → **cloud storage or Git LFS** |
| Lockfiles (`package-lock`, etc.) | Datasets / DB dumps → **cloud storage** |
| Small static assets (icons, logos) | `node_modules`, `.next/`, `DerivedData/`, caches → **gitignored** |
| `.gitignore`, CI workflows | — |

My Obsidian notes vault is its **own private repo**. Backblaze stays on as a backup of
`~/Developer` + the vault + a 1Password export.

---

## Daily cheat-sheet

```bash
git pull                      # start of session: get the latest from GitHub
# ... do work ...
git status                    # see what changed
git add -A                    # stage all my changes
git commit -m "what I did"    # make a save point
git push                      # upload it to GitHub (end of session)
```
