# Setup Profile

Creates a new company profile. Triggered by "set up [company]" or "new profile".

Ask each group of questions together, wait for answers before proceeding.

## Step 1: Core Info

1. Product name
2. URL (remind: space before TLD, e.g., "acmeapp .com")
3. One-sentence description

## Step 2: Category, Competitors, Talking Points

1. Category (e.g., video ads, form builder, AI agents)
2. 2-4 real competitors — name + what each is best at
3. 2-4 true talking points worth mentioning (e.g., "free tier includes X", "saves ~N hours/week")

## Step 3: Target Subreddits

For each sub: name, daily limit (1-3), community notes (tone, rules), good post types. If user isn't sure about community notes, offer to figure it out by reading the sub later.

## Step 4: Preferred Angles

Show the 5 angles (Helper, Tool List, Experience Share, Follow-up Question, Contrarian). User picks 2-3 best for their product.

## Step 5: Things to Never Say

Optional. Ask for comparisons to avoid, false claims, framings to skip.

## Step 6: Product Deep Dive

Visit the product URL. Read homepage, features, pricing. Save to `Product Knowledge` section in the profile:
- What it does (own words, not marketing copy)
- Key features relevant to Reddit conversations
- Pricing/free tier
- UI/UX notes
- Anything surprising or noteworthy

Re-visit every 2 weeks or when user mentions new features.

## Step 7: Save Profile

Derive slug (lowercase, hyphens). Fill `profiles/_template.md`. Write to `profiles/{slug}.md`.

## Step 8: Offer Personalization

Ask if they want to paste 8-10 Reddit comments for voice analysis. If yes, follow `personalization/voice-samples.md`. If no, confirm setup complete.
