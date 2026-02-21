---
name: directory-submitter
description: Submit products to AI/startup directories using browser automation. Supports interactive product profiles, homepage screenshots, form filling, and submission tracking. Triggers on "submit [product] to directories", "set up [product] for directories", "show submission progress", "add directory", or when the user shares a directory submission URL.
---

# Directory Submitter

## FIRST — check what the user wants

| User says | Do this, then STOP |
|---|---|
| "set up [product]" / "new product" / shares a product URL | Read `workflows/setup-product.md` and follow it |
| "submit [product]" / "submit to directories" | Read `workflows/submit-mode.md` and follow it |
| "show progress" / "submission status" | Read and display `tracking/{slug}.md` |
| "add directory" / "new directory" | Open `directories/DIRECTORIES.md` and add entry with user |

If none match → show this menu and wait for user choice:

1. **Set up a product** — create a profile from your product URL
2. **Submit to directories** — fill and submit forms via browser
3. **Show progress** — see submission status for a product
4. **Add a directory** — add a new directory to the list

---

## File reference timing

Don't read files in advance — only at the step that needs them.

| File | When |
|---|---|
| `profiles/{slug}.md` | When user mentions a product name |
| `directories/DIRECTORIES.md` | Start of submit-mode |
| `tracking/{slug}.md` | Start of submit-mode, and after each submission |

---

## Browser automation

**Tool priority:** Chrome Extension → Playwright → manual paste

| Action | Chrome Extension | Playwright |
|---|---|---|
| Navigate | `navigate` | `browser_navigate` |
| Read page | `read_page` | `browser_snapshot` |
| Find element | `find` | _(snapshot refs)_ |
| Click | `computer` (left_click) | `browser_click` |
| Type | `form_input` / `computer` (type) | `browser_type` |
| Screenshot | `computer` (screenshot) | `browser_take_screenshot` |
| Upload file | `upload_image` | `browser_file_upload` |

**Chrome Extension setup:** `tabs_context_mcp` → `tabs_create_mcp` → use `tabId` for all calls.

Minimize tokens: pass only concise instructions. Navigate directly to URLs, never click links.

---

## Quick process overview

1. **Set up** — visit product URL, extract info, ask clarifying questions, generate descriptions, save profile
2. **Submit** — load profile + directory list, navigate to each directory, fill form, confirm with user, log result
3. **Track** — persistent markdown file per product, updated after each submission
