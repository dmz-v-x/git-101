## Git Clean — Removing Untracked Files Safely  

> Sometimes your working directory gets cluttered with temporary or generated files that aren’t tracked by Git —  
> build artifacts, logs, test outputs, or leftover files from experiments.  
>  
> The `git clean` command helps you **remove untracked files and directories** safely, keeping your workspace tidy.

---

### 1. What Is `git clean`?

- **Purpose:** Deletes **untracked** files and/or directories from your working tree.  
- **Important:** It **does not affect tracked files** (those added with `git add`) or committed history.
- It’s useful when you want to reset your local working directory to a pristine state — as if you just cloned it.

---

### 2. Use With Caution

`git clean` **permanently deletes** untracked files — they do **not** go to trash or recycle bin.  
Always preview what will be deleted before actually cleaning!

---

### 3. Preview Before Cleaning (Dry Run)

### Safe Mode — Check What Will Be Deleted
```bash
git clean -n
# or
git clean --dry-run
```

✅ Shows what would be removed  
❌ Does not actually delete anything

Example output:
```
Would remove temp.txt
Would remove build/
Would remove logs/error.log
```

---

### 4. Actually Clean the Untracked Files

Once you’re confident, run:
```bash
git clean -f
```
(`-f` stands for *force* — required to prevent accidental deletion.)

This removes **untracked files** in the current directory and its subdirectories.

---

### 5. Cleaning Untracked Directories

By default, `git clean -f` only removes **files**, not **directories**.

To clean both files and directories:
```bash
git clean -fd
# or equivalently:
git clean -f -d
```

Example:
```
Removing build/
Removing tmp/
```

---

### 6. Cleaning Ignored Files Too

If you also want to delete **ignored files** (those in `.gitignore`):
```bash
git clean -f -X
```
Deletes **only ignored files**.

To delete **both ignored and untracked files**:
```bash
git clean -f -x
```

| Option | Deletes | Keeps |
|---------|----------|--------|
| `-f` | Untracked files | Ignored files |
| `-fd` | Untracked files & dirs | Ignored files |
| `-f -X` | Ignored files | Untracked files |
| `-f -x` | All (untracked + ignored) | Nothing |

---

### 7. Interactive Cleaning (Safer Alternative)

Git provides an **interactive mode** so you can selectively delete files:

```bash
git clean -i
```

This opens a prompt like:
```
Would remove the following items:
  temp.log
  dist/
*** Commands ***
    1: clean                2: filter by pattern
    3: select by numbers    4: ask each
    5: quit                 6: help
What now> 
```

👉 You can choose what to delete safely, file by file.

---

### 8. Typical Use Cases

### Case 1: Clean build artifacts
```bash
git clean -fd
```
Removes old compiled files or temporary directories before building again.

### Case 2: Remove ignored cache files
```bash
git clean -f -X
```

### Case 3: Full cleanup (all untracked + ignored)
```bash
git clean -fdx
```
Equivalent to a **fresh clone** — only committed files remain.

---

### 9. Combining with Other Git Commands

You can use `git status` before `git clean` to confirm what’s untracked:
```bash
git status
# On branch main
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#   temp.txt
#   build/
```

Then:
```bash
git clean -n  # preview
git clean -fd # execute
```

---

### 10. Summary Table

| Command | Description |
|----------|--------------|
| `git clean -n` | Preview what would be deleted |
| `git clean -f` | Delete untracked files |
| `git clean -fd` | Delete untracked files + directories |
| `git clean -f -X` | Delete only ignored files |
| `git clean -f -x` | Delete all untracked + ignored files |
| `git clean -i` | Interactive clean (confirm before delete) |
| `git clean -e <pattern>` | Exclude specific files from cleaning |

---

### 11. Excluding Files While Cleaning

If you want to **exclude certain files or directories** from deletion:
```bash
git clean -f -e build/
```
This removes all other untracked files except the `build/` directory.

---

### 12. Example Workflow

### Scenario:
You’ve been testing a project and created a bunch of temporary files.

```bash
$ git status
Untracked files:
  temp/
  debug.log
  cache/
```

To clean:
```bash
git clean -n
# Would remove temp/
# Would remove debug.log
# Would remove cache/
```

Looks good, so:
```bash
git clean -fd
```

Output:
```
Removing temp/
Removing debug.log
Removing cache/
```

Now:
```bash
git status
# nothing to commit, working tree clean
```

---

### 13. Important Safety Tips

Always run `git clean -n` first — **preview before delete**.  
`git clean` cannot be undone — the deleted files are **gone permanently**.  
Avoid using `-x` unless you’re absolutely sure — it deletes ignored files too.  
Stash uncommitted changes first if you’re unsure:
```bash
git stash
git clean -fd
git stash pop
```

---

### 14. TL;DR Summary

| Use Case | Command | Description |
|-----------|----------|-------------|
| Preview what will be removed | `git clean -n` | Safe dry-run |
| Delete only untracked files | `git clean -f` | Removes untracked files |
| Delete untracked dirs too | `git clean -fd` | Removes files + dirs |
| Delete only ignored files | `git clean -f -X` | Removes ignored files only |
| Delete everything | `git clean -fdx` | Removes all untracked + ignored |
| Interactive mode | `git clean -i` | Choose what to remove manually |

---

### 15. Recommended Workflow Before Cleaning

1. Check what’s going on:
   ```bash
   git status
   ```
2. Preview the clean:
   ```bash
   git clean -n
   ```
3. If you’re confident:
   ```bash
   git clean -fd
   ```
4. If you want to reset completely:
   ```bash
   git reset --hard
   git clean -fdx
   ```
