# React Effect Guardrail

Before adding `useEffect`, check whether the logic can be expressed more simply.

Prefer:

- Deriving values during render instead of syncing duplicate state
- Updating state inside the event that caused it
- Resetting or remounting with a `key` when the UI should restart from scratch
- Moving user-triggered logic out of effects and into explicit actions

Use an effect when you truly need to synchronize with something outside React, such as the network, DOM APIs, subscriptions, timers, or third-party systems.

Reference:

- `https://react.dev/learn/you-might-not-need-an-effect`
