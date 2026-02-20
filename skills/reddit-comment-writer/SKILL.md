---
name: reddit-comment-writer
description: Write authentic Reddit comments that naturally mention a product without sounding spammy. Supports company profiles, batch mode ("do today for [company]"), activity tracking, and voice personalization. Triggers on "write a reddit comment", "reply to this reddit post", "set up [company]", "do today for [company]", "fill quota", "learn my style", "show progress", or when the user shares a Reddit URL.
---

# Reddit Comment Writer

Write replies that genuinely help the conversation while naturally weaving in the user's product as one option among several. Golden rule: if a comment sounds like an ad, it fails. Every reply must pass as peer advice from someone who happens to use the product.

## Structure

- `rules/` - Writing rules and quality checks
  - `style-guide.md` - Voice, formatting, capitalization, tone, do/don't examples
  - `comment-angles.md` - 5 comment angles with patterns and real-world examples
  - `spam-signals.md` - Spam patterns to avoid, anti-patterns, red flags
- `workflows/` - Multi-step flows
  - `setup-profile.md` - Interactive company profile creation
  - `batch-mode.md` - Quota-filling loop across subreddits
- `profiles/` - Company profiles (one per product)
  - `_template.md` - Blank profile schema
  - `{slug}.md` - Filled profiles created via setup flow
- `personalization/` - Optional voice matching
  - `voice-samples.md` - User's Reddit comments + auto-generated Voice Analysis
- `tracking/` - Daily activity logs (auto-created at runtime)
  - `{YYYY-MM-DD}.md` - Per-day comment log with quota progress

## Critical Rules

- **Login Required:** Check Reddit account login status before any posting action
- **Rate Limiting:** Posting too fast risks account restrictions — respect cooldowns between comments
- **Community Rules:** Follow each subreddit's specific rules (check sidebar before first comment)
- **Spam Prevention:** NO copy-pasting the same content across threads. Every comment must be unique
- **Review Required:** If any checklist item from Step 3 is violated, rewrite — never post a failing comment
- **Post Analysis Required:** NEVER write a comment without fully reading the post first. Judging by title alone causes serious errors — always complete Step 1 before drafting

## Intent Detection

| User says | Action |
|---|---|
| "set up [company]" / "new profile" | Read and follow [setup-profile.md](workflows/setup-profile.md) |
| "do today for [company]" / "fill quota" | Read and follow [batch-mode.md](workflows/batch-mode.md) |
| "learn my style" / pastes Reddit comments | Read and follow [voice-samples.md](personalization/voice-samples.md) |
| Shares a Reddit URL | Single-comment flow (continue below) |
| "show progress" / "what did I do today" | Read and display `tracking/{YYYY-MM-DD}.md` (today's date) |

**If the intent matches a row above, follow that workflow only and STOP — do NOT continue to the Process section.**

If no clear intent is detected (user just activated the skill without specifying what to do), check for existing profiles in `profiles/` and present the available options:

> Here's what I can do:
>
> 1. **Write comments** — give me Reddit post URLs and I'll draft replies (or I can find posts for you in your target subreddits)
> 2. **Do today for [company]** — fill your daily comment quota automatically
> 3. **Set up a new profile** — save your product info so you don't repeat it every time
> 4. **Learn your style** — paste some Reddit comments and I'll match your voice
> 5. **Show progress** — see what you've done today
>
> What would you like to do?

Wait for the user's response before proceeding.

## File Reference Timing

Reference each file only at the relevant step — don't read in advance unless noted.

| File | When to read |
|---|---|
| `profiles/{slug}.md` | Input — when company name is mentioned, load profile and skip product questions |
| `rules/style-guide.md` | Step 2 — writing voice, formatting, do/don't examples |
| `rules/comment-angles.md` | Step 2 — 5 angles with patterns and real examples. In batch mode, read once at session start |
| `rules/spam-signals.md` | Step 3 — spam patterns, anti-patterns, red flags |
| `personalization/voice-samples.md` | Step 2 — only if Voice Analysis section is populated. User's voice takes priority over style guide |
| `tracking/{YYYY-MM-DD}.md` | Step 5 — logging. Create if it doesn't exist |

## Browser Automation

**Prefer Chrome Extension** (`mcp__claude-in-chrome__`) → falls back to **Playwright** (`mcp__playwright__`) → falls back to pasted text.

Minimize tokens in all browser calls — pass only concise instructions (e.g., "Navigate to [URL]", "Click comment box", "Type: [text]"). Always navigate directly to URLs instead of clicking links.

| Action | Chrome Extension | Playwright |
|---|---|---|
| Navigate | `navigate` | `browser_navigate` |
| Read page | `read_page` | `browser_snapshot` |
| Find element | `find` (natural language) | _(snapshot refs)_ |
| Click | `computer` (left_click) | `browser_click` |
| Type | `form_input` / `computer` (type) | `browser_type` |

Chrome Extension setup: `tabs_context_mcp` → `tabs_create_mcp` → use `tabId` for all subsequent calls.

## Process

### Input

If the user mentioned a company, check `profiles/{slug}.md` (derive slug: lowercase, hyphens). If found, load it and skip product questions. Otherwise ask for **product name + URL** and **one-sentence description**.

Then determine how to get the Reddit post:

- **User provides URLs:** The user shares one or more Reddit post URLs. Process each one through Steps 1-5.
- **Agent finds posts:** If the user says "find posts" or the profile has target subreddits, navigate to those subreddits (sorted by new/rising), find 2-3 candidate posts that fit the product, present them to the user, and let them pick which to reply to. Filter out posts older than 24h, posts with fewer than 2 comments, and posts already in tracking files from the last 7 days.

### Step 1. Read the Thread

Navigate to the post URL via browser automation. Read the post title, body, and top comments. Identify what the person is asking, what would genuinely help, and whether the product fits naturally.

### Step 2. Generate 5 Drafts

Read [style-guide.md](rules/style-guide.md) and [comment-angles.md](rules/comment-angles.md). If `personalization/voice-samples.md` has a Voice Analysis, read and blend it.

Write 5 drafts, one per angle (Helper, Tool List, Experience Share, Follow-up Question, Contrarian). If the product doesn't fit naturally, write a value-only comment — forcing a mention is worse than skipping it.

### Step 3. Self-Critique and Select

Read [spam-signals.md](rules/spam-signals.md). Evaluate each draft for spam signals, relevance, value, and style. Discard failing drafts. Rewrite the top 3, present ranked with recommended pick marked.

### Step 4. Post the Comment

Only after the user picks a draft and explicitly confirms. Navigate to the post, find the comment box, type the text, verify it reads correctly, ask for final confirmation, then submit.

### Step 5. Log to Tracking

Log the comment to `tracking/{YYYY-MM-DD}.md` (create if needed). Format specified in [batch-mode.md](workflows/batch-mode.md#tracking-format). Include: subreddit, time, post title + URL, angle, product mentioned (yes/no), word count, full comment text.

