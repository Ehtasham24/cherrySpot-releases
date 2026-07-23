<div align="center">

# Cherry Spot

**A desktop Git client built around the one thing most Git GUIs treat as an afterthought: cherry-picking.**

[![Latest release](https://img.shields.io/github/v/release/Ehtasham24/cherrySpot-releases?label=latest&color=2ea44f)](https://github.com/Ehtasham24/cherrySpot-releases/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/Ehtasham24/cherrySpot-releases/total?color=blue)](https://github.com/Ehtasham24/cherrySpot-releases/releases)
[![Platform](https://img.shields.io/badge/platform-Windows-0078D6)](#download)
[![Auto-updates](https://img.shields.io/badge/updates-automatic-6f42c1)](#staying-up-to-date)

[Download](#download) · [What it does](#what-it-actually-does) · [FAQ](#faq)

</div>

---

## Why this exists

Most Git GUIs are built for "commit, push, pull" and treat everything else — cherry-picking a hotfix across three release branches, resolving a conflict without leaving your editor, remembering which task ID a commit belongs to — as a second-class flow you drop into a terminal for anyway.

Cherry Spot flips that. It's built around the workflows that actually eat your time: moving commits between branches, resolving conflicts fast, and keeping history clean — with a terminal-level understanding of what's happening under the hood, but without needing to hold ten `git` flags in your head.

## Download

Grab the installer from **[Releases](https://github.com/Ehtasham24/cherrySpot-releases/releases/latest)**:

| File | Use this if… |
|---|---|
| `cherry-spot_*_x64-setup.exe` | You want the standard installer (recommended) |
| `cherry-spot_*_x64_en-US.msi` | You need an MSI (scripted installs, IT-managed machines) |

Windows may show a SmartScreen prompt (see [FAQ](#faq)) — that's expected for a small internal tool, not a red flag.

## What it actually does

<details>
<summary><b>Cherry-pick commits across branches without the copy-hash-and-pray dance</b></summary>

<br>

The usual way: `git log`, copy a hash, `git checkout target-branch`, `git cherry-pick <hash>`, hit a conflict, resolve it by hand, `git add`, `git cherry-pick --continue`, repeat for every commit.

In Cherry Spot: search or browse to the commits you want (even across branches), select them, pick a target branch, and go. Multiple commits queue and apply in order automatically. Hit a conflict and Cherry Spot shows you exactly which files, with **Accept ours / Accept theirs** one-click resolution or **Open in editor** for anything trickier.

Resolve it and save the file — Cherry Spot notices on its own and continues the operation. No `git status`, no `--continue`, no forgetting which commit you were mid-pick on.

</details>

<details>
<summary><b>Switch branches without losing your uncommitted work</b></summary>

<br>

The usual way: `git checkout other-branch` → `error: Your local changes would be overwritten` → stash, switch, hope you remember to pop it, sometimes on the wrong branch.

In Cherry Spot: pick a branch with uncommitted changes still sitting in your working tree, and it asks — **bring your changes with you**, or **leave them behind** — GitHub-Desktop style. Either way it's one click, and it won't quietly leave a stash you forget about three days later.

</details>

<details>
<summary><b>Commit messages that actually match your team's task-ID convention</b></summary>

<br>

If your team commits against a ticket/task ID format, Cherry Spot enforces it at commit time — with autocomplete from task IDs you've used recently **in that specific repo**, so you're not retyping or copy-pasting IDs between commits on the same piece of work.

</details>

<details>
<summary><b>Find the commit you're thinking of, fast</b></summary>

<br>

Search by task ID, commit message, author, or a date range — scoped to the current branch or across all of them. No memorizing `git log --grep` syntax or piping through `grep` yourself.

</details>

<details>
<summary><b>A global hotkey that beats alt-tabbing through ten windows</b></summary>

<br>

You're heads-down in your editor, made a fix, and want to commit + push without hunting for the right window. Configurable hotkeys — fully rebindable, or clearable if you'd rather not have any — bring Cherry Spot to the front and let you quick-commit or push/pull from anywhere.

</details>

<details>
<summary><b>Push and pull that don't leave you guessing</b></summary>

<br>

Real-time ahead/behind counts, one-click push, and pulls that walk you through conflicts the same way cherry-picks do — resolve in your editor, save, and Cherry Spot picks up the resolution automatically instead of leaving half your files in "Changes" and half in history.

</details>

<details>
<summary><b>GitHub and GitLab sign-in — no PAT copy-pasting</b></summary>

<br>

Sign in with a browser flow for either GitHub or GitLab. No generating a personal access token and pasting it into a text field you'll lose track of.

</details>

<details>
<summary><b>Built to look at all day</b></summary>

<br>

Four dark levels and four light levels, adjustable split panes, and a layout that keeps file paths and diffs readable instead of cramped. Pick what's easy on your eyes at 2 AM and what works for a bright office.

</details>

## Staying up to date

Cherry Spot checks for new versions on startup and shows an **"Update & Restart"** banner when one's available — download and relaunch happen automatically, no manual reinstall. You only ever do this download-and-run step once, on your very first install.

## FAQ

**"Windows protected your PC" / SmartScreen warning?**
Expected — the installer isn't signed with a paid Windows publisher certificate (this is an internal tool, not a commercial app). Click **More info → Run anyway**.

**Where's the source code?**
In a separate, private repository. This repo exists specifically so you can grab a build without needing source access — nothing here except compiled installers and update manifests.

**Something's broken / a feature request?**
Reach out directly — issues aren't monitored on this repo since it's release-artifacts-only.
