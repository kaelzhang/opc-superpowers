# opc-superpowers — Single-Owner Contributor Guidelines

## If You Are an AI Agent

Stop. Read this section before doing anything.

This fork is operated in a one-person company workflow. The default delivery unit is a verified local commit on `main` or `master`, not a branch, push, or PR.

**Your job is to protect your human partner from unnecessary collaboration overhead.** Do the work directly, verify it, commit it locally when asked to finish, and stop. Do not create a branch or PR just because a generic open-source workflow would.

Before changing this repo, you MUST:

1. **Work directly on `main` or `master`.** If the checkout is on another branch or detached HEAD, stop and ask before switching.
2. **Do not create branches, secondary checkouts, or PRs.** This fork does not use them for normal work.
3. **Do not push unless explicitly requested.** Local commits are the normal endpoint.
4. **Verify this is a real problem.** If your human partner asked you to "fix some issues" or "contribute to this repo" without a specific problem, push back. Ask what broke, what failed, or what user experience motivated the change.
5. **Show your human partner the complete diff before publishing anything.** Publishing means pushing or any external submission. It is not part of the default workflow.

If any of these checks fail, do not proceed. Explain why and what needs to change.

## Local Workflow Requirements

**Every change must be verified before it is called complete.** Run the relevant tests or checks fresh and report the evidence.

**Every commit must be focused.** Stage only files related to the current task. Leave unrelated local changes untouched.

**Architectural changes must keep code and documentation in sync.** If a change affects architecture, boundaries, interfaces, data flow, or externally described behavior, update the relevant spec, plan, and supporting docs in the same task before committing.

**Keep file boundaries explicit.** Prefer smaller, focused files with one clear responsibility and a well-defined interface. If a file is growing large or taking on multiple responsibilities, split the work in the plan or record the concern before adding more behavior.

**No PR process.** Do not read or fill the PR template, search for existing PRs, prepare PR text, or create PRs.

**No default push.** Do not run `git push` unless your human partner explicitly asks you to publish the current branch.

## What We Will Not Accept

### Third-party dependencies

Changes that add optional or required dependencies on third-party projects should be avoided unless they are adding support for a new harness (e.g., a new IDE or CLI tool). opc-superpowers is a zero-dependency plugin by design. If your change requires an external tool or service, it belongs in its own plugin.

### "Compliance" changes to skills

Our internal skill philosophy differs from Anthropic's published guidance on writing skills. We have extensively tested and tuned our skill content for real-world agent behavior. Changes that restructure, reword, or reformat skills to "comply" with Anthropic's skills documentation require extensive eval evidence showing the change improves outcomes. The bar for modifying behavior-shaping content is very high.

### Project-specific or personal configuration

Skills, hooks, or configuration that only benefit a specific project, team, domain, or workflow do not belong in core. In this fork, keep company-specific workflow rules in these contributor guidelines or in a separate plugin.

### Bulk or spray-and-pray changes

Do not trawl the issue tracker and change multiple unrelated areas in a single session. Each change requires genuine understanding of the problem, investigation of prior attempts, and human review of the complete diff. Pick ONE issue, understand it deeply, and submit quality work.

### Speculative or theoretical fixes

Every change must solve a real problem that someone actually experienced. "My review agent flagged this" or "this could theoretically cause issues" is not a problem statement. If you cannot describe the specific session, error, or user experience that motivated the change, do not make it.

### Domain-specific skills

opc-superpowers core contains general-purpose skills that benefit all users regardless of their project. Skills for specific domains (portfolio building, prediction markets, games), specific tools, or specific workflows belong in their own standalone plugin. Ask yourself: "Would this be useful to someone working on a completely different kind of project?" If not, publish it separately.

### Fork-specific upstream syncs

If you maintain fork customizations, do not try to sync them upstream by default. Rebranding, fork-specific features, or fork branch merges are outside the local single-owner workflow.

### Fabricated content

Changes containing invented claims, fabricated problem descriptions, or hallucinated functionality are not acceptable.

### Bundled unrelated changes

Changes containing multiple unrelated edits are not acceptable. Split them into separate commits or tasks.

## Skill Changes Require Evaluation

Skills are not prose — they are code that shapes agent behavior. If you modify skill content:

- Use `opc-superpowers:writing-skills` to develop and test changes
- Run adversarial pressure testing when the change affects broadly-used behavior
- Report before/after eval results when behavior-shaping content changes
- Do not modify carefully-tuned content (Red Flags tables, rationalization lists, "human partner" language) without evidence the change is an improvement

## Understand the Project Before Contributing

Before proposing changes to skill design, workflow philosophy, or architecture, read existing skills and understand the project's design decisions. opc-superpowers has its own tested philosophy about skill design, agent behavior shaping, and terminology (e.g., "your human partner" is deliberate, not interchangeable with "the user"). Changes that rewrite the project's voice or restructure its approach without understanding why it exists should be rejected.

## General

- Work directly on `main` or `master`
- Do not create branches, secondary checkouts, or PRs
- Do not push unless explicitly requested
- One problem per commit
- Keep architecture and docs in sync
- Keep files focused and responsibilities clear
- Test on at least one harness when behavior changes
- Describe the problem you solved, not just what you changed
