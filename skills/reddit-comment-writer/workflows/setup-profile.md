# Setup Profile

Creates a new company profile. Ask each group together, wait for answers before proceeding.

## Step 1: Core Info

1. Product name
2. URL (remind: space before TLD, e.g., "acmeapp .com")
3. One-sentence description
4. Category (e.g., video ads, form builder, AI agents)

## Step 2: Product Deep Dive

Visit the product URL immediately. Read homepage, features, pricing. Save to `Product Knowledge` section in the profile:
- What it does (own words, not marketing copy)
- Key features relevant to Reddit conversations
- Pricing/free tier
- UI/UX notes
- Anything surprising or noteworthy

Re-visit every 2 weeks or when user mentions new features.

## Step 3: Competitors and Talking Points

1. 2-4 real competitors — name + what each is best at
2. 2-4 true talking points worth mentioning (e.g., "free tier includes X", "saves ~N hours/week")
3. Things to never say — optional. Comparisons to avoid, false claims, framings to skip.

## Step 4: Target Subreddits

Ask: "do you have specific subreddits in mind, or should I find the best ones for your product?"

- **User has subs:** collect name, daily limit (1-3), community notes, good post types per sub.
- **Auto-discovery:** save no subs. The agent searches for relevant communities before each session based on category and competitors. Good subs get saved to the profile after being scored.

## Step 5: Preferred Angles

Show the 5 angles (Helper, Tool List, Experience Share, Follow-up Question, Contrarian). User picks 2-3 best for their product.

## Step 6: Voice

Ask: "want me to match your Reddit writing style? paste 8-10 of your comments and I'll learn your tone. if not, I'll use a natural casual voice."

- If yes, follow `personalization/voice-samples.md`.
- If no, use built-in style from `rules/style-guide.md`.

## Step 7: Save + Start

Derive slug (lowercase, hyphens). Fill `profiles/_template.md`. Write to `profiles/{slug}.md`. Then go straight into the first session — follow `workflows/batch-mode.md`.
