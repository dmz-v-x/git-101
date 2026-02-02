## Git Hooks

### 1. Introduction: What Are Git Hooks and Why They Exist

Git Hooks are **scripts that Git automatically runs** when certain events happen.

Why hooks exist:
- Enforce code quality
- Automate repetitive checks
- Prevent bad commits from entering history
- Integrate workflows with CI/CD

Mental model:
A Git hook is a **checkpoint** where Git says  
“Before/After this action, do you want to run something?”

Hooks turn Git from a passive tool into an **active enforcer**.

---

### 2. Where Git Hooks Live (.git/hooks)

Every Git repository contains a hidden directory:
    .git/hooks/

This folder:
- Exists locally on your machine
- Contains sample hook scripts
- Is NOT committed to the repository by default

Important implication:
Hooks are **local by default**, not shared automatically.

---

### 3. Core Prerequisites (Very Important)

Before using hooks, you should understand:
- Basic Git commands (commit, push, merge)
- Shell scripting basics
- Exit codes (0 = success, non-zero = failure)
- That Git actions can be blocked intentionally

Hooks rely heavily on **exit status**.

---

### 4. How Git Hooks Work Internally

How Git executes a hook:
1. A Git event occurs (e.g., commit)
2. Git checks if a hook script exists
3. If executable → Git runs it
4. Script exits
5. Exit code decides whether Git continues

Rule:
- Exit 0 → allow action
- Exit non-zero → block action

This is the foundation of hook power.

---

### 5. Types of Git Hooks (High-Level View)

Git hooks are divided into:
- Client-side hooks
- Server-side hooks

Client-side:
- Run on developer machines
- Enforce local checks

Server-side:
- Run on central repository
- Enforce organization-wide rules

---

### 6. Client-Side Hooks (Overview)

Common client-side hooks:
- pre-commit
- commit-msg
- post-commit
- pre-push
- post-checkout
- post-merge

Client-side hooks:
- Improve developer experience
- Catch issues early
- Are not security guarantees

---

### 7. Pre-Commit Hook (Most Important)

The **pre-commit** hook runs:
- Before the commit is created
- After `git commit` is triggered
- Before commit message is finalized

Use cases:
- Linting
- Formatting
- Static analysis
- Prevent committing secrets

This hook blocks bad commits early.

---

### 8. Pre-Commit Hook Mental Model

Think of pre-commit as:
“You’re about to save history. Are you sure this code is acceptable?”

If the hook fails:
- Commit is aborted
- Developer must fix issues

This encourages clean history.

---

### 9. Common Pre-Commit Use Cases

Typical checks:
- ESLint / Prettier
- Type checking
- Unit tests (lightweight)
- File size limits
- Forbidden patterns

Rule:
Pre-commit hooks should be **fast**.

---

### 10. Creating a Pre-Commit Hook (Basics)

Steps:
1. Go to `.git/hooks/`
2. Create a file named `pre-commit`
3. Make it executable
4. Write script logic

Git automatically detects it by name.

---

### 11. Commit Message Hooks (commit-msg)

The `commit-msg` hook runs:
- After message is written
- Before commit is finalized

Use cases:
- Enforce message format
- Enforce conventional commits
- Reject empty or vague messages

This keeps history readable and consistent.

---

### 12. Post-Commit Hook

The **post-commit** hook runs:
- After a commit is successfully created
- Cannot block the commit

Use cases:
- Notifications
- Logging
- Local automation
- Updating documentation

Post-commit hooks are informative, not preventive.

---

### 13. Pre-Push Hook (Very Powerful)

The **pre-push** hook runs:
- Before pushing to a remote
- After commits already exist locally

Use cases:
- Run full test suite
- Check branch rules
- Prevent pushing to protected branches
- Validate environment

Pre-push is stricter than pre-commit.

---

### 14. Pre-Push vs Pre-Commit (Key Difference)

Pre-commit:
- Runs often
- Must be fast
- Code-quality focused

