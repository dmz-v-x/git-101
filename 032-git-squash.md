## Git Squash — Combining Commits into One Clean Commit

> “Squashing” in Git means combining multiple commits into a **single, meaningful commit**.  
> It’s a powerful way to tidy up your Git history before merging or sharing your branch.

---

### 1. What Is Git Squash?

Every time you commit, Git saves a snapshot of your changes.  
Sometimes, while working on a feature, you might make many small commits like:

```
commit 1: Added login form
commit 2: Fixed typo
commit 3: Adjusted layout
commit 4: Updated validation logic
```

Before merging into `main`, you might want all these small commits combined into one:

```
commit: Added login form feature
```

That’s **squashing** — taking several commits and merging them into a single, cleaner one.

---

### 2. Why Squash Commits?

**Cleaner History** — makes your Git log easier to read  
**Single Commit per Feature** — better for pull requests and code reviews  
**Avoid Clutter** — small “fix typo”, “update spacing” commits disappear  
**Professionalism** — makes your contributions look polished and organized

---

### 3. Ways to Squash Commits

There are two main methods:

1. **Using Interactive Rebase (`git rebase -i`)** — manual and precise  
2. **Using Merge Squash (`git merge --squash`)** — automatic, when merging a branch

Let’s go through both.

---

### 4. Method 1: Interactive Rebase (Manual Squash)

### Step 1: Check Your Commit History
```bash
git log --oneline
```

Example output:
```
a1b2c3e Added login form
b2c3d4f Fixed typo
c3d4e5f Updated form style
d4e5f6g Improved validation
```

You want to squash the **last 3 commits** into one.

---

### Step 2: Start Interactive Rebase
```bash
git rebase -i HEAD~4
```
(`HEAD~4` means “the last 4 commits including the one you want to keep.”)

---

### Step 3: The Rebase Editor Opens

```
pick a1b2c3e Added login form
pick b2c3d4f Fixed typo
pick c3d4e5f Updated form style
pick d4e5f6g Improved validation
```

To squash, change all but the first `pick` to `squash` (or `s`):

```
pick a1b2c3e Added login form
squash b2c3d4f Fixed typo
squash c3d4e5f Updated form style
squash d4e5f6g Improved validation
```

---

### Step 4: Combine Commit Messages

Git opens another editor window asking you to combine or edit commit messages.

You can keep just one clean message:
```
Added login form feature with style and validation improvements
```

Save and close the editor.

---

### Step 5: Finalize the Rebase

Once done, verify your new history:
```bash
git log --oneline
```

Output:
```
e7f8g9h Added login form feature with style and validation improvements
```

Your 4 commits are now 1 clean commit.

---

## 5. Method 2: Squash on Merge (Automatic)

This is useful when merging a feature branch into `main`.

### Step 1: Checkout Main
```bash
git checkout main
```

### Step 2: Merge with Squash
```bash
git merge --squash feature-branch
```

This applies all commits from `feature-branch` as a **single set of staged changes** — not as individual commits.

### Step 3: Commit the Squashed Changes
```bash
git commit -m "Added login feature with validation"
```

### Step 4: Push to Remote
```bash
git push origin main
```

You’ve successfully merged multiple commits as one clean commit.

---

### 6. Squashing Best Practices

| Practice | Why |
|-----------|-----|
| Squash commits **before merging** a feature branch | Keeps `main` clean |
| Avoid squashing after pushing to shared remote branches | Changes commit hashes and can confuse teammates |
| Use meaningful messages after squashing | Better commit history and traceability |
| Use `--force-with-lease` when pushing rebased or squashed commits | Safer than `--force` |

---

### 7. Squash vs Rebase — Key Differences

| Action | Command | Purpose |
|---------|----------|----------|
| **Rebase** | `git rebase main` | Replay commits on another branch |
| **Interactive Rebase (Squash)** | `git rebase -i HEAD~n` | Combine commits manually |
| **Merge Squash** | `git merge --squash feature` | Combine commits automatically while merging |

---

### 8. Example: Real-World Workflow

### Scenario:
You’re developing a feature with multiple commits:

```
commit 1: Added signup form
commit 2: Fixed typo
commit 3: Added password validation
commit 4: Updated button color
```

Before merging to main, you want to squash them into one.

1. Start rebase:
   ```bash
   git rebase -i HEAD~4
   ```

2. Change:
   ```
   pick
   squash
   squash
   squash
   ```

3. Write clean message:
   ```
   Added signup form with validation and UI fixes
   ```

4. Force push (if branch already pushed):
   ```bash
   git push origin feature --force-with-lease
   ```

5. Create pull request → one clean commit visible to reviewers

---

### 9. Undo a Bad Squash (Recovery)

If your squash caused issues:
```bash
git reflog
# Find the commit hash before squash
git reset --hard <old-commit-hash>
```

This restores your branch to its previous state.

---

### 10. Summary Table

| Task | Command |
|------|----------|
| Start interactive rebase | `git rebase -i HEAD~n` |
| Squash commits manually | Change `pick` → `squash` |
| Merge & squash automatically | `git merge --squash feature-branch` |
| Undo a squash | `git reflog` → `git reset --hard` |
| Safe force-push after squash | `git push --force-with-lease` |
