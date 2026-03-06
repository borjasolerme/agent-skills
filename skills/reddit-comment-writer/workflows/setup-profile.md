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

Ask: "do you have specific subreddits in mind, or should I find the best ones for your product?"

- **User has subs:** collect name, daily limit (1-3), community notes, good post types per sub.
- **User wants auto-discovery:** save no subs in profile. The agent will search Reddit for relevant communities before each session based on product category and competitors. Good subs discovered this way get saved to the profile automatically after being scored.

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
