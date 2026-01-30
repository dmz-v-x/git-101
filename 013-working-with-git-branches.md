## Creating, Switching, and Deleting Branches in Git

##  Overview

Branches in Git are lightweight pointers to commits.  
They allow you to work on different features or fixes **independently** without disturbing the main branch.

You can **create**, **switch**, **rename**, **list**, and **delete** branches using `git branch`, `git checkout`, and `git switch`.

---

##  Branch Management Commands

### 1. List Branches

| Command | Description | Example |
|----------|--------------|----------|
| `git branch` | Lists all local branches | `git branch` |
| `git branch -a` | Lists all branches (local + remote) | `git branch -a` |
| `git branch -r` | Lists only remote branches | `git branch -r` |

---

### 2. Create a New Branch

| Command | Description | Example |
|----------|--------------|----------|
| `git branch <branch-name>` | Creates a new branch but **doesn’t switch** to it | `git branch feature-login` |

To both **create and switch** in one step:

| Command | Description | Example |
|----------|--------------|----------|
| `git checkout -b <branch-name>` | Creates and switches to the new branch | `git checkout -b feature-login` |
| `git switch -c <branch-name>` | Newer, simpler alternative to checkout | `git switch -c feature-login` |

---

### 3. Switch Between Branches

| Command | Description | Example |
|----------|--------------|----------|
| `git checkout <branch-name>` | Switches to an existing branch | `git checkout main` |
| `git switch <branch-name>` | Recommended modern command | `git switch main` |

---

### 4. Rename a Branch

| Command | Description | Example |
|----------|--------------|----------|
| `git branch -m <old-name> <new-name>` | Renames a branch (works for current or other branches) | `git branch -m master main` |

If you’re already on the branch you want to rename:
```bash
git branch -m <new-name>
```

---

### 5. Delete a Branch

#### Local Deletion

| Command | Description | Example |
|----------|--------------|----------|
| `git branch -d <branch-name>` | Deletes the branch **safely** (warns if unmerged changes exist) | `git branch -d feature-login` |
| `git branch -D <branch-name>` | Force deletes the branch (even if unmerged) | `git branch -D feature-login` |

#### Remote Deletion

| Command | Description | Example |
|----------|--------------|----------|
| `git push origin --delete <branch-name>` | Deletes branch from remote repository | `git push origin --delete feature-login` |

---

### Summary

| Action | Command | Notes |
|--------|----------|-------|
| Create branch | `git branch feature-x` | Just creates the branch |
| Create & switch | `git checkout -b feature-x` or `git switch -c feature-x` | One-step creation |
| Switch branch | `git checkout main` or `git switch main` | Move between branches |
| Rename branch | `git branch -m old new` | Works locally |
| Delete branch | `git branch -d feature-x` | Safe delete |
| Force delete | `git branch -D feature-x` | Unchecked delete |
| Delete remote | `git push origin --delete feature-x` | Removes from remote |

**In short:**  
Git branches are flexible, powerful, and fast.  
They let you isolate your work, experiment freely, and collaborate effectively — all while keeping your main codebase stable.
