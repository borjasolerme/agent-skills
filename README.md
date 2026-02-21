# Agent Skills

A collection of personal skills I use for my work and projects with [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

## Skills

### Reddit Comment Writer

Write authentic Reddit comments that naturally mention a product without sounding spammy.

**Triggers:** `write a reddit comment`, `set up [company]`, `do today for [company]`, `fill quota`, `learn my style`, `show progress`

**What it does:**
- Creates company profiles with talking points, target subreddits, and preferred angles
- Finds relevant posts and drafts comments using 5 different angles (helper, tool list, experience share, follow-up question, contrarian)
- Runs anti-spam checks against real Reddit detection patterns
- Learns your writing voice from comment samples
- Tracks daily activity and quota per subreddit
- Posts via browser automation with user confirmation

```
skills/reddit-comment-writer/
├── SKILL.md
├── rules/
│   ├── style-guide.md
│   ├── comment-angles.md
│   └── spam-signals.md
├── workflows/
│   ├── setup-profile.md
│   └── batch-mode.md
├── personalization/
│   └── voice-samples.md
├── profiles/
└── tracking/
```

---

### Directory Submitter

Submit products to 190 free AI/startup directories using browser automation.

**Triggers:** `submit [product] to directories`, `set up [product] for directories`, `show submission progress`, `add directory`

**What it does:**
- Visits your product URL, extracts info, and generates short/medium/long descriptions
- Takes homepage screenshots for directory submissions
- Fills submission forms automatically via browser automation
- Confirms with user before each submit
- Tracks submission status per directory (submitted, pending, approved, live, rejected)
- 190 free directories sorted by Domain Rating (DR 92 to 0)

```
skills/directory-submitter/
├── SKILL.md
├── directories/
│   └── DIRECTORIES.md
├── workflows/
│   ├── setup-product.md
│   └── submit-mode.md
├── profiles/
└── tracking/
```

---

## Setup

1. Clone this repo into your agents directory:

```bash
git clone git@github.com:borjasolerme/agent-skills.git ~/.agents/skills
```

2. Reference the skills directory in your `CLAUDE.md`:

```markdown
Skills are located at ~/.agents/skills/
```

3. Start a new Claude Code conversation and trigger any skill by name.

## Design Patterns

All skills follow the same patterns:

- **Lazy file loading** -- files are only read at the step that needs them, not upfront
- **Browser automation priority** -- Chrome Extension > Playwright > manual paste
- **Interactive flows** -- questions are asked together, agent waits for answers before proceeding
- **Persistent tracking** -- markdown files updated after each action
- **User confirmation** -- destructive or public actions always require explicit approval
