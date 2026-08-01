# Quickstart

Go from zero to a fully reactive store in under five minutes. This guide installs
Glide, wires up your first store, and reads it from a component.

> [!NOTE]
> **Prerequisites.** Glide requires `Node.js 18+` and works with React, Vue, and Svelte.

## Installation

Install the core package with your preferred package manager.

```bash
npm install @glide/core
```

## Create a store

A *store* bundles reactive state with the actions that mutate it. Define one with
`createStore` - actions receive a draft you can mutate directly.

```ts
import { createStore } from '@glide/core'

// A store holds reactive state and the actions that mutate it
export const counter = createStore({
  state: { count: 0 },
  actions: {
    increment: (s) => s.count++,
    add: (s, n) => (s.count += n),
  },
})
```

> [!TIP]
> **Tip.** State is structurally shared - only components that read a changed slice
> re-render. No selectors required for correctness.

## Reading data

Subscribe from any component with `useStore`. Pass a selector to read just the slice
you need.

```tsx
import { useStore } from '@glide/react'
import { counter } from './store'

export function Counter() {
  const count = useStore(counter, (s) => s.count)

  return (
    <button onClick={counter.increment}>
      Clicked {count} times
    </button>
  )
}
```

## Configuration options

Pass a second argument to `createStore` to tune persistence, devtools, and batching.

| Option     | Type      | Default | Description                                              |
| ---------- | --------- | ------- | -------------------------------------------------------- |
| `persist`  | `boolean` | `false` | Save state to storage and rehydrate on load.             |
| `devtools` | `boolean` | `true`  | Enable the time-travel devtools overlay in development.  |
| `name`     | `string`  | -       | Label shown in devtools and error messages.              |
| `throttle` | `number`  | `16`    | Milliseconds to batch notifications before flushing.     |

> [!WARNING]
> **Heads up.** Enabling `persist` writes to `localStorage` synchronously. For large
> stores, prefer the async `persist.adapter` option.

Toggle the devtools overlay any time with <kbd>⌘</kbd> <kbd>⇧</kbd> <kbd>D</kbd> while
your app is running.
