---
name: gtm-task-generator
description: "Generate TASK.md files for growth Ralph campaigns. Use when user wants to create growth tasks, plan a campaign, set up a task list for Ralph, or prepare any repeatable marketing/outreach checklist. Works for any platform, any product, any execution skill."
user-invocable: true
---

# Growth Task Generator

Create a TASK.md ready for growth Ralph.

## Workflow

### 1. Ask these questions — ALWAYS, even if some seem obvious

Ask all of these one by one. Do NOT assume answers from context. Do NOT skip any. Wait for the user to respond before proceeding.

1. **Product** — which product and a one-liner about it
2. **Platform** — where will this run (Reddit, directories, Quora, forums, etc.)
3. **Goal** — what should each task accomplish
4. **Skill** — which installed skill should Ralph load to execute each task? List the user's installed skills and ask them to pick one, or "none" if tasks are just instructions.
5. **Tasks** — ask the user to provide their list of URLs or actions

### 2. Output

Create `[platform]-[product]/TASK.md` in the current directory:

```markdown
# [Campaign Title]

## Product
[Name] — [one-liner]

## Platform
[Platform]

## Goal
[What each task accomplishes]

## Skill
[Skill name or "none"]

## Context
[Enough detail for autonomous execution — positioning, tone, features, constraints.]

## Tasks
- [ ] [task or URL]
- [ ] [task or URL]
```

Create `[platform]-[product]/progress.txt`:

```
# Progress Log — [campaign-name]
# Created: [date]
---
```

### 3. Confirm

Show the TASK.md to the user BEFORE saving. Ask:
- Does this look right?
- Anything to change?

Only save after user confirms. Then show:

```bash
cd growth
./scripts/ralph/ralph.sh [campaign-name] 20
```
