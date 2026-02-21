# Setup Product Profile

Interactive flow to create a product profile. Ask questions together, wait for answers before proceeding.

---

## Step 1 — Visit the product URL

User provides a URL. Use browser automation to visit it and read the page content.

1. Open the URL with browser automation
2. Read the full page — extract: product name, tagline, description, features, pricing, team info, social links
3. Take a screenshot of the homepage for reference

---

## Step 2 — Ask clarifying questions

Based on what you found, ask the user to confirm or fill gaps. Ask these together:

1. **Product name** — confirm what you found
2. **Tagline** — one-liner, confirm or ask for one
3. **Category** — suggest based on page content (e.g., AI, SaaS, Developer Tools, Productivity)
4. **Pricing** — confirm what you found (free, freemium, paid, enterprise)
5. **Key features** — list 3-5 you found, ask user to confirm or edit
6. **Target audience** — who is this for?

Wait for answers.

---

## Step 3 — Generate descriptions

Generate three versions of the product description:

- **Short** (~50 chars) — for tight character limits
- **Medium** (~150 chars) — for most directory fields
- **Long** (~500 chars) — for directories that allow more detail

Show all three to the user. Ask if they want edits. Wait for approval.

---

## Step 4 — Image handling

Ask the user:

> Do you have a product logo or screenshot to use? If yes, provide the file path. If not, I'll use the homepage screenshot from Step 1.

If user provides a path → save it in the profile.
If not → use the screenshot taken in Step 1, save to `profiles/{slug}-screenshot.png`.

---

## Step 5 — Save profile

Derive slug from product name: lowercase, hyphens, no special chars.

Write profile to `profiles/{slug}.md` using this format:

```markdown
# {Product Name}

- **URL:** {url}
- **Category:** {category}
- **Pricing:** {pricing}
- **Target audience:** {audience}

## Descriptions

- **Short:** {short description}
- **Medium:** {medium description}
- **Long:** {long description}

## Key Features

- {feature 1}
- {feature 2}
- {feature 3}

## Image

- **Path:** {image path or screenshot path}

## Team / Founder

- {name, role — if available}

## Social Links

- {any links found on the page}
```

Tell the user: profile saved, they can now run "submit {product name} to directories".
