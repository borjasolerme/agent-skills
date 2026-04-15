# Coding Workflow Examples

These examples show the expected behavior of this skill. Follow the pattern, not the exact code.

## 1. Think Before Coding

### Example 1: Hidden Assumptions

**User Request:** "Add a feature to export user data"

### X What LLMs Do (Wrong Assumptions)

```ts
export async function exportUsers() {
  const users = await db.user.findMany();

  const csv = users.map((user) => ({
    id: user.id,
    email: user.email,
  }));

  await writeFile("./users.csv", stringify(csv));

  return { ok: true };
}
```

Problems:

- Assumed it should export all users
- Assumed CSV instead of clarifying the output format
- Assumed which fields should be included
- Assumed a file should be written on the server
- Ignored privacy, permissions, and scale concerns

### Check What Should Happen

```md
Before implementing, clarify the request:

1. Should this export all users or only a filtered subset?
2. Which fields are allowed to be exported?
3. Should the export download in the browser, run as a background job, or send by email?
4. Who is allowed to perform the export?
5. What format is needed: CSV, JSON, or something else?
```

## 2. Reuse Existing UI

### Example 2: Do Not Invent New Components

**User Request:** "Clean up the settings screen"

### X What LLMs Do (Wrong Assumptions)

```tsx
export function FancySettingsCard() {
  return (
    <div className="rounded-3xl bg-gradient-to-br from-blue-500 to-cyan-400 p-6 shadow-2xl">
      <button className="inline-flex rounded-full bg-black px-5 py-3 text-white">
        Save Changes
      </button>
    </div>
  );
}
```

Problems:

- Added gradients that may not exist in the app
- Invented a new card style instead of reusing the current one
- Invented a custom button instead of reusing the app button
- Changed the visual language instead of following it

### Check What Should Happen

```md
During implementation:

1. Inspect the existing settings page and current design primitives.
2. Reuse the existing card, button, input, modal, and layout components.
3. Reuse current colors, spacing, shadows, and typography.
4. Do not add gradients or decorative styling unless the app already uses them.
5. Keep the change visually consistent with the rest of the product.
```

## 3. Use TDD for Normal Changes

### Example 3: Vertical Slices, Not Test-After

**User Request:** "Expired coupons should not reduce the cart total"

### X What LLMs Do (Wrong Assumptions)

```md
1. Implement coupon expiration handling.
2. Implement error messages.
3. Update totals.
4. Add a few tests afterwards.
```

Problems:

- Implementation came before the first failing test
- Multiple behaviors were changed at once
- The test plan is vague and likely low-signal
- This is not a red-green-refactor loop

### Check What Should Happen

```md
Use one vertical slice at a time:

1. Confirm the first public behavior to prove:
   "Expired coupons show an error and do not reduce the total."
2. Write one failing test for that behavior.
3. Implement the minimum code to make the test pass.
4. Run the test and get back to green.
5. Only then choose the next behavior to prove.
```

## 4. Avoid Unnecessary Effects

### Example 4: Do Not Reach for useEffect First

**User Request:** "Keep the selected tab in sync with the URL"

### X What LLMs Do (Wrong Assumptions)

```tsx
const [selectedTab, setSelectedTab] = useState("overview");

useEffect(() => {
  if (pathname.includes("/settings")) setSelectedTab("settings");
  if (pathname.includes("/billing")) setSelectedTab("billing");
}, [pathname]);
```

Problems:

- Duplicated state that can drift from the route
- Added synchronization logic that may not be needed
- Reached for `useEffect` before checking simpler options

### Check What Should Happen

```md
Before adding an effect:

1. Check whether the selected tab can be derived directly from the route.
2. If local state is still needed, update it in the user action that changes it.
3. Use `useEffect` only when synchronizing with something outside React.
4. Read `react-effects.md` before committing to an effect-based solution.
```

## 5. Prefer Agent Browser for Browser Validation

### Example 5: Use the Right Browser Tool

**User Request:** "Fix the drag-and-drop board layout"

### X What LLMs Do (Wrong Assumptions)

```md
I changed the drag logic and ran unit tests.
It should be fine now.
```

Problems:

- No real browser validation
- No visual confirmation that drag-and-drop works
- No check for overlap, clipping, or layout regressions

### Check What Should Happen

```md
After implementation:

1. Test isolated logic with unit tests where appropriate.
2. Use `agent-browser` as the default browser automation tool for interactive validation.
3. Verify the drag interaction actually works in the UI.
4. Confirm layout and visual regressions with snapshots or screenshots.
5. Use Playwright only if the repo already relies on it for committed browser tests or the task explicitly requires it.
```

## 6. Debug by Finding the Truth

### Example 6: Do Not Blindly Retry

**User Request:** "The invite flow works locally but fails in production"

### X What LLMs Do (Wrong Assumptions)

```md
1. Re-run the same test.
2. Restart the app.
3. Change a few things that might help.
4. Hope the failure disappears.
```

Problems:

- No concrete hypothesis
- No instrumentation
- No root-cause investigation
- High risk of a patchy fix

### Check What Should Happen

```md
Debugging workflow:

1. Read the relevant code path carefully.
2. Form a concrete hypothesis about the failure.
3. Liberally add temporary logging statements anywhere in the codebase to verify logic works as you expect.
4. Compare observed behavior with expected behavior.
5. Fix the root cause, not just the symptom.
6. Remove temporary debugging code before finishing and do not commit it.
```

## 7. Review for Reuse and Simplicity

### Example 7: Avoid the Quick Fix

**User Request:** "Ship the fix quickly"

### X What LLMs Do (Wrong Assumptions)

```ts
// TODO: clean this later
// special case for this screen only
if (pathname === "/settings" && user?.role === "admin" && flag !== "legacy") {
  setTimeout(() => {
    refetch();
  }, 250);
}
```

Problems:

- Hard-coded and brittle
- Poorly explained intent
- Likely to confuse the next agent
- Optimized for speed now, not maintainability

### Check What Should Happen

```md
Before finishing, review:

1. Is this reusable and understandable?
2. Does it follow existing components and patterns?
3. For React and Next.js work, does it follow `vercel-react-best-practices`?
4. Did we keep the implementation simple instead of over-engineered?
5. Will another agent understand the intent quickly?
```
