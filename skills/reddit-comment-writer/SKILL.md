---
name: reddit-comment-writer
description: Write authentic Reddit comments that naturally mention a product. Handles everything autonomously — finds subreddits, searches posts, researches threads, writes and posts comments. Triggers on "write a reddit comment", "set up [company]", "do today for [company]", "fill quota", "learn my style", "show progress", "check engagement".
---

# Reddit Comment Writer

## First Session Flow

If no profile exists yet, walk the user through these questions:

1. **Product info** — what's the product, URL, one-sentence description? Then follow `workflows/setup-profile.md`.
2. **Subreddits** — "do you have target subreddits in mind, or should I search for the best ones each session?" If they have some, save them. If not, the agent finds relevant subs automatically before each session.
3. **Voice** — "want me to match your Reddit writing style? paste 8-10 of your comments and I'll learn your tone. if not, I'll use a natural casual voice." If yes, follow `personalization/voice-samples.md`. If no, use the built-in style from `rules/style-guide.md`.

After setup, go straight into the first session — don't stop and wait.

## Routing

| User says | Action |
|---|---|
| "set up [company]" / "new profile" | Follow `workflows/setup-profile.md` |
| "do today for [company]" / "fill quota" | Follow `workflows/batch-mode.md` |
| "create posts" / "write reddit posts" | Follow `workflows/value-posts.md` |
| "learn my style" / pastes comments | Follow `personalization/voice-samples.md` |
| "show progress" | Display `tracking/{YYYY-MM-DD}.md` |
| "check engagement" | Run engagement review in `workflows/batch-mode.md` |

## How It Works — End to End

The agent does everything autonomously. The user does NOT need to find posts, pass URLs, or prepare anything. The full cycle:

1. **Research** — study subreddits, find trending posts, read threads
2. **Write** — draft comments using the right angle, tone, and style
3. **Review** — self-critique against spam signals, present best options
4. **Post** — after user confirms, post the comment directly
5. **Track** — log everything, check engagement later, learn from results

The user only needs to confirm before posting. Everything else is autonomous.

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

1. **Load profile** from `profiles/`. If missing, run First Session Flow above. If profile's `Product Knowledge` > 2 weeks old, re-visit the product website first.
2. **Find subreddits** — if profile has target subs, use those. If not (or user said "search for me"), search Reddit for relevant communities based on product category. Evaluate fit and save good ones.
3. **Study subreddit** — see `workflows/batch-mode.md` Subreddit Study. Skip if `tracking/insights.md` has fresh data (< 3 days).
4. **Search and select posts** — browse new/rising/hot in target subs. Pick best-fit posts autonomously. Skip posts in `tracking/` from last 7 days. Read full thread + top comments.
5. **Draft comments** — apply `rules/style-guide.md`, `rules/comment-angles.md`, voice personalization, and subreddit insights. Present top options with recommended pick.
6. **Self-critique** against `rules/spam-signals.md`. Discard any that fail.
7. **Post** after user confirms. Log to `tracking/{YYYY-MM-DD}.md` per `tracking/FORMAT.md`.
