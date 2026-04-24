---
name: finishing-a-development-branch
description: Use when implementation is complete in a single-owner repository and changes need final verification and local commit handling
---

# Finishing Current Main/Master Work

This skill keeps its historical name for compatibility. In this fork, it does **not** merge branches, push branches, or create PRs.

## Overview

Complete development work on the current `main` or `master` branch.

**Core principle:** Verify tests -> review diff -> commit local changes -> stop.

**Announce at start:** "I'm using the finishing workflow to verify and commit this main/master work."

## The Process

### Step 1: Confirm Current Branch

```bash
BRANCH=$(git branch --show-current)
```

**If on `main` or `master`:** Continue.

**If detached HEAD or another branch:**

```
Current branch is <branch-or-detached>. This single-owner workflow finishes work on main/master and does not create branches or PRs.

Should I switch to main/master before finishing?
```

Stop until the human partner confirms. Do not create a branch.

### Step 2: Verify Tests

Run the project test suite before committing:

```bash
npm test / cargo test / pytest / go test ./...
```

**If tests fail:**

```
Tests failing (<N> failures). Must fix before committing:

[Show failures]

Cannot complete local commit until tests pass.
```

Stop. Do not commit.

**If tests pass:** Continue.

### Step 3: Review Workspace Changes

```bash
git status --short
git diff
```

Identify which files belong to the completed task.

- Stage only task-related files.
- Leave unrelated user changes unstaged.
- If ownership is unclear, ask before staging.
- If there are no changes, report that there is nothing to commit.
- If architecture, boundaries, interfaces, or externally described behavior changed, stage the corresponding spec/plan/doc updates too. Do not finalize with architecture drift between code and docs.

### Step 4: Commit Locally

```bash
git add <task-related-files>
git commit -m "<clear summary>"
```

Use a focused commit message that describes the user-facing change or behavior change.

### Step 5: Report Result

```
Committed locally on <main-or-master>: <commit-sha> <commit-title>

No branch was created.
No PR was created.
No push was performed.
```

## Quick Reference

| Situation | Action |
|-----------|--------|
| Tests fail | Stop; fix or ask |
| Tests pass + related changes exist | Stage related files and commit locally |
| No changes | Report nothing to commit |
| Unrelated changes exist | Leave unstaged |
| On another branch | Ask before switching to main/master |
| User asks to push | Confirm explicitly, then push current branch only |
| User asks for PR | Stop; PRs are outside this workflow |

## Common Mistakes

**Creating a branch or PR**
- **Problem:** Adds collaboration overhead this fork does not use.
- **Fix:** Finish with a local commit on `main` or `master`.

**Pushing by default**
- **Problem:** Publishes changes before the human partner asks.
- **Fix:** Commit locally only. Push only with explicit instruction.

**Bundling unrelated changes**
- **Problem:** Existing local work becomes part of the wrong commit.
- **Fix:** Inspect `git status` and stage only task-related files.

**Undocumented architecture changes**
- **Problem:** Code no longer matches the recorded design or interface expectations.
- **Fix:** Update the relevant spec, plan, README, or supporting docs before committing.

**Skipping test verification**
- **Problem:** Commits broken code.
- **Fix:** Always verify tests before committing.

## Red Flags

**Never:**
- Create a branch
- Create a worktree
- Create a PR
- Push without explicit request
- Commit with failing tests
- Stage unrelated changes
- Leave architecture/documentation changes out of the commit when code changed the design
- Delete or overwrite work without confirmation

**Always:**
- Finish on `main` or `master`
- Verify tests before committing
- Review diff before staging
- Keep architecture docs in sync with implementation changes
- Commit locally
- Report that no branch, PR, or push was performed

## Integration

**Called by:**
- **subagent-driven-development** (Step 7) - After all tasks complete
- **executing-plans** (Step 3) - After all batches complete

**Pairs with:**
- **using-git-worktrees** - Verifies the current main/master workspace before work starts
