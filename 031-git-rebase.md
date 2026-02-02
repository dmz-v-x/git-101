## Git Rebase & Interactive Rebase — Complete Guide

> Rebasing is one of the most powerful yet misunderstood features in Git.  
> It helps you rewrite, reorganize, and clean your commit history — making it linear, readable, and professional.

---

### 1. What Is Git Rebase?

`git rebase` is a command used to **move or reapply commits** from one branch onto another.  
It helps maintain a **clean, linear commit history** instead of merge commits.

### Basic Idea

> "Take my commits and replay them on top of another branch."

---

### Example:

Let’s say your branch history looks like this:

```
main:    A --- B --- C
feature:        \--- D --- E
```

When you run:
```bash
git rebase main
```

Git takes commits `D` and `E`, and **reapplies** them on top of `C`:

```
main:    A --- B --- C
feature:              \--- D' --- E'
```

Notice that commits `D'` and `E'` are **new commits** — rebasing rewrites history.

---

### 2. When To Use Rebase

✅ Use rebase when you want to:
- Clean up commit history before merging
- Update your feature branch with the latest main branch changes
- Avoid unnecessary merge commits
- Combine small commits into a single, meaningful one

❌ Avoid rebasing:
- On **shared branches** where others are also working — it rewrites commit history and causes confusion.

---

### 3. Rebase vs Merge

| Action | Command | Result | History |
|---------|----------|---------|----------|
| Merge | `git merge main` | Creates a merge commit | Non-linear |
| Rebase | `git rebase main` | Reapplies commits on top | Linear & clean |

### Example

```
# Merge
A -- B -- C (main)
      \
       D -- E -- F (feature)
       |
       G (merge commit)
```

```
# Rebase
A -- B -- C (main)
             \
              D' -- E' -- F' (feature)
```

---

### 4. Basic Rebase Workflow

### Scenario:
You’re working on a feature branch that’s behind main.

1. Fetch the latest main branch:
   ```bash
   git fetch origin
   ```

2. Switch to your feature branch:
   ```bash
   git checkout feature
   ```

3. Rebase your branch on top of the updated main:
   ```bash
   git rebase origin/main
   ```

4. If conflicts occur:
   ```bash
   git status
   # Fix conflicts manually
   git add <fixed-files>
   git rebase --continue
   ```

5. If you need to stop:
   ```bash
   git rebase --abort
   ```

6. Once done:
   ```bash
   git push origin feature --force-with-lease
   ```

---

### 5. Interactive Rebase (`git rebase -i`)

Interactive rebase gives you full control over your commit history.

```bash
git rebase -i HEAD~n
```

- `HEAD` → the latest commit
- `HEAD~n` → “n commits before HEAD”
- Example: `git rebase -i HEAD~5` lets you interactively rebase the last 5 commits.

---

### Inside the Interactive Rebase Editor

When you run `git rebase -i HEAD~3`, Git opens a text editor like this:

```
pick 123abc Commit message 1
pick 456def Commit message 2
pick 789ghi Commit message 3
```

You can now replace `pick` with any of the following commands:

| Command | Meaning |
|----------|----------|
| `pick` | Keep the commit as is |
| `reword` | Change the commit message |
| `edit` | Pause and modify the commit content |
| `squash` | Combine this commit with the previous one (keep both messages) |
| `fixup` | Combine with previous commit (discard this commit’s message) |
| `drop` | Delete this commit entirely |

---

### Example: Combining Commits

```
pick 123abc Added user model
squash 456def Fixed user model bug
squash 789ghi Updated tests for user model
```

When you save and exit, Git combines all three into one single commit.

---

### 6. Editing a Commit During Rebase

To modify an old commit:

1. Start an interactive rebase:
   ```bash
   git rebase -i HEAD~3
   ```

2. Change the command from `pick` to `edit` on the commit you want to modify.

3. Git pauses the rebase. Make your changes.

4. Stage them:
   ```bash
   git add .
   ```

5. Amend the commit:
   ```bash
   git commit --amend
   ```

6. Continue the rebase:
   ```bash
   git rebase --continue
   ```

---

### 7. Reordering Commits

Simply change the **order of lines** in the interactive editor to reorder commits.

Example:

```
pick 123abc Commit A
pick 456def Commit B
pick 789ghi Commit C
```

Swap lines to change order:
```
pick 789ghi Commit C
pick 123abc Commit A
pick 456def Commit B
```

Git will replay them in that order.

---

### 8. Fixing Mistakes During Rebase

If something goes wrong:
- **Abort rebase and return to original state:**
  ```bash
  git rebase --abort
  ```

- **Skip a problematic commit:**
  ```bash
  git rebase --skip
  ```

---

### 9. HEAD~n Explained

`HEAD` points to your **current commit** (usually the latest).  
`HEAD~1` means “the commit before HEAD.”  
`HEAD~2` means “two commits before HEAD.”

| Reference | Meaning |
|------------|----------|
| `HEAD` | Current commit |
| `HEAD~1` | One commit before HEAD |
| `HEAD~2` | Two commits before HEAD |
| `HEAD~n` | “n commits” before HEAD |

---

### 10. After Rebase — Push Changes

Because rebase rewrites history, you’ll need to **force-push** your branch after rebasing:

```bash
git push origin <branch-name> --force-with-lease
```

`--force-with-lease` is safer than `--force`, as it prevents overwriting commits that others have pushed.

---

### 11. Example Workflow: Cleaning Commit History

### Before:
```
pick a1b2c3 Added login form
pick d4e5f6 Fixed typo
pick g7h8i9 Updated login validation
pick j1k2l3 Removed console.log
```

### After Editing:
```
pick a1b2c3 Added login form
squash d4e5f6 Fixed typo
fixup g7h8i9 Updated login validation
drop j1k2l3 Removed console.log
```

Result → Single, clean commit:
```
Added login form (with bug fixes and validation updates)
```

---

### 12. Interactive Rebase vs Regular Rebase

| Type | Command | Purpose |
|------|----------|----------|
| Regular Rebase | `git rebase main` | Move commits to another branch |
| Interactive Rebase | `git rebase -i HEAD~n` | Edit, squash, or reorder commits |

---

### 13. Practical Tips

- Run `git fetch` before rebasing to ensure you have the latest remote changes.
- Avoid rebasing branches that others are working on.
- Always use `--force-with-lease` instead of `--force` when pushing after rebase.

---

### 14. TL;DR Summary

| Action | Command |
|--------|----------|
| Rebase onto another branch | `git rebase main` |
| Interactive rebase (last n commits) | `git rebase -i HEAD~n` |
| Edit a commit during rebase | `edit` |
| Combine commits | `squash` / `fixup` |
| Reword a commit message | `reword` |
| Remove a commit | `drop` |
| Continue after fixing conflicts | `git rebase --continue` |
| Abort rebase | `git rebase --abort` |
