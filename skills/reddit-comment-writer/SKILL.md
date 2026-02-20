---
name: reddit-comment-writer
description: Write authentic Reddit comments that naturally mention a product without sounding spammy. Use this skill when the user wants to reply to a Reddit post or comment thread to engage genuinely while subtly promoting their product. Triggers on requests like "write a reddit comment", "reply to this reddit post", "engage in this thread", or when the user shares a Reddit URL and asks for a comment draft.
---

Read the Reddit post via Playwright MCP browser tools or from pasted text. Write a reply that genuinely helps the conversation while naturally weaving in the user's product as one option among several.

Golden rule: if a comment sounds like an ad, it fails. Every reply must pass as peer advice from someone who happens to use the product.

## Required Tool: Playwright MCP

This skill uses Playwright MCP to interact with Reddit.

| MCP Tool | Purpose |
|---|---|
| `browser_navigate` | Navigate to Reddit pages |
| `browser_snapshot` | Capture page structure (accessibility tree) |
| `browser_click` | Click elements (comment box, buttons) |
| `browser_type` | Input text (comment content) |
| `browser_wait_for` | Wait for page loading |

**Important rules when using Playwright MCP:**
- Minimize tokens: don't pass entire conversation context to MCP calls — only concisely summarize the essential info needed for that action
- Direct navigation: use `browser_navigate` to go to URLs directly rather than clicking links (prevents click errors, saves tokens)
- Concise instructions: pass only minimal instructions like "Navigate to [URL]", "Click [element]", "Type: [text]"
- No screenshots: do NOT use `browser_take_screenshot`. Always use only `browser_snapshot` for page verification (accessibility tree is sufficient)

## Input

Ask the user for anything missing before drafting:

1. **Product name + URL** (e.g., "acmeapp .com")
2. **One-sentence product description**
3. **The Reddit post** (URL preferred — the agent will navigate to it via Playwright)

## Writing Style

Match the casual, lowercase, founder-in-the-trenches tone. For the full style reference with do/don't examples, see [style-guide.md](references/style-guide.md).

Key rules:
- all lowercase except proper nouns
- short sentences, double line breaks between them
- conversational and helpful, never salesy
- product mentioned as one tool among several real alternatives
- no em dashes, no bullet point walls, no corporate language
- URLs with space before TLD (e.g., "acmeapp .com")
- under 250 words, ideally 50-150

<examples>

which is the main problem for you? the script? to make the avatar realistic?

to make the avatar realistic you can use [tool-a] ai model, quite good. for the script the best thing is giving 5 example of working scripts, you can download tiktok videos get the transcript from them and paste them as example to chatgpt.

if you don't want to worry about anything of that, i would say one of the best tools i've found is [your-product]

---

have you tried doing some ads? you can use [your-product], [tool-b] or similar

also, what could work in your case is showcasing your knowledge through linkedin, freebies can be a good option

and a lot of direct outreach

---

at the end small business don't have time to use more tools, it is only going to work if the tool does "everything for them", so here I would go with AI tools

examples:
- chat support: [tool-a]
- automations with [tool-b] or [tool-c]
- video ads: [your-product]

</examples>

Replace `[your-product]` with the real product name. Replace `[tool-x]` with real, well-known tools relevant to the thread.

## Comment Angles

Each draft should use a different angle. For detailed patterns and real-world examples of each, see [comment-angles.md](references/comment-angles.md).

| Angle | Strategy | Product mention |
|---|---|---|
| **Helper** | Answer their question, mention product as one option | Medium |
| **Tool List** | Curated list of 4-6 tools including yours | Medium |
| **Experience Share** | Personal story, product comes up naturally | Low |
| **Follow-up Question** | Engage genuinely, product only if relevant | Minimal/none |
| **Contrarian** | Different perspective, product as evidence | Low |

If the product doesn't fit the conversation naturally, write a value-only comment. Forcing a mention is worse than skipping it.

## Process

### 1. Read the thread (via Playwright)

1. `browser_navigate` to the Reddit post URL
2. `browser_snapshot` to capture the post title, body, and top comments
3. If comments aren't loaded, scroll down and snapshot again

From the snapshot, identify:
- What the person is actually asking or struggling with
- What kind of reply would genuinely help
- Whether mentioning the product fits naturally

### 2. Generate 5 drafts

Write 5 drafts, one per angle (helper, tool list, experience share, follow-up question, contrarian).

### 3. Self-critique and select

Evaluate each draft. For full spam patterns to avoid, see [spam-signals.md](references/spam-signals.md).

| Criterion | Pass if... |
|---|---|
| **Spam** | Could not be mistaken for marketing |
| **Relevance** | Directly addresses the post's topic |
| **Value** | Reader learns something useful even ignoring the product |
| **Style** | Matches the lowercase, casual examples above |

Discard drafts that fail any criterion. Rewrite the top 3, present them ranked with the recommended pick clearly marked.

### 4. Post the comment (optional, only if user confirms)

Only after the user picks a draft and explicitly says to post it:

1. `browser_navigate` to the Reddit post URL (if not already there)
2. `browser_snapshot` to find the comment input box
3. `browser_click` on the comment box
4. `browser_type` the selected comment text
5. `browser_snapshot` to verify the text is correct
6. Ask the user for final confirmation before clicking submit
7. `browser_click` the submit/comment button

## Fallback Templates

If drafts don't feel right, offer these for manual adaptation:

**The Helper:**
[name], [role] at [company].
[One sentence on what worked for you]
Happy to share more if useful.

**The Data Drop:**
[Result] in [timeframe].
Cost: [X] | Time: [X]/week | Stack: [tool/tool/tool]
[One thing that didn't work]. [One fix].

**The Follow-up:**
[Acknowledge their point].
[What worked for you, one sentence].
[Question to keep thread alive]?