Pre-push:
- Runs less often
- Can be slower
- Safety-focused

Use both together for layered protection.

---

### 15. Other Useful Client-Side Hooks

Less common but useful hooks:
- post-checkout → react to branch switches
- post-merge → run after merges
- pre-rebase → block dangerous rebases

These hooks support advanced workflows.

---

### 16. Custom Automation with Hooks

Hooks are just scripts.

You can:
- Run any command
- Call scripts
- Trigger tools
- Chain workflows

Hooks can automate:
- Code generation
- Dependency checks
- Environment validation

Think beyond just linting.

---

### 17. Limitations of Client-Side Hooks

Important limitations:
- Not shared automatically
- Can be bypassed
- Depend on local environment

Conclusion:
Client-side hooks are **guidelines**, not enforcement.

---

### 18. Sharing Hooks Across Teams (Important Problem)

Since `.git/hooks` isn’t committed:
- Teams need a strategy

Common approaches:
- Scripts folder + setup script
- Git templates
- Hook managers
- Documentation + enforcement

Consistency requires tooling.

---

### 19. Hook Management Tools (Advanced)

Popular hook management solutions:
- Husky
- pre-commit framework
- Lefthook
- Simple shell scripts

These tools:
- Version hooks
- Auto-install hooks
- Reduce friction

They bridge the sharing gap.

---

### 20. Server-Side Hooks (Concept)

Server-side hooks run:
- On the Git server
- After push attempts
- Before accepting data

Key difference:
Developers cannot bypass them.

Server-side hooks enforce rules globally.

---

### 21. Common Server-Side Hooks

Important server hooks:
- pre-receive
- update
- post-receive

Use cases:
- Reject unsigned commits
- Enforce branch protection
- Validate commit metadata
- Trigger deployments

These hooks are authoritative.

---

### 22. Modern Reality: Hosted Git Platforms

On platforms like GitHub and GitLab:
- Direct server hooks are not accessible
- Security restrictions apply

Instead, platforms provide:
- CI pipelines
- Webhooks
- Policy enforcement tools

This shifts enforcement to CI/CD.

---

### 23. Git Hooks vs CI/CD Pipelines

Git hooks:
- Local or server-level
- Immediate feedback
- Lightweight

CI/CD:
- Centralized
- Slower but stronger
- Non-bypassable

Best practice:
Use hooks for **early feedback**  
Use CI for **final enforcement**.

---

### 24. GitHub Actions / GitLab CI Integration (Basics)

Workflow:
1. Developer commits (local hooks run)
2. Developer pushes (pre-push hook may run)
3. CI pipeline triggers on push or tag
4. CI validates code centrally
5. Merge allowed or blocked

Hooks + CI form a safety net.

---

### 25. Advanced Enforcement Strategies

Advanced setups:
- Require passing CI checks
- Require signed commits
- Block force-pushes
- Enforce branch naming
- Enforce tag rules

Hooks support culture, CI enforces policy.

---

### 26. Security Considerations with Hooks

Risks:
- Malicious hook scripts
- Environment-specific failures
- Silent bypassing

Best practices:
- Audit shared hooks
- Keep hooks readable
- Avoid destructive operations

Hooks should protect, not surprise.

---

### 27. Common Mistakes with Git Hooks

- Running slow tasks in pre-commit
- Relying only on hooks for enforcement
- Not documenting hook behavior
- Assuming hooks are shared automatically
- Ignoring Windows compatibility

---

### 28. Best Practices Summary

- Keep pre-commit fast
- Use pre-push for safety checks
- Share hooks via tooling
- Enforce rules in CI
- Treat hooks as helpers, not guards

---

### 29. Final Summary

You now understand:
- What Git hooks are
- Where they live and how they run
- Pre-commit, post-commit, and pre-push hooks
- Custom automation possibilities
- Server-side hooks and CI integration
- Limitations, risks, and best practices

At this point, you can **design professional-grade Git automation workflows** using hooks combined with CI/CD.
