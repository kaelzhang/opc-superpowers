---
name: using-git-worktrees
description: Use when starting implementation work in a single-owner repository where changes should stay on main/master rather than branches or PRs
---

# Using the Current Main/Master Workspace

This skill keeps its historical name for compatibility. In this fork, it does **not** create git worktrees or branches.

## Overview

Single-owner work happens directly on `main` or `master`.

**Core principle:** Verify current workspace state + baseline tests = ready to edit.

**Announce at start:** "I'm using the workspace setup skill to verify the current main/master workspace."

## The Process

### Step 1: Confirm Current Branch

```bash
BRANCH=$(git branch --show-current)
```

**If on `main` or `master`:** Continue.

**If detached HEAD or another branch:**

```
Current branch is <branch-or-detached>. This single-owner workflow works directly on main/master and does not create branches.

Should I switch to main/master before continuing?
```

Stop until the human partner confirms. Do not create a branch.

### Step 2: Check Workspace State

```bash
git status --short
```

**If clean:** Continue.

**If dirty:** Read the diff and identify whether changes are related to this task.

- Related changes: work with them.
- Unrelated changes: leave them alone and avoid staging them.
- Unclear ownership: ask before touching or staging them.

Never discard, reset, or overwrite existing work without explicit instruction.

### Step 3: Run Project Setup

Auto-detect and run appropriate setup if dependencies may be missing:

```bash
# Node.js
if [ -f package.json ]; then npm install; fi

# Rust
if [ -f Cargo.toml ]; then cargo build; fi

# Python
if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
if [ -f pyproject.toml ]; then poetry install; fi

# Go
if [ -f go.mod ]; then go mod download; fi
```

Skip setup when the project is already configured and there is no reason to reinstall.

### Step 4: Verify Clean Baseline

Run tests before editing so new failures are distinguishable from existing failures:

```bash
# Examples - use project-appropriate command
npm test
cargo test
pytest
go test ./...
```

**If tests fail:** Report failures and ask whether to investigate before implementing.

**If tests pass:** Report ready.

### Step 5: Report State

```
Workspace ready on <main-or-master>
Tests passing (<N> tests, 0 failures)
Ready to implement <feature-name>
```

## Quick Reference

| Situation | Action |
|-----------|--------|
| On `main` or `master` | Continue |
| On another branch | Ask before switching; do not create a branch |
| Detached HEAD | Ask how to get back to main/master |
| Dirty workspace | Inspect and preserve existing work |
| Tests fail during baseline | Report failures + ask |
| No package.json/Cargo.toml | Skip dependency install |

## Common Mistakes

### Creating isolation that this fork does not use

- **Problem:** Branches and worktrees add process overhead for this single-owner workflow.
- **Fix:** Work directly on `main` or `master`.

### Staging unrelated changes

- **Problem:** Existing local work gets bundled into the current task.
- **Fix:** Inspect `git status` and stage only task-related files.

### Proceeding with failing tests

- **Problem:** Can't distinguish new bugs from pre-existing issues.
- **Fix:** Report failures, get explicit permission to proceed.

### Pushing or opening PRs

- **Problem:** Publishing is not part of the default local workflow.
- **Fix:** Commit locally only. Push only when explicitly requested. Do not create PRs.

## Red Flags

**Never:**
- Create a branch
- Create a worktree
- Open a PR
- Push by default
- Skip baseline test verification
- Proceed with failing tests without asking
- Discard or stage unrelated work

**Always:**
- Work directly on `main` or `master`
- Check current branch before editing
- Inspect workspace status
- Auto-detect project setup when needed
- Verify clean test baseline

## Integration

**Called by:**
- **brainstorming** (Phase 4) - REQUIRED when design is approved and implementation follows
- **subagent-driven-development** - REQUIRED before executing any tasks
- **executing-plans** - REQUIRED before executing any tasks
- Any skill needing current workspace verification

**Pairs with:**
- **finishing-a-development-branch** - REQUIRED for final verification and local commit handling
