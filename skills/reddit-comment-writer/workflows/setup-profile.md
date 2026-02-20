# Setup Profile

Interactive flow for creating a new company profile. Triggered when the user says "set up [company]", "new profile", or similar.

---

## Step 1: Core Product Info

Ask the user these three questions together:

1. **Product name** — what's the product called?
2. **URL** — what's the domain? (remind them: space before TLD, e.g., "acmeapp .com")
3. **One-sentence description** — what does it do and who is it for?

Wait for answers before proceeding.

---

## Step 2: Category, Competitors, and Talking Points

Ask these three together:

1. **Category** — what space is this in? (e.g., video ads, form builder, spend management, AI agents)
2. **Competitors** — name 2-4 real alternatives and briefly say what each is best at. These will be mentioned alongside the product in comments for authenticity.
3. **Key talking points** — what are 2-4 true, useful things worth mentioning? (e.g., "free tier includes X", "saves ~N hours/week", "works with Y")

Wait for answers before proceeding.

---

## Step 3: Target Subreddits

Ask the user to list the subreddits they want to engage in. For each subreddit, collect:

1. **Subreddit name** (e.g., r/SaaS, r/smallbusiness)
2. **Daily comment limit** (recommend 1-3 per sub)
3. **Community notes** — any context about tone, rules, what gets upvoted
4. **Good post types** — what kind of posts to look for (e.g., "how do I..." questions, tool recommendations)

If the user isn't sure about community notes, suggest: "I can help figure this out later by reading the sub."

Wait for answers before proceeding.

---

## Step 4: Preferred Angles

Show the user the 5 angles and ask which 2-3 work best for their product:

> Here are the comment angles we can use. Pick 2-3 that fit best for {product name}:
>
> 1. **Helper** — answer their question, mention product as one option
> 2. **Tool List** — curated list of 4-6 tools including yours
> 3. **Experience Share** — personal story, product comes up naturally
> 4. **Follow-up Question** — engage genuinely, product only if relevant
> 5. **Contrarian** — different perspective, product as evidence
>
> Which work best? I'll prioritize these when writing comments.

Wait for answers before proceeding.

---

## Step 5: Things to Never Say

Ask:

> Anything I should **never** say or claim about {product name}? For example:
> - Comparisons to avoid ("don't compare to X — they have fans in r/subreddit")
> - Claims that aren't true yet ("don't say we have enterprise features")
> - Framings to avoid ("don't call it AI-powered — users associate that with slop")
>
> This is optional — skip if nothing comes to mind.

Wait for answer (or skip confirmation) before proceeding.

---

## Step 6: Create the Profile File

1. Derive the slug: lowercase the product name, replace spaces with hyphens, remove special characters (e.g., "Acme App" → `acme-app`)
2. Read the template from `profiles/_template.md`
3. Fill in all sections with the user's answers
4. Write the completed profile to `profiles/{slug}.md`
5. Confirm to the user: "Profile saved to `profiles/{slug}.md`. You can edit it anytime."

---

## Step 7: Offer Personalization

After saving the profile, ask:

> Want me to learn your Reddit writing voice too? If you paste 8-10 of your Reddit comments, I can analyze your style and make drafts sound more like you.
>
> You can do this now or later — just say "learn my style" anytime.

If the user wants to proceed, direct them to paste comments and follow the flow in [voice-samples.md](../personalization/voice-samples.md).

If they skip, confirm the setup is complete and remind them they can use the profile with "do today for {product name}" or by sharing a Reddit URL.
