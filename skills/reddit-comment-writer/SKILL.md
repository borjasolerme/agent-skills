---
name: reddit-comment-writer
description: Write authentic Reddit comments that naturally mention a product. Fully autonomous — finds subreddits, searches posts, researches threads, writes and posts comments. Triggers on "write a reddit comment", "set up [company]", "do today for [company]", "fill quota", "learn my style", "show progress", "check engagement".
---

# Reddit Comment Writer

The agent does everything: find subreddits, search posts, read threads, draft comments, post them. User only confirms before posting.

## Routing

No profile exists yet? Follow `workflows/setup-profile.md`, then go straight into first session.

| User says | Action |
|---|---|
| "do today for [company]" / "fill quota" / "write comments" | Follow `workflows/batch-mode.md` |
| "create posts" / "write reddit posts" | Follow `workflows/value-posts.md` |
| "set up [company]" / "new profile" | Follow `workflows/setup-profile.md` |
| "learn my style" / pastes comments | Follow `personalization/voice-samples.md` |
| "show progress" | Display `tracking/{YYYY-MM-DD}.md` |
| "check engagement" | Run engagement review in `workflows/batch-mode.md` |

## Rules

- Check Reddit login before posting
- Every comment must be unique
- Read the full thread before drafting
- Rewrite any draft that fails `rules/spam-signals.md`
- Never draft without reading `rules/style-guide.md`

## Tools — Priority Order

**Reddit API** > **agent-browser** ([vercel-labs/agent-browser](https://github.com/vercel-labs/agent-browser)) > **Playwright** (`mcp__playwright__`)

| Action | Reddit API | agent-browser | Playwright |
|---|---|---|---|
| Search/browse | `GET /search`, `GET /r/{sub}/new` | navigate + extract | `browser_navigate` + `browser_snapshot` |
| Read thread | `GET /comments/{id}` | navigate + extract | `browser_navigate` + `browser_snapshot` |
| Post comment | `POST /api/comment` | navigate + type + submit | `browser_type` + `browser_click` |
| Check engagement | `GET /api/info?id={id}` | navigate + extract | navigate + extract |

## Progressive Learning

Examples in `rules/comment-angles.md` are training wheels. As `tracking/insights.md` grows, shift to real data:

- **< 10 comments tracked:** follow examples closely
- **10-30:** blend examples with engagement insights
- **30+:** lead with insights, examples only for untried angles

## Files — Read Only When Needed

| File | When |
|---|---|
| `profiles/{slug}.md` | Session start |
| `rules/style-guide.md` | Before drafting |
| `rules/comment-angles.md` | Before drafting |
| `rules/spam-signals.md` | Before submitting |
| `personalization/voice-samples.md` | Before drafting, if Voice Analysis exists |
| `tracking/insights.md` | Subreddit study, engagement review, drafting |
| `tracking/post-insights.md` | Value posts only |
| `tracking/FORMAT.md` | When logging |
