# Handoff — continue the GitHub-first setup

Paste the prompt below into Claude Code on the Mac to continue the GitHub-first
cutover, vault recovery, and project audit. See `WORKFLOW.md` in this repo for the
full runbook and exact audit commands.

## Heads-up: two "Developer" folders (don't confuse them)

- `/Users/chasewhittaker/Users/chase/Developer` — **restored backup** of the old
  machine, from Backblaze. *Evidence/staging only*: used to verify GitHub has
  everything and to recover local-only files. **Never work from it.**
- `/Users/chasewhittaker/Developer` (= `~/Developer`) — **real working folder** on this
  Mac. Verified repos get freshly cloned here from GitHub.

---

## The prompt (copy everything below)

~~~
I'm Chase — new to git & GitHub, so teach me like a 5th grader: plain language and
analogies (git = video-game save points; GitHub = the cloud those saves upload to).
Short primer when you introduce a concept, then re-explain it just-in-time as we use it.
Work style = learn-by-doing: give me the exact command + a one-line "what this does and
why," let me run it, and we decode the output together. Keep a running learning log
(glossary of every new term + a dated journal of what we did and why + a daily
cheat-sheet); its permanent home will be my private Obsidian vault once it's recovered.

WHERE THINGS STAND
- You (Claude Code) are installed and logged in on my Mac (Claude Max, Opus 4.7),
  running in my home folder /Users/chasewhittaker. That's fine for this setup since the
  work spans my home folder; going forward I'll cd into a project first.
- My main MacBook is at Apple for a battery swap. I'm on my wife's MacBook Pro under a
  NEW macOS account (username "chasewhittaker", home /Users/chasewhittaker).
- Goal: go GitHub-first — "GitHub is the source of truth, never a laptop."

BACKBLAZE RESTORE (still downloading right now)
- A Backblaze restore of my OLD machine is in progress. It lands at:
      /Users/chasewhittaker/Users/chase/...
  (My old account was "chase", home /Users/chase, so the restore recreates that old
  structure nested inside my new home.) My old code folder will be at:
      /Users/chasewhittaker/Users/chase/Developer
- Treat the whole /Users/chasewhittaker/Users/chase/ tree as STAGING / evidence ONLY —
  it's for verifying GitHub has everything and recovering local-only files. I do NOT
  work from it.
- My real working folder is ~/Developer (= /Users/chasewhittaker/Developer), where
  verified repos get freshly cloned from GitHub.

DECISIONS ALREADY MADE (don't re-litigate)
- Hybrid, cloud-first: web/TS projects (shipyard-os, moving-the-needle, clarityos-money)
  in Claude Code on the web; iOS/Swift (unnamed-ios) local in Xcode.
- Local code root: ~/Developer (never ~/Documents or ~/Desktop — iCloud breaks builds).
- Secrets: master copies in 1Password; each repo's .env gitignored and recreatable from
  1Password / Vercel / Supabase.
- Verify everything is on GitHub by comparing against the Backblaze restore BEFORE
  trusting it.
- I have an existing PRIVATE Obsidian vault to recover from the restore; decide how to
  sync Obsidian<->GitHub only AFTER inspecting how it was set up.

ALREADY DONE
- New macOS account; Xcode + Homebrew installed; Claude Code installed + logged in.
- Keyboard (Microsoft Sculpt): swapped Command/Option; Wispr Flow on Caps Lock (->Fn).
- Committed to my profile repo iamchasewhittaker/iamchasewhittaker on branch
  claude/peaceful-einstein-kiuQf: WORKFLOW.md (master runbook), .gitignore.template,
  CLAUDE.md. Read WORKFLOW.md if you can — it has the exact audit commands.

WHAT TO DO NOW (restore isn't finished, so start with the parts that don't need it)
1. Check what's installed and install what's missing: git, Node, gh (GitHub CLI),
   1Password, Obsidian. Sign me into GitHub (gh auth login or an SSH key).
2. Set my git identity: name "Chase Whittaker", email chase.t.whittaker@gmail.com.
3. Create my working folder: ~/Developer.
Teach me each step and let me run the commands.

THEN, once the restore at /Users/chasewhittaker/Users/chase/ has finished:
4. Audit each project in the restore: confirm it's fully on GitHub (git status /
   unpushed commits / remote), push anything missing, and find local-only files by
   diffing against a fresh clone.
5. Recover my Obsidian vault (search the /Users/chasewhittaker/Users/chase/ tree for a
   folder containing a .obsidian folder); inspect how it was synced; create a NEW
   private GitHub repo for it; decide the Obsidian Git setup; start the learning log in it.
6. Fresh-clone each verified repo into ~/Developer; recreate each .env from 1Password.
7. Load all secrets/keys (including the Apple .p8 signing key) into 1Password.

Begin with step 1 now. Also show me how to tell when the Backblaze restore has finished
before we rely on it.
~~~
