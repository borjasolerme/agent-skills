---
name: reddit-comment-writer
description: Write authentic Reddit comments that naturally mention a product. Supports profiles, batch mode, engagement tracking, and progressive learning. Triggers on "write a reddit comment", "set up [company]", "do today for [company]", "fill quota", "learn my style", "show progress", "check engagement", or when the user shares a Reddit URL.
---

# Reddit Comment Writer

## Routing

| User says | Action |
|---|---|
| "set up [company]" / "new profile" | Follow `workflows/setup-profile.md` |
| "do today for [company]" / "fill quota" | Follow `workflows/batch-mode.md` |
| "create posts" / "write reddit posts" | Follow `workflows/value-posts.md` |
| "learn my style" / pastes comments | Follow `personalization/voice-samples.md` |
| "show progress" | Display `tracking/{YYYY-MM-DD}.md` |
| "check engagement" | Run engagement review in `workflows/batch-mode.md` |
| Shares a Reddit URL | Skip to Write Comments below |
| None of the above | Show menu: write comments, do today, create posts, set up profile, learn style, show progress, check engagement |

## Critical Rules

- Check Reddit login before posting
- Every comment must be unique
- Read the full thread before drafting
- Rewrite any draft that fails `rules/spam-signals.md` checks
- Never draft without reading `rules/style-guide.md` first

## File Loading — Read Only When Needed

| File | When |
|---|---|
| `profiles/{slug}.md` | When user names a company |
| `rules/style-guide.md` | Before drafting |
| `rules/comment-angles.md` | Before drafting |
| `rules/spam-signals.md` | Before submitting |
| `personalization/voice-samples.md` | Before drafting, if Voice Analysis exists |
| `tracking/insights.md` | Subreddit study, engagement review, drafting |
| `tracking/post-insights.md` | Value posts research |

## Tools — Priority Order

**Reddit API** > **agent-browser** ([vercel-labs/agent-browser](https://github.com/vercel-labs/agent-browser)) > **Playwright** (`mcp__playwright__`) > pasted text.

| Action | Reddit API | agent-browser | Playwright |
|---|---|---|---|
| Search/browse | `GET /search`, `GET /r/{sub}/new` | navigate + extract | `browser_navigate` + `browser_snapshot` |
| Read thread | `GET /comments/{id}` | navigate + extract | `browser_navigate` + `browser_snapshot` |
| Post comment | `POST /api/comment` | navigate + type + submit | `browser_type` + `browser_click` |
| Check engagement | `GET /api/info?id={id}` | navigate + extract | navigate + extract |

## Progressive Learning

The examples in `rules/comment-angles.md` are training wheels. As `tracking/insights.md` grows with real engagement data, shift away from examples toward what actually works:

- **< 10 tracked comments:** Follow examples closely
- **10-30 comments:** Blend examples with engagement insights
- **30+ comments:** Lead with insights, reference examples only for untried angles

## Write Comments Flow

1. **Load profile** from `profiles/`. If missing, ask product name + URL + description. If profile's `Product Knowledge` > 2 weeks old, re-visit the product website first.
2. **Study subreddit** — see `workflows/batch-mode.md` Subreddit Study. Skip if `tracking/insights.md` has fresh data (< 3 days).
3. **Find posts** — use target subreddits from profile, skip posts in `tracking/` from last 7 days. Read full thread + top comments for each.
4. **Draft 5 comments** — one per angle. Apply `rules/style-guide.md`, `rules/comment-angles.md`, voice personalization, and subreddit insights.
5. **Self-critique** against `rules/spam-signals.md`. Present top 3, mark recommended pick.
6. **Post** after user confirms. Log to `tracking/{YYYY-MM-DD}.md` per `tracking/FORMAT.md`.
