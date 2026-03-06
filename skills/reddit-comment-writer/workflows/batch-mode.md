# Batch Mode

Fills the daily comment quota for a company profile. Triggered by "do today for [company]" or "fill quota".

## Prerequisites

1. Load `profiles/{slug}.md`. No profile? Run setup first (see `SKILL.md` First Session Flow).
2. **Find subreddits** if profile has none — search Reddit for communities matching the product category. Evaluate fit, save the best ones to the profile.
3. Load `tracking/{YYYY-MM-DD}.md` (today). Calculate remaining quota per subreddit.
4. Load `rules/comment-angles.md` and `rules/style-guide.md` once.
5. Load `personalization/voice-samples.md` if Voice Analysis exists.
6. Run **Engagement Review** if tracked comments > 12 hours old lack engagement data.
7. Run **Subreddit Study** for any sub with stale insights (> 3 days in `tracking/insights.md`).

## Session Plan

Check `tracking/insights.md` for subreddit scores. Only include eligible subs:
- **A/B:** full quota
- **C:** half quota
- **D:** skip unless user asks
- **F:** never include — suggest removing from profile
- **Unscored** (< 5 comments): full quota

Show plan, then start the loop.

## Per-Subreddit Loop

### 1. Find candidates
Fetch new/rising posts (alternate). Pick 2-3 matching profile's "good post types". Filter out: already tracked (last 7 days), > 24h old, poor fit, < 2 comments.

### 2. Present candidates
Title, 1-sentence summary, why it fits, estimated angle. User picks one or skips.

### 3. Read thread
Full post + top comments via Reddit API (see `SKILL.md` tools). Note: what they need, what's been said, whether product fits.

### 4. Draft 3 comments
One per angle. Prioritize angles that performed well per `tracking/insights.md`. Match subreddit tone/length from study. Apply progressive learning (see `SKILL.md`). Follow `rules/style-guide.md`.

### 5. Critique + present top 2
Check against `rules/spam-signals.md`. Show recommended pick, angle, word count, product mentioned y/n.

### 6. Post + log
Post after user confirms. Log to `tracking/{YYYY-MM-DD}.md` per `tracking/FORMAT.md`.

### 7. Transition
Report progress. Suggest 2-5 min break between subs. Pre-scan next sub during wait.

## Stop When

- All quotas filled
- User says stop
- No suitable posts remain
- 3 consecutive skips

## Session Summary

Show per-sub progress, total comments, product mention count, angles used.

---

## Subreddit Study

Run once per sub before writing. Teaches what works *today* in each community.

1. Fetch 5-10 top/hot posts. Read top 3-5 comments on each.
2. Note: tone, winning length, structure, openers, what gets upvoted, what gets ignored.
3. Save to `tracking/insights.md` under subreddit heading.

**Refresh rules:** Re-study if > 3 days old, or after poor engagement review. Skip if fresh.

---

## Engagement Review

Run at session start if tracked comments > 12h old lack engagement data.

1. Load tracking files (last 7 days). Fetch each comment with a permalink via API.
2. Record: score, reply count, OP replies, removed/flagged.
3. Update tracking entries. Score each subreddit (A-F). Update `tracking/insights.md`.
4. Present summary: best/worst per sub, avg scores, product mention impact, score changes.

### Subreddit Scoring (A-F)

Based on: avg upvotes, reply rate, product mention impact, removals, audience fit.

- **A:** High engagement, mentions welcome. Prioritize.
- **B:** Solid. Keep posting.
- **C:** Mixed. Reduce quota, experiment with angles.
- **D:** Low engagement or hostile to mentions. Rarely post, pure value only.
- **F:** Removals/downvotes/callouts. Stop posting. Suggest replacements.

### Discovering New Subreddits

When D/F subs get dropped, look for replacements via cross-posts, sidebar links, user mentions of other communities. Suggest to user with reason.
