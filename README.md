<div align="center">

<img src="assets/cherry-spot-logo.png" alt="Cherry Spot" width="96" height="96" />

# Cherry Spot

**A desktop Git client built around the one thing most Git GUIs treat as an afterthought: cherry-picking.**

[![Latest release](https://img.shields.io/github/v/release/Ehtasham24/cherrySpot-releases?label=latest&color=2ea44f)](https://github.com/Ehtasham24/cherrySpot-releases/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/Ehtasham24/cherrySpot-releases/total?color=blue)](https://github.com/Ehtasham24/cherrySpot-releases/releases)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux-0078D6)](#download)
[![Auto-updates](https://img.shields.io/badge/updates-automatic-6f42c1)](#staying-up-to-date)

[Download](#download) · [Getting started](#getting-started) · [Features](#features) · [FAQ](#faq) · [Bugs & feature requests](#bugs--feature-requests)

</div>

---

## What Cherry Spot is

Cherry Spot is a desktop Git client built for one recurring workflow: moving commits between branches — cherry-picking a fix from `dev` up to `staging`, then up to `live`, opening a pull request automatically wherever one's required — without living in a terminal or a browser to get it done.

It exists because most Git GUIs are built for "commit, push, pull" and treat everything else — cherry-picking across branches, resolving a conflict, remembering which task ID a commit belongs to, opening the PR a protected branch demands — as a second-class flow you drop out of the app for anyway. Cherry Spot builds each of those directly into the UI instead.

**Where it fits:** Cherry Spot isn't trying to be a complete general-purpose Git GUI replacement. Cross-branch cherry-picking, conflict resolution, task-ID search, and PR/MR automation get the deepest attention here; a few things power users expect from a full-featured client — an interactive rebase editor, a dedicated visual 3-way merge tool — aren't built in (yet). Keep a general client around for those if you need them; use Cherry Spot for the workflow it's actually built for.

## Download

Grab the installer from **[Releases](https://github.com/Ehtasham24/cherrySpot-releases/releases/latest)**:

**Windows**

| File | Use this if… |
|---|---|
| `cherry-spot_*_x64-setup.exe` | You want the standard installer (recommended) |
| `cherry-spot_*_x64_en-US.msi` | You need an MSI (scripted installs, IT-managed machines) |

Windows may show a SmartScreen prompt on first run — that's expected for a small internal tool without a paid publisher certificate, not a red flag. Click **More info → Run anyway**.

**Linux**

| File | Use this if… |
|---|---|
| `cherry-spot_*_amd64.deb` | Debian, Ubuntu, or a derivative |
| `cherry-spot-*.x86_64.rpm` | Fedora, RHEL, or a derivative |
| `cherry-spot_*_amd64.AppImage` | Any other distro — no install step, just `chmod +x` and run it |

macOS support is in progress — code-signing/notarization setup isn't finished yet, so there's no `.dmg` build here until that's done.

## Getting started

### 1. Sign in

Open Cherry Spot and sign in with GitHub or GitLab from the top right. This is a browser-based OAuth flow — no personal access token to generate or paste in. GitLab sign-in also works against self-managed instances, not just gitlab.com.

### 2. Add a repository

Use whichever fits:
- **Clone** — paste a repo URL.
- **Browse your repos** — pick one straight from a list of everything your signed-in account has access to.
- **Open existing** — point Cherry Spot at a repo already on disk.

A "Current repository" dropdown, top left, keeps recently opened repos one click away after that.

### 3. The core workflow

1. **Pick a branch, then search.** Enter a task ID, keyword, or paste a commit hash directly; results come from the commit history of the current branch, a specific branch, or every branch at once (toggle **All branches**). Search updates as you type — no Enter needed.
2. **Select commits, choose a target branch (or several), and cherry-pick.** Before anything runs, Cherry Spot shows exactly what's about to happen to each target — a direct commit, or a pull/merge request if that branch requires one. Prefer to see the shape of a branch's history first? Switch **History** to **Graph** view to see how commits and merges actually connect.
3. **Resolve conflicts in place, if any come up.** Use **Accept Current** / **Accept Incoming** for a quick resolution, **Accept Both** to keep both sides' content instead of picking one, **Keep** / **Delete** when a file was added or removed on one side, or **Open in editor** to fix the file yourself and save — Cherry Spot detects the save and continues automatically.
4. **Push.** One button in the header, always visible. It checks the remote first, so a push that would've been rejected opens a Pull prompt instead of failing outright.

### 4. Where things live

- **Header** — Fetch origin, Pull, Push, **Compare** (diff any two branches), and **Task Status** (check which branches have a given task ID's commits, and which are still missing them).
- **Settings** (gear icon, top right) — sign-in/account, keyboard shortcuts, theme, Recent Activity (your own commit feed across GitHub + GitLab, over a From/To date range you pick), and Branch Rules.
- **Tray icon + global hotkey** (Ctrl+Shift+F by default, rebindable in Settings) — show or hide the whole app from anywhere, without alt-tabbing to find it.

### Staying up to date

Cherry Spot checks for new versions on startup and shows an **"Update & Restart"** banner when one's available. Download, install, and relaunch happen in one click — no manual reinstall. The download-and-run step above is a one-time thing, for your very first install only.

## Features

<details>
<summary><b>Cherry-pick commits across branches without the copy-hash-and-pray dance</b></summary>

<br>

The usual way: `git log`, copy a hash, `git checkout target-branch`, `git cherry-pick <hash>`, hit a conflict, resolve it by hand, `git add`, `git cherry-pick --continue`, repeat for every commit.

In Cherry Spot: search or browse to the commits you want (even across branches), select them, pick a target branch, and go. Multiple commits queue and apply in order automatically. Hit a conflict and Cherry Spot shows you exactly which files, with **Accept Current / Accept Incoming** one-click resolution (labeled correctly whether it's a cherry-pick, merge, or rebase — "current" and "incoming" don't mean the same thing across all three), **Accept Both** when you actually want both sides' changes kept, **Keep / Delete** for files added or removed on one side, or **Open in editor** for anything trickier.

Resolve it and save the file — Cherry Spot notices on its own and continues the operation. No `git status`, no `--continue`, no forgetting which commit you were mid-pick on.

</details>

<details>
<summary><b>Send the same fix to several branches — and let Cherry Spot open the PR where one's required</b></summary>

<br>

The usual way: cherry-pick to `staging`, done. Then cherry-pick the *same* commits again for `live` — except `live` needs a reviewed pull request, so that's a second, entirely manual detour: create a branch by hand, cherry-pick onto it, push it, switch to the browser, open the PR, and write the title and description yourself.

In Cherry Spot: pick several target branches at once from the same selection. Branches that don't need review get the commits directly, same as a normal cherry-pick. Branches that do — because your team protects them on GitHub/GitLab, or flagged them in Branch Rules — get a disposable branch cut from that target's freshest `origin`, the same commits cherry-picked onto it, pushed, and a PR or MR opened automatically. You fill in one small dialog first (Fix/Feat/Chore/Task-Ticket, a task ID, a description) so the PR reads like a normal commit instead of an auto-generated placeholder, and one screen shows exactly what's about to happen to every branch before anything runs.

</details>

<details>
<summary><b>Won't let you accidentally push straight to a protected branch</b></summary>

<br>

Cherry Spot reads your repo's actual GitHub/GitLab branch protection, so if one teammate protects `live`, everyone else sees it protected the moment they open the same repo — nothing to sync by hand. Try to push straight to a branch like that and it stops you before the push even goes out, with a plain explanation instead of a confusing rejection from the remote.

</details>

<details>
<summary><b>Know exactly which branches have your fix — without asking around</b></summary>

<br>

Enter a task ID and see, at a glance, which branches have all of its commits, some, or none — down to the exact commits still missing on any given branch, with one click to cherry-pick the gap closed. Or compare any two branches directly to see what's actually different between them, grouped by task. Diffs show line numbers and are fully selectable, so copying a snippet out doesn't mean opening the file somewhere else first.

</details>

<details>
<summary><b>See how branches actually diverged, not just a flat list of commits</b></summary>

<br>

Switch the History tab to **Graph** view and get a colored lane graph — the same kind you'd get from the command line's `git log --graph`, without the command line. Forks, merges, and where a branch actually split off are visible at a glance instead of something you reconstruct in your head from hashes and badges. Hover any commit or line for the details behind it, and it stays in lockstep as you scroll through history.

</details>

<details>
<summary><b>Find a commit by its hash as fast as by its message</b></summary>

<br>

Paste a full or partial commit hash into search and Cherry Spot resolves it directly — no need to know which branch it's on first. Search runs as you type, with no Enter required, so results narrow down live instead of after a keypress-and-wait.

</details>

<details>
<summary><b>Migrate a whole module or folder from another branch, not just individual commits</b></summary>

<br>

Sometimes what needs to move isn't "the commits for task #X" — it's a whole module or folder mirrored exactly from another branch (or, over SSH, from a module living on a company server). **Migrate Module** does that: pick the source and the folder, browse its tree visually instead of typing a path, and Cherry Spot adds/updates/deletes files on your current branch to match it exactly — staged for review before anything's committed. Multi-select lets you migrate several modules in one action. A **Repository Type** setting in Settings (Odoo-style module folders vs. a plain conventional repo) tells it how your codebase is actually organized, so the tool matches your project instead of the other way around.

</details>

<details>
<summary><b>Stash changes without losing track of them</b></summary>

<br>

The usual way: `git stash`, forget what's in it three branches later, `git stash list`, squint at auto-generated messages to figure out which one you need.

In Cherry Spot: a dedicated **Stash** button on the Changes tab opens a GitHub-Desktop-style stash manager — create, apply, pop, or drop stashes, each with a per-file diff preview so you can see what's actually in one before you touch it. If applying or popping hits a conflict, it routes through the same conflict-resolution screen as everything else.

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

If your team commits against a ticket/task ID format, Cherry Spot enforces it at commit time — pick Fix, Feat, Chore, or Task/Ticket and it builds the message for you (a fully custom template for Task/Ticket commits), with autocomplete from task IDs you've used recently **in that specific repo**, so you're not retyping or copy-pasting IDs between commits on the same piece of work.

</details>

<details>
<summary><b>A few extra safety nets for when something needs undoing</b></summary>

<br>

Amend your last commit's message without leaving the Changes tab, browse any file's full history or see who last touched each line, and — if a reset or rebase went further than intended — browse the reflog and restore to any prior state. All from the same window, no terminal required.

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

Sign in with a browser flow for either GitHub or GitLab. No generating a personal access token and pasting it into a text field you'll lose track of. If something else in your workflow still needs a GitLab personal access token, Settings has a page for that too — see your existing tokens with an expiring-soon warning, and generate a new one via GitLab's own API without leaving the app.

</details>

<details>
<summary><b>Built to look at all day</b></summary>

<br>

Four dark levels and four light levels, adjustable split panes, and a layout that keeps file paths and diffs readable instead of cramped. Pick what's easy on your eyes at 2 AM and what works for a bright office.

</details>

## FAQ

**"Windows protected your PC" / SmartScreen warning?**
Expected — the installer isn't signed with a paid Windows publisher certificate (this is an internal tool, not a commercial app). Click **More info → Run anyway**.

**AppImage won't run on Linux?**
It needs the executable bit set first: `chmod +x cherry-spot_*.AppImage`, then run it directly (`./cherry-spot_*.AppImage`).

**Where's the source code?**
In a separate, private repository. This repo exists specifically so you can grab a build without needing source access — nothing here except compiled installers and update manifests.

**Do I need to reinstall for every update?**
No — after the first install, Cherry Spot updates itself in place (see [Staying up to date](#staying-up-to-date)).

## Bugs & feature requests

Found something broken, or want a feature added? [**Open an issue**](https://github.com/Ehtasham24/cherrySpot-releases/issues/new) — include what you were doing, what you expected, and what happened instead (a screenshot helps). Feature requests are just as welcome as bug reports.
