# Value Posts

Triggered by "create posts", "write reddit posts", "post value content", or at the end of a batch session. Creates 3 original Reddit posts across different subreddits that share genuine value based on knowledge accumulated from reading threads.

---

## Prerequisites

1. **Load profile:** Read `profiles/{slug}.md` for the active company. Posts are informed by the product's domain expertise but are NOT promotional.
2. **Load today's tracking file:** Read `tracking/{YYYY-MM-DD}.md` to review all threads read and comments written today.
3. **Load last 7 days of tracking:** Scan `tracking/` for recent files to build a bigger knowledge base of threads, questions, and patterns observed.
4. **Load style references:** Read `rules/style-guide.md` and `rules/spam-signals.md`.
5. **Load personalization (if exists):** Check `personalization/voice-samples.md` for Voice Analysis.

---

## Step 1. Build a Knowledge Map

From all tracked threads (today + last 7 days), extract:

- **Recurring questions** — what do people keep asking about?
- **Common pain points** — what frustrations come up repeatedly?
- **Bad advice patterns** — what wrong or outdated advice keeps getting upvoted?
- **Gaps** — what topics get asked about but never get a solid answer?
- **Winning post patterns** — what format, length, and tone got the most engagement in the threads you've seen?

Summarize this as a short internal list (not shown to the user yet).

---

## Step 2. Generate 3 Post Ideas

Each post must target a **different subreddit** from the profile's target list. For each post, pick the format that best fits the knowledge found:

### Post Formats (pick the best fit per post)

| Format | When to use | Example title pattern |
|---|---|---|
| **Lessons learned** | You've seen the same mistake repeated across threads | "things i wish i knew before [doing X]" |
| **How-to breakdown** | A recurring question deserves a thorough standalone answer | "how we [solved X] — step by step" |
| **Myth buster** | Bad advice keeps circulating | "unpopular opinion: [common belief] is wrong and here's why" |
| **Data/results share** | You can compile real insights from multiple threads | "i reviewed [N] threads about [topic] — here's what actually works" |
| **Resource roundup** | People keep asking for tools/resources | "the actual tools people are using for [X] in 2026" |

Present the 3 ideas to the user:

```
post ideas based on what i've read this week:

1. r/{sub_1} — "{title idea}"
   format: {format name}
   based on: {1-sentence explanation of what knowledge this draws from}

2. r/{sub_2} — "{title idea}"
   format: {format name}
   based on: {1-sentence explanation}

3. r/{sub_3} — "{title idea}"
   format: {format name}
   based on: {1-sentence explanation}
```

Wait for user approval or edits before drafting.

---

## Step 3. Draft Each Post

For each approved idea, write a full post draft. Follow these rules:

### Writing Rules

- **Match the voice of top posts in that subreddit.** Before drafting, navigate to the target subreddit and read 2-3 of the most upvoted recent posts. Match their tone, length, and structure.
- **All lowercase** (except proper nouns) — same as comment style guide.
- **No marketing language, no hype, no corporate tone.**
- **Length:** 150-400 words. Long enough to be useful, short enough to get read.
- **Structure:** Short paragraphs (1-3 sentences), double line breaks between thought groups. Use bullet lists only when listing specific items.
- **Open with the insight, not a preamble.** No "hey everyone, i wanted to share..." — jump straight into the value.
- **End with a question** to invite discussion. Posts that ask a genuine question get more engagement.
- **NO product mention in the post body.** These posts are pure value. The product connection is in your profile/comment history, not in the post itself. If someone asks in the comments, the user can reply naturally then.
- **NO links in the post.** Links trigger spam filters and reduce reach.
- **Flair:** suggest appropriate flair if the subreddit uses it.

### Quality Checks

Before presenting each draft, verify:

1. Could this have been written by someone with no product to sell? If no, rewrite.
2. Does it contain a specific insight, number, or example? Generic advice fails.
3. Would someone save or share this post? If not, add more substance.
4. Does it match the tone of top posts in that subreddit?
5. Does it end with something that invites replies?

---

## Step 4. Present Drafts for Review

Show all 3 drafts together:

```
draft 1 — r/{sub_1}: "{title}"
format: {format} | words: {n}

{full post text}

---

draft 2 — r/{sub_2}: "{title}"
...
```

Wait for the user to approve, edit, or reject each one.

---

## Step 5. Post with Confirmation

For each approved draft:

1. Navigate to the target subreddit
2. Click "Create Post"
3. Enter the title and body
4. Set flair if suggested and available
5. Show a preview and ask for final confirmation before submitting
6. Submit only after explicit "yes"

Post one at a time. Wait 3-5 minutes between posts to keep patterns natural.

---

## Step 6. Log to Tracking

Append each post to `tracking/{YYYY-MM-DD}.md` using this format:

```markdown
### Post {n}. r/{subreddit} — {HH:MM}

- **Type:** VALUE POST
- **Post URL:** {url after posting}
- **Title:** {title}
- **Format:** {Lessons learned/How-to/Myth buster/Data share/Resource roundup}
- **Product mentioned:** No
- **Word count:** {n}
- **Based on:** {brief note on what threads/knowledge informed this post}

> {full post text}
```

Update the session summary header to include value posts count.

---

## Timing and Frequency

- **When to run:** ideally after a comment session, or as a standalone session
- **Frequency:** max 3 value posts per day across all subreddits
- **Spacing:** 3-5 minutes between posts
- **Best times:** check each subreddit's active hours — generally weekday mornings (EST) for business subs

---

## Why This Works

Value posts serve two purposes:

1. **Build karma and credibility** — the account looks like a genuine contributor, not just a commenter dropping product names
2. **Create natural opportunities** — when a value post gets engagement, people check your profile and reply. That's where organic product conversations happen without any shilling.

This directly supports the 90/10 rule from `spam-signals.md`. Value posts are the 90%.
