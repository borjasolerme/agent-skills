# Submit Mode

Per-directory submission loop with browser automation.

---

## Prerequisites

1. Read `profiles/{slug}.md` — if it doesn't exist, run setup-product first
2. Read `directories/DIRECTORIES.md` — get the full directory list
3. Read `tracking/{slug}.md` — if it exists, check what's already submitted

---

## Step 1 — Show status

Display a summary table:

```
Product: {name}
Profile: profiles/{slug}.md

| Directory | Status |
|---|---|
| Product Hunt | submitted 2026-02-15 |
| There's An AI For That | pending |
| Ben's Bites | not started |
```

Ask the user which directory to submit to next, or offer to go through remaining ones in order.

---

## Step 2 — Per-directory submission

For each directory the user wants to submit to:

### 2a. Show field mapping

Read the directory entry from DIRECTORIES.md. Show what fields are needed and what we have from the profile:

```
Directory: {name}
URL: {submission URL}

| Field | Required | Value from profile |
|---|---|---|
| Name | yes | {product name} |
| Description | yes | {medium or short, depending on limit} |
| URL | yes | {product URL} |
| Logo | no | {image path} |
```

Ask the user to confirm or override any values before proceeding.

### 2b. Navigate and fill

1. Open the submission URL with browser automation
2. Read the page to identify form fields
3. Fill each field using the mapped values
4. Upload image if the form has a file upload field
5. **STOP before clicking submit** — show the user what was filled

### 2c. Confirm and submit

Ask the user: "Ready to submit? (yes / edit / skip)"

- **yes** → click submit, wait for confirmation page
- **edit** → user specifies what to change, re-fill
- **skip** → move to next directory

### 2d. Log result

After submission, update `tracking/{slug}.md`:

- Add a row with: directory name, "submitted", today's date, any confirmation URL, notes
- If the directory showed an error, log "failed" with the error message

---

## Step 3 — Session summary

After the user is done (no more directories or they say stop), show:

```
Session complete.

Submitted: {n} directories
Skipped: {n}
Failed: {n}

Updated tracking: tracking/{slug}.md
```

---

## Notes

- Always confirm with user before clicking submit — never auto-submit
- If a directory requires login, tell the user to log in first, then continue
- If a form has unexpected fields not in our profile, ask the user what to fill
- Pick the right description length based on the directory's character limits
