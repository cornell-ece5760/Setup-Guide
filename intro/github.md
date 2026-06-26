# Git & GitHub Overview

Git is an extremely popular tool for software version control. Its primary purpose is to track your work — as you make incremental changes to files, you can always revert to, compare, or recombine old versions. When combined with a remote repository (GitHub), it gives you an online backup of your work and makes collaboration far easier than emailing files back and forth.

In ECE 5760, Git is how the staff tracks your progress and how your group shares code. **Keep your private repo up to date.**

> Publishing your code to a public repository is an academic integrity violation.

---

## Table of Contents

1. [Installing Git](#installing-git)
2. [Setting Up GitHub](#setting-up-github)
3. [How Git Works — The Mental Model](#how-git-works--the-mental-model)
4. [Cloning Your Repository](#cloning-your-repository)
5. [Core Workflow: Stage → Commit → Push → Pull](#core-workflow-stage--commit--push--pull)
6. [Checking Status and History](#checking-status-and-history)
7. [Branching](#branching)
8. [Merging and Resolving Conflicts](#merging-and-resolving-conflicts)
9. [Forking](#forking)
10. [Pulling from Upstream](#pulling-from-upstream)
11. [Rewinding History](#rewinding-history)
12. [Quick Reference](#quick-reference)

---

## Installing Git

If you do not have Git installed, download it from the [official website](https://git-scm.com/). Verify your installation:

```bash
git --version
```

---

## Setting Up GitHub

### Create / Log Into Your GitHub Account

Go to [github.com](https://github.com) and log in (or create an account). Your private course repo will be created for you by the staff — you do not need to create one yourself.

### Set Up SSH Credentials

SSH lets you push and pull without typing a password every time.

**1. Generate an SSH key** (skip if you already have one at `~/.ssh/id_rsa.pub` or `~/.ssh/id_ed25519.pub`):

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Press Enter through the prompts (optionally set a passphrase).

**2. Copy your public key:**

```bash
cat ~/.ssh/id_ed25519.pub
```

**3. Add it to GitHub:** go to **Settings → SSH and GPG Keys → New SSH key**, paste the key, and save.

**4. Test your connection:**

```bash
ssh -T git@github.com
```

You should see a greeting with your username.

---

## How Git Works — The Mental Model

Understanding the four "zones" prevents most confusion:

```
┌─────────────────┐    git add     ┌──────────────┐
│  Working Tree   │ ─────────────► │ Staging Area │
│ (files on disk) │                │  (index)     │
└─────────────────┘                └──────┬───────┘
        ▲                                 │ git commit
        │ git checkout                    ▼
        │                        ┌──────────────────┐
        │                        │  Local Repo      │
        │                        │  (.git folder)   │
        │                        └────────┬─────────┘
        │                                 │ git push
        │                                 ▼
        │                        ┌──────────────────┐
        └──────── git pull ───── │  Remote Repo     │
                                 │  (GitHub)        │
                                 └──────────────────┘
```

- **Working tree** — the files you actually edit
- **Staging area** — a holding zone for changes you plan to commit
- **Local repo** — your full commit history, stored in the hidden `.git/` folder
- **Remote repo** — the copy on GitHub's servers

---

## Cloning Your Repository

Cloning downloads the remote repository to your machine. Find the **Code** button on your GitHub repo page, select **SSH**, and copy the URL.

```bash
git clone git@github.com:your-org/your-repo.git
cd your-repo
```

> If you get authentication errors, your SSH key isn't linked to your GitHub account yet — revisit the [SSH setup](#set-up-ssh-credentials) above.

---

## Core Workflow: Stage → Commit → Push → Pull

### `git pull` — Start here

Always pull before you start working to get the latest changes from your teammates:

```bash
git pull
```

### `git add` — Stage your changes

After editing files, stage the ones you want to include in your next commit:

```bash
git add file.txt           # stage one file
git add src/               # stage a whole directory
git add -p                 # interactively pick chunks within files
```

> Avoid `git add .` or `git add -A` — these stage everything indiscriminately, including temporary files, build artifacts, and secrets.

### `git commit` — Save a snapshot

A commit is a permanent, labeled snapshot of your staged changes:

```bash
git commit -m "Describe what changed and why"
```

Good commit messages make it easy to find what you're looking for later. Prefer short, specific messages: `"Fix UART baud rate calculation"` over `"fix bug"`.

### `git push` — Send commits to GitHub

```bash
git push
```

This uploads your local commits to the remote. Without it, your changes exist only on your machine — if your laptop dies, they're gone.

### Typical session

```bash
git pull                          # sync before starting
# ... edit files ...
git status                        # see what changed
git add changed_file.v            # stage
git commit -m "Add PWM module"    # commit
git push                          # share
```

---

## Checking Status and History

### `git status`

The most useful command. Run it constantly:

```bash
git status
```

It shows:
- Files modified but not staged (red)
- Files staged but not committed (green)
- Untracked files Git doesn't know about yet

### `git diff`

See exactly what changed, line by line:

```bash
git diff              # unstaged changes vs. last commit
git diff --staged     # staged changes vs. last commit
git diff main..dev    # differences between two branches
```

### `git log`

Browse your commit history:

```bash
git log                        # full history
git log --oneline              # compact, one line per commit
git log --oneline --graph      # shows branching visually
git log --oneline -10          # last 10 commits
git log -- src/pwm.v           # history of one file
```

Each commit has a **hash** (e.g., `a3f9c12`) that uniquely identifies it. You'll use these when rewinding history.

---

## Branching

Branches let you develop a feature or experiment without touching the main working code. Think of the main branch as the "official" version and feature branches as sandboxes.

### View branches

```bash
git branch            # local branches (* = current)
git branch -a         # local + remote branches
```

### Create and switch to a new branch

```bash
git switch -c feature/vga-output    # create and switch
```

Or the older form:

```bash
git checkout -b feature/vga-output
```

### Switch between branches

```bash
git switch main
git switch feature/vga-output
```

> Your working tree updates to reflect the state of whichever branch you switch to. Make sure you've committed (or stashed) any changes before switching.

### Push a new branch to GitHub

```bash
git push -u origin feature/vga-output
```

The `-u` flag links your local branch to the remote one so future `git push` / `git pull` work without arguments.

### Delete a branch (after merging)

```bash
git branch -d feature/vga-output          # local
git push origin --delete feature/vga-output   # remote
```

---

## Merging and Resolving Conflicts

### Merge a feature branch into main

```bash
git switch main
git pull                             # make sure main is up to date
git merge feature/vga-output
git push
```

### Resolving conflicts

If two people edited the same lines, Git can't auto-merge and will mark conflicts in the file:

```
<<<<<<< HEAD
  your version of the line
=======
  teammate's version of the line
>>>>>>> feature/vga-output
```

Edit the file to keep the right content, remove the conflict markers, then:

```bash
git add the_file.v
git commit -m "Resolve merge conflict in vga module"
```

### Pull Requests (PRs)

For team projects, instead of merging locally it's often better to:

1. Push your feature branch
2. Open a **Pull Request** on GitHub
3. Have a teammate review it
4. Merge via the GitHub UI

PRs give you a review step and a clean record of what changed and why.

---

## Forking

A **fork** is your personal copy of someone else's repository. Forking is common when you want to contribute to a project you don't own.

1. Click **Fork** on the original repo's GitHub page
2. Clone your fork: `git clone git@github.com:you/repo.git`
3. Make changes on a branch, push to your fork
4. Open a **Pull Request** from your fork back to the original repo

In ECE 5760, you won't typically fork the course repo — your group will have its own private repo. But forking is useful if you want to contribute to open-source libraries or reference projects.

---

## Pulling from Upstream

When you fork a repo, the original is called **upstream**. To keep your fork in sync:

```bash
# One-time setup: add the upstream remote
git remote add upstream git@github.com:original-owner/repo.git

# Verify your remotes
git remote -v

# Fetch and merge upstream changes into your local branch
git fetch upstream
git switch main
git merge upstream/main

# Push the updated main to your fork on GitHub
git push origin main
```

This pattern also applies in ECE 5760 if the staff pushes updates to a shared starter repo.

---

## Rewinding History

### Stash — temporarily shelve changes

If you need to switch branches but aren't ready to commit:

```bash
git stash           # shelve all uncommitted changes
git stash pop       # restore them later
git stash list      # see all stashes
```

### Reset — undo commits locally

`git reset` moves the branch pointer backward. There are three modes:

| Mode | Commits | Staging area | Working tree |
|---|---|---|---|
| `--soft` | Undone | Kept staged | Unchanged |
| `--mixed` (default) | Undone | Cleared | Unchanged |
| `--hard` | Undone | Cleared | **Reverted** |

```bash
git reset HEAD~1          # undo last commit, keep files as-is
git reset --soft HEAD~2   # undo 2 commits, keep changes staged
git reset --hard HEAD~1   # undo last commit AND discard file changes
```

> `--hard` destroys uncommitted work permanently. Use with caution.

### Revert — safely undo a published commit

If you've already pushed a commit and want to undo it, **don't reset** (it rewrites history that others may have). Instead, create a new commit that undoes the change:

```bash
git revert a3f9c12        # creates an "undo" commit for that hash
git push
```

### Restore a single file

To discard changes to one file and go back to the last committed version:

```bash
git restore src/broken.v
```

### Checkout an old version to look at it

```bash
git checkout a3f9c12      # detached HEAD — read-only look at old commit
git switch main           # go back to normal
```

---

## Quick Reference

| Command | What it does |
|---|---|
| `git status` | Show changed/staged/untracked files |
| `git diff` | Show unstaged line-by-line changes |
| `git diff --staged` | Show staged changes |
| `git log --oneline --graph` | Visual commit history |
| `git add <file>` | Stage a file |
| `git commit -m "msg"` | Commit staged changes |
| `git push` | Upload commits to GitHub |
| `git pull` | Download and merge remote changes |
| `git switch -c <branch>` | Create and switch to a new branch |
| `git switch <branch>` | Switch to an existing branch |
| `git merge <branch>` | Merge a branch into the current one |
| `git stash` / `git stash pop` | Shelve / restore uncommitted changes |
| `git reset HEAD~1` | Undo last commit, keep file changes |
| `git reset --hard HEAD~1` | Undo last commit, discard file changes |
| `git revert <hash>` | Create a new commit that undoes an old one |
| `git restore <file>` | Discard working-tree changes to a file |
| `git remote -v` | Show configured remotes |
| `git fetch upstream` | Download upstream changes without merging |

---

> Most of the time, `add`, `commit`, `push`, and `pull` are all you need. Don't worry about mastering everything at once — you'll pick up the rest as you go.

---

*Adapted from [Cornell CS 3410, "Git," Fall 2025](https://www.cs.cornell.edu/courses/cs3410/2025fa/rsrc/git.html)*
