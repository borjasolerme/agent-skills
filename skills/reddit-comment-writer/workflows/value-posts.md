# Value Posts

Creates original Reddit posts that share genuine value. No product mentions. Triggered by "create posts" or "write reddit posts".

## Prerequisites

1. Load `profiles/{slug}.md`. Posts draw from the product's domain expertise but are NOT promotional.
2. Load tracking files (today + last 7 days) for knowledge base.
3. Load `rules/style-guide.md` and `rules/spam-signals.md`.
4. Load `personalization/voice-samples.md` if Voice Analysis exists.
5. Load `tracking/post-insights.md` if it exists — apply learnings from past posts.
6. Run **Post Engagement Review** if tracked posts > 24h old lack engagement data.

## 1. Research Top Posts

Study what's getting upvoted in each target subreddit right now. Not optional.

- Fetch 10-15 top posts from last week per sub.
- Note: title style, length, format, opening hook, closing, upvotes, flair.
- Identify patterns: what titles work, what length, stories vs how-tos, hot topics vs overdone.
- Save to `tracking/post-insights.md`.

**Progressive learning:**
- First session: full research, lean on format table below.
- 3+ posts tracked: compare your performance to top posts, favor what worked.
- 10+ posts tracked: quick refresh only (skim 5 posts for trends). Lead with your own data.

## 2. Build Knowledge Map

From tracked threads (7 days), extract: recurring questions, common pain points, bad advice patterns, gaps, winning formats. Cross-reference with `tracking/post-insights.md` trends.

## 3. Generate 3 Post Ideas

Each targets a different subreddit. Pick format based on knowledge + what works per `tracking/post-insights.md`:

| Format | When to use |
|---|---|
| **Lessons learned** | Same mistake repeated across threads |
| **How-to breakdown** | Recurring question deserves standalone answer |
| **Myth buster** | Bad advice circulating |
| **Data/results share** | Can compile insights from multiple threads |
| **Resource roundup** | People keep asking for tools/resources |

Present ideas with: subreddit, title, format, 1-sentence basis. Wait for approval.

## 4. Draft Each Post

- Match tone/length/structure of top posts in that sub (from research + `tracking/post-insights.md`).
- All lowercase (except proper nouns). No marketing language.
- 150-400 words. Short paragraphs. Open with insight, not preamble. End with question.
- **NO product mention.** NO links. Suggest flair if applicable.
- Quality check: could a non-seller write this? Specific insight included? Worth saving/sharing?

Present all 3 drafts. Wait for approval.

## 5. Post + Log

Post one at a time after explicit confirmation. 3-5 min between posts. Log per `tracking/FORMAT.md` with `Type: VALUE POST`.

## Post Engagement Review

Run if tracked posts > 24h old lack engagement data. Posts need more time than comments.

1. Fetch each tracked post via API. Record: upvotes, ratio, comments, removed, top reply themes.
2. Update tracking entries. Analyze: best formats, title patterns, length sweet spots, topics that resonated/flopped.
3. Update `tracking/post-insights.md` with learnings.
4. Present summary: per-sub performance, best/worst posts, format insights.

## Timing

- Max 3 value posts/day. 3-5 min spacing.
- Best after a comment session or standalone.
- Check sub active hours (generally weekday mornings EST for business subs).
