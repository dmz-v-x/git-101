## Git Tags

### 1. Introduction: What Are Git Tags and Why They Matter

A **Git tag** is a **named reference to a specific commit**.

Why tags exist:
- Mark important points in history
- Identify releases (v1.0.0, v2.1.3)
- Provide stable references
- Enable clean release workflows

Mental model:
A tag is a **sticky note** placed on a commit saying  
“This commit matters”.

Unlike branches:
- Tags do not move
- Tags are immutable by convention

---

### 2. Core Prerequisites (Very Important)

Before using Git tags, you should understand:
- Commits and commit hashes
- Branches vs HEAD
- Remotes and pushing
- Basic Git history navigation

Key idea:
Tags always point to **exact commits**, not files or branches.

---

### 3. Types of Git Tags (High-Level View)

Git provides **two types of tags**:
- Lightweight tags
- Annotated tags

Both point to commits  
But they store **very different metadata**.

Understanding this difference is critical.

---

### 4. Lightweight Tags (Basics)

A **lightweight tag** is:
- Just a name pointing to a commit
- No extra metadata
- No message
- No author information

Think of it as:
A simple alias for a commit hash.

Creating a lightweight tag:
    git tag v1.0.0

This tags the current HEAD.

---

### 5. When to Use Lightweight Tags

Use lightweight tags when:
- You want quick markers
- You do not need metadata
- Internal or temporary labeling is enough

Avoid them for:
- Public releases
- Auditable versioning
- Signed releases

---

### 6. Annotated Tags (Most Important)

An **annotated tag** is a full Git object.

It stores:
- Tag name
- Tag message
- Tagger name & email
- Date
- Optional cryptographic signature

Creating an annotated tag:
    git tag -a v1.0.0 -m "Release version 1.0.0"

This is the **recommended type for releases**.

---

### 7. Lightweight vs Annotated Tags (Direct Comparison)

Lightweight:
- Name → commit pointer
- No metadata
- Fast and simple

Annotated:
- Full object
- Message + author + date
- Can be signed
- Suitable for releases

Rule of thumb:
Use annotated tags for anything important.

---

### 8. Listing and Inspecting Tags

List all tags:
    git tag

View tag details:
    git show v1.0.0

For annotated tags:
- You see message and metadata

For lightweight tags:
- You only see commit info

---

### 9. Tagging Past Commits

Tags don’t have to be on HEAD.

To tag a specific commit:
    git tag -a v1.2.0 <commit-hash>

This is common when:
- Retroactively marking releases
- Fixing forgotten tags

---

### 10. Tags Are Not Automatically Pushed (Critical Detail)

Important behavior:
Tags are **local by default**.

To push a single tag:
    git push origin v1.0.0

To push all tags:
    git push origin --tags

This explicit step prevents accidental releases.

---

### 11. Deleting Tags (Local and Remote)

Delete a local tag:
    git tag -d v1.0.0

Delete a remote tag:
    git push origin --delete v1.0.0

Tag deletion should be rare and carefully communicated.

---

### 12. Using Tags for Versioning (Core Practice)

Tags commonly represent **semantic versions**.

Example:
- v1.0.0
- v1.1.0
- v2.0.0

Each tag:
- Marks a released state
- Maps directly to a commit
- Enables reproducible builds

Versioning becomes part of Git history.

---

### 13. Semantic Versioning (SemVer Basics)

SemVer format:
    MAJOR.MINOR.PATCH

Rules:
- MAJOR → breaking changes
- MINOR → backward-compatible features
- PATCH → bug fixes

Tags enforce discipline in release management.

---

### 14. Releasing Software with Git Tags (Workflow)

Typical release flow:
1. Finish development on main branch
2. Run tests
3. Create annotated tag
4. Push tag
5. Build artifacts from the tag
6. Publish release

Tags act as **release triggers**.

---

### 15. Tags and CI/CD Pipelines

Modern CI systems:
- Detect new tags
- Run release pipelines
- Publish artifacts automatically

Example logic:
- On push to branch → run tests
- On tag creation → build & release

Tags separate development from release.

---

### 16. Checking Out Tags (Detached HEAD)

To inspect a tag:
    git checkout v1.0.0

Result:
- Detached HEAD state
- Read-only exploration

For fixes:
- Create a branch from the tag

---

### 17. Signing Tags and Commits (Security)

Signing ensures:
- Authenticity
- Integrity
- Trust in releases

Git supports:
- GPG-signed commits
- GPG-signed tags

Signed tags are preferred for official releases.

---

### 18. GPG Keys: Mental Model

A GPG key pair:
- Private key → used to sign
- Public key → used to verify

You keep:
- Private key secret

You share:
- Public key with platforms like GitHub

---

### 19. Signing an Annotated Tag

To sign a tag:
    git tag -s v1.0.0 -m "Signed release v1.0.0"

This:
- Creates an annotated tag
- Cryptographically signs it

Verification:
    git tag -v v1.0.0

---

### 20. Signing Commits vs Signing Tags

Signed commits:
- Verify individual commits

Signed tags:
- Verify entire release snapshot

Best practice:
- Sign commits during development
- Sign tags for releases

---

### 21. Trust and Verification in Teams

Why signatures matter:
- Prevent tampering
- Prove authorship
- Secure supply chain

Many orgs:
- Require signed tags
- Reject unsigned releases

---

### 22. Common Mistakes with Git Tags

- Forgetting to push tags
- Using lightweight tags for releases
- Retagging released versions
- Not signing important tags
- Treating tags like branches

---

### 23. Advanced Tag Usage

- Tag release candidates (v2.0.0-rc.1)
- Tag hotfix releases
- Automate tag creation
- Enforce tag naming conventions

Tags integrate deeply with automation.

---

### 24. Best Practices Summary

- Use annotated tags for releases
- Follow semantic versioning
- Sign important tags
- Never move published tags
- Document your release process

---

### 25. Final Summary

You now understand:
- What Git tags are
- Lightweight vs annotated tags
- How tagging works internally
- Using tags for versioning
- Secure signing with GPG
- Releasing software using tags

At this point, you can **confidently design professional Git release workflows** using tags.
