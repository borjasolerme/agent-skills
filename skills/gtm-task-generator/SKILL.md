---
name: gtm-task-generator
description: "Generate TASK.md files for growth Ralph campaigns. Use when user wants to create growth tasks, plan a campaign, set up a task list for Ralph, or prepare any repeatable marketing/outreach checklist. Works for any platform, any product, any execution skill."
user-invocable: true
---

# Growth Task Generator

Create a TASK.md ready for growth Ralph.

## Workflow

### 1. Ask what's missing

- **Product** — which product and a one-liner
- **Platform** — where will this run
- **Goal** — what each task accomplishes
- **Skill** — which skill Ralph should load per task (or "none")
- **Tasks** — the list of URLs or actions to execute

Skip anything already clear from conversation.

### 2. Output

Create `growth/[platform]-[product]/TASK.md`:

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

Create `growth/[platform]-[product]/progress.txt`:

```
# Progress Log — [campaign-name]
# Created: [date]
---
```

### 3. Confirm

Show the user the TASK.md. Ask if anything needs changing. Then confirm:

```bash
cd growth
./scripts/ralph/ralph.sh [campaign-name] 20
```
