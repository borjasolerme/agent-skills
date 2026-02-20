# Batch Mode

Triggered by "do today for [company]", "fill quota", or similar. This workflow fills the daily comment quota for a company profile across all its target subreddits.

---

## Prerequisites

1. **Load profile:** Read `profiles/{slug}.md` for the requested company. If not found, prompt the user to run setup first ("no profile found for {company} — want to set one up?").
2. **Load today's tracking file:** Read `tracking/{YYYY-MM-DD}.md` (today's date). If it doesn't exist, this is the first session today — the file will be created after the first comment.
3. **Load reference files once:** Read `rules/comment-angles.md` and `rules/style-guide.md` at session start. Do not re-read these mid-session.
4. **Load personalization (if exists):** Check if `personalization/voice-samples.md` has a Voice Analysis section. If populated, read it once and apply during drafting.
5. **Calculate remaining quota:** For each target subreddit in the profile, subtract comments already logged today from the daily limit.

---

## Session Plan

Present the user with a status overview before starting:

```
Today's plan for {product name}:

r/{sub_1}: {done}/{limit} — {remaining} to go
r/{sub_2}: {done}/{limit} — {remaining} to go
...
Total: {total_remaining} comments remaining
```

If all quotas are filled, report that and ask if the user wants to do extra.

---

## Per-Subreddit Loop

For each subreddit with remaining quota:

### 1. Find Candidate Posts

- Navigate to the subreddit sorted by **new** or **rising** (alternate between sessions)
- Identify 2-3 candidate posts that match the profile's "good post types"
- **Filter out:**
  - Posts already commented on (check URLs in tracking files from the last 7 days)
  - Posts older than 24 hours (diminishing visibility)
  - Posts that are a poor fit for the product
  - Posts with fewer than 2 comments (too early, low engagement signal)

### 2. Present Candidates

Show the user 2-3 candidates with:
- Post title
- Brief summary (1 sentence)
- Why it's a good fit
- Estimated angle

The user picks one, or skips all (move to next subreddit).

### 3. Read the Thread

Navigate to the selected post. Read the full post body and top comments using browser automation (see SKILL.md for tool mapping). Identify:
- What the person is actually asking or struggling with
- What existing comments have already said (don't repeat)
- Whether the product fits naturally

### 4. Generate 3 Drafts

Write **3 drafts** (not 5 — token-efficient for batch mode). Each draft should:
- Use a different angle from the profile's preferred angles
- Apply voice personalization if available
- Follow the style guide

### 5. Critique and Present Top 2

Evaluate each draft against the spam signals checklist. Present the **top 2** with:
- The recommended pick clearly marked
- Angle used
- Word count
- Whether it mentions the product

### 6. Post with Confirmation

Only after the user picks a draft and confirms:
1. Post the comment using browser automation (see SKILL.md for posting flow)
2. Wait for confirmation that the comment was posted

### 7. Log to Tracking

Append the comment to `tracking/{YYYY-MM-DD}.md`. See **Tracking Format** below.

---

## Subreddit Transition

After completing a subreddit's quota:

1. Report progress: "r/{sub}: {done}/{limit} complete"
2. If more subreddits remain, tell the user: "moving to r/{next_sub} — good to take a 2-5 minute break between subs to keep posting patterns natural"
3. During the wait, pre-scan the next subreddit for candidate posts

---

## Termination Conditions

Stop the batch session when any of these are true:

- All subreddit quotas are filled
- User says "stop", "done", or "that's enough"
- No suitable posts remain in any subreddit
- 3 consecutive skips or failures (user skipped all candidates 3 times in a row)

---

## Session Summary

At the end of the session, read the tracking file and present:

```
Session complete for {product name}:

r/{sub_1}: {done}/{limit}
r/{sub_2}: {done}/{limit}
...
Total: {total_done} comments posted
Product mentioned: {count}/{total_done}
Angles used: {list}
```

---

## Duplicate Prevention

Before selecting any candidate post, check tracking files from the **last 7 days** for the post URL:

```
tracking/{YYYY-MM-DD}.md   (today)
tracking/{YYYY-MM-DD}.md   (yesterday)
...
tracking/{YYYY-MM-DD}.md   (7 days ago)
```

If the URL appears in any file, skip that post.

---

## Tracking Format

Each daily tracking file (`tracking/YYYY-MM-DD.md`) follows this format:

```markdown
# {YYYY-MM-DD} — {product name}

**Total:** {n} comments
**Quota progress:** r/{sub_1}: {done}/{limit} | r/{sub_2}: {done}/{limit}

---

## 1. r/{subreddit} — {HH:MM}

- **Post:** [{post title}]({post URL})
- **Angle:** {Helper/Tool List/Experience Share/Follow-up Question/Contrarian}
- **Product mentioned:** {yes/no}
- **Word count:** {n}

> {full comment text}

---

## 2. r/{subreddit} — {HH:MM}

...
```

Update the **Total** and **Quota progress** lines in the header after each new comment.
