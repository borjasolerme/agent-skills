---
name: coding-workflow
description: Use when implementing, debugging, or reviewing code in an existing app and the user wants simple changes, reuse of existing components and design patterns, strong code quality, TDD-minded testing, and no over-engineering. Also use when deciding how much testing is needed, when validating UI changes with Agent Browser, or when simplifying a spec before coding.
license: MIT
user-invocable: true
argument-hint: [task or change request]
---

# Coding Workflow

Apply these guardrails whenever you are coding, debugging, or reviewing.

For concrete phrasing and example workflows, read `references/examples.md` only when examples would help with the current task.

## Companion skills and tools

If installed and relevant, prefer these helpers:

- `tdd` from `https://github.com/mattpocock/skills` before planning tests or adding tests
- `vercel-react-best-practices` for React and Next.js changes, especially during review
- `frontend-design` during implementation, but only within the app's existing design language
- `emil-design-eng` only when the user explicitly asks for extra UI polish
- `agent-browser` for visual validation, layout checks, canvas, drag-and-drop, and "does this look right?" checks

Do not force these skills if the task is too small or the tool is not available.

Suggested install set:

- `npx skills add https://github.com/vercel-labs/agent-browser --skill agent-browser`
- `npx skills add https://github.com/vercel-labs/agent-skills --skill vercel-react-best-practices`
- `npx skills add https://github.com/anthropics/skills --skill frontend-design`
- `npx skills add emilkowalski/skill`
- `npx skills add https://github.com/mattpocock/skills --skill tdd`

## 1. Before implementing

Start by clarifying the task instead of guessing.

- State assumptions explicitly
- If the request is ambiguous, present the main interpretations instead of silently choosing one
- Push back when a simpler path would achieve the same goal
- If something is still unclear, stop and ask

Before coding, step back and ask:

`How can we make this simpler and dumber while still achieving the goal?`

## 2. Implementation defaults

Prefer the smallest coherent change.

- Reuse the app's existing components before creating new ones
- Reuse existing colors, spacing, shadows, typography, and interaction patterns
- Do not redesign the product unless the user explicitly asks for redesign work
- Do not add gradients or decorative styling that does not already exist in the app
- Do not create custom buttons, cards, inputs, modals, or other UI primitives if existing ones already cover the need
- Do not introduce custom abstractions or components without clear payoff
- Keep the implementation readable for the next agent

For React changes, avoid adding effects by reflex. First prefer derived state, event handlers, keyed resets, and data flow that does not need `useEffect`. Reference: `https://react.dev/learn/you-might-not-need-an-effect`

## 3. Choose the right level of process

### Super small changes

If the change is truly small, do it directly with good code practices and avoid process overhead.

### Normal changes

Use TDD with vertical slices, keeping the implementation as simple as possible.

- Confirm the behavior to prove before writing code
- Write one failing test for one behavior
- Implement the minimum code to make that test pass
- Repeat one behavior at a time
- Add tests that prevent this class of bug from returning
- Do not add broad, low-signal tests just to say "tested"

Pick the lightest tool that covers the risk:

- `Vitest` for business logic, hooks, utilities, and component behavior that does not need a browser
- `pgTAP` for Supabase database logic, SQL, RLS, and policy behavior
- `agent-browser` as the default browser automation tool for agent-run validation, including auth, CRUD, routing, navigation, visual checks, canvas, drag-and-drop, and layout validation
- `Playwright` only when the project already uses it for committed in-repo browser tests or when the task specifically requires Playwright

If UI was changed in a meaningful visual way, explicitly confirm whether `agent-browser` validation was done.

## 4. Debugging

Debug by seeking truth, not by retrying blindly.

- Read the code carefully before rerunning commands
- Form a concrete hypothesis for the failure
- Liberally add temporary logging statements anywhere in the codebase to verify logic works as you expect, but do not commit them
- Trace the root cause before fixing symptoms
- Remove temporary debugging code before finishing

## 5. Review before finishing

Review the change with these questions:

- Is this reusable and understandable, or is it a quick fix?
- Does it follow the app's existing patterns?
- For React and Next.js work, does it follow `vercel-react-best-practices`?
- Did we avoid over-engineering?
- If another agent opens this later, will the intent be obvious?

## 6. Git hygiene for concurrent sessions

When the user expects active branch hygiene across multiple agent sessions:

- Commit after each meaningful change set
- Push the branch if the change has not already been pushed
- Do not rewrite or revert unrelated work from other sessions
- Keep commits scoped and readable

Do not force a commit/push if the repo state is unclear, broken, or the user is obviously still iterating on the same unfinished change.

## User request

$ARGUMENTS
