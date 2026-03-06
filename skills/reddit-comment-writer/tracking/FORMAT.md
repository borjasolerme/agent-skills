# Tracking Formats

## Daily Log — `tracking/{YYYY-MM-DD}.md`

```markdown
# {YYYY-MM-DD} — {product name}

**Total:** {n} comments | **Value posts:** {n}
**Quota:** r/{sub_1}: {done}/{limit} | r/{sub_2}: {done}/{limit}

---

## 1. r/{subreddit} — {HH:MM}

- **Post:** [{title}]({url})
- **Comment:** [{permalink}]({comment url})
- **Angle:** {Helper/Tool List/Experience Share/Follow-up Question/Contrarian}
- **Product mentioned:** {yes/no}
- **Word count:** {n}
- **Engagement:** _pending review_ | {score} upvotes, {n} replies

> {full comment text}
```

For value posts, use the same format but add:
- **Type:** VALUE POST
- **Format:** {Lessons learned/How-to/Myth buster/Data share/Resource roundup}

## Insights — `tracking/insights.md`

```markdown
# Subreddit Insights

## Rankings

| Subreddit | Score | Comments | Avg upvotes | Mention impact | Status |
|---|---|---|---|---|---|
| r/{sub} | {A-F} | {n} | {n} | {+/-/neutral} | {active/paused/dropped} |

## r/{subreddit}

**Updated:** {YYYY-MM-DD} | **Score:** {A-F}

- **Winning tone:** {description}
- **Winning length:** {range}
- **Winning patterns:** {what gets upvoted}
- **Avoid:** {what doesn't work}
```

## Post Insights — `tracking/post-insights.md`

```markdown
# Post Insights

## r/{subreddit}

**Updated:** {YYYY-MM-DD} | **Posts tracked:** {n} yours, {n} studied

- **Best format:** {format + evidence}
- **Title style:** {pattern}
- **Length:** {range}
- **Best topics:** {list}
- **Avoid:** {what doesn't work}
- **Your top:** ({upvotes}) "{title}" — {format}
- **Your worst:** ({upvotes}) "{title}" — {format}, likely because: {reason}
```
