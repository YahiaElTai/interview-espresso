# React & State Management

> **27 questions** — 13 theory, 10 practical, 4 experience

- Reconciliation algorithm: virtual DOM diffing heuristics, key-based identity, element type comparison, O(n) tradeoffs
- Re-render rules: what triggers renders, subtree re-rendering by default, state/props/context changes, comparison with fine-grained reactivity (Solid, Svelte)
- State management: Context vs Redux vs Zustand vs React Query
- React Query as server state cache (stale-while-revalidate, deduplication, background refetching)
- React Server Components and the server/client boundary
- Advanced patterns: compound components, render props, custom hooks
- Forms: controlled vs uncontrolled components, React Hook Form vs Formik, validation strategies, form state complexity
- Error boundaries: class-based error catching, fallback UI, granularity strategies, limitations (no hooks equivalent, no async errors)
- Hooks rules and mental model: why call order is fixed, closure stale-value traps, rules of hooks enforcement
- useEffect mental model: dependency arrays, cleanup timing, effect vs event distinction, common pitfalls (missing deps, infinite loops)
- Performance profiling: React DevTools Profiler, React.memo, useMemo, useCallback
- Code splitting: React.lazy, Suspense, route-based and component-based splitting

---

## Foundational

<details>
<summary>1. How does React's reconciliation algorithm work — what heuristics does the virtual DOM diffing use to avoid O(n^3) tree comparison, why does React diff by element type and key instead of doing deep structural comparison, and what practical consequences do these heuristics have for how you structure component trees?</summary>

<!-- Answer will be added later -->

</details>

## Conceptual Depth

<details>
<summary>2. How do React's re-render rules actually work — what triggers a re-render, why does React re-render the entire subtree by default instead of only the changed component, and how does this "coarse-grained" rendering model compare to the fine-grained reactivity of frameworks like Solid or Svelte in terms of performance tradeoffs and developer experience?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>3. When choosing between Context, Redux, Zustand, and React Query for state management — what type of state is each best suited for, what are the real performance and complexity tradeoffs (especially Context's re-render problem at scale), and when is reaching for an external state library overkill vs essential?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>4. Why should server state be treated differently from client state — how does React Query's stale-while-revalidate model work, what do its deduplication and background refetching features solve that manual useEffect + useState patterns don't, and when does React Query add unnecessary complexity?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>5. What are React Server Components and what problem do they solve -- how does the server/client boundary work in practice, what can and can't you do in a Server Component vs a Client Component, and what constraints does the boundary impose on data flow and component composition?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>6. How do React Server Components differ from traditional SSR -- what does each approach send to the client, how do they handle interactivity differently, and what are the real tradeoffs teams should evaluate before adopting RSC (bundle size, hosting requirements, ecosystem support, mental model complexity)?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>7. When do advanced component patterns (compound components, render props, custom hooks) genuinely improve a codebase vs add unnecessary abstraction — what specific problem does each pattern solve, how do they compare in terms of API ergonomics and composability, and what signals tell you a pattern is being overengineered?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>8. How are hooks implemented internally in React's Fiber tree — why does React use a linked list to store hook state, why must hooks be called in the same order every render (and what breaks if they aren't), and how do closure stale-value traps occur in useEffect and event handlers?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>9. What is the correct mental model for useEffect -- why should effects be thought of as synchronization with external systems rather than lifecycle callbacks, how does cleanup timing actually work (when does React run the cleanup function and why), what is the distinction between effects and event handlers that determines which one you should use, and what causes the common infinite loop pitfall where adding a dependency triggers the effect which updates the dependency?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>10. Why do React.memo, useMemo, and useCallback exist and what is the correct mental model for when they help vs when they hurt — how does each one prevent unnecessary work, what is the cost of memoization itself (memory, comparison overhead), and what common misuses actually make performance worse?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>11. What are the different code splitting strategies in React (route-based vs component-based) — how do React.lazy and Suspense enable lazy loading, what determines where you should place split points for maximum bundle size impact, and when can aggressive splitting actually hurt performance through excessive network requests?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>12. Why do forms in React become complex as they grow -- what are the tradeoffs between controlled and uncontrolled components, when does each approach break down, and why do libraries like React Hook Form and Formik exist instead of just using native form state? What validation strategy considerations (schema-based vs field-level, sync vs async) matter when choosing between them?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>13. Why are error boundaries still class components in React and what are their actual limitations -- what errors do they catch vs miss (async errors, event handlers, SSR), how do you decide on error boundary granularity (page-level vs component-level), and what patterns work around the lack of a hooks-based error boundary API?</summary>

<!-- Answer will be added later -->

</details>

## Practical — Performance Profiling & Optimization

<details>
<summary>14. Walk through a performance profiling session using React DevTools Profiler — how do you identify which components are re-rendering unnecessarily, how do you read the flamegraph and ranked chart, what do the commit durations and render reasons tell you, and how do you translate profiler findings into actionable optimizations?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>15. Given a component tree where a parent re-renders frequently and causes expensive child re-renders — show the before/after code applying React.memo, useMemo, and useCallback to fix it, explain why each optimization is necessary in this specific case, and demonstrate a scenario where applying React.memo without stabilizing props actually does nothing?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>16. Set up route-based code splitting for a React application using React.lazy and Suspense — show the router configuration, the lazy-loaded route components, the Suspense fallback, and then add a component-level split for a heavy feature within one of those routes. Explain how you verify the split is working using the browser's network tab and what the bundle size impact looks like?</summary>

<!-- Answer will be added later -->

</details>

## Practical — State Management & Component Patterns

<details>
<summary>17. Build a compound component (e.g., a Tabs component with Tabs, TabList, Tab, TabPanel) in TypeScript — show the full implementation using Context to share state between the compound parts, explain the component API design decisions, and demonstrate how this pattern gives consumers flexible composition while keeping internal state encapsulated?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>18. Set up React Query for a feature that lists and creates items -- show the TypeScript code for the query hook, mutation hook, and cache invalidation strategy, and explain how staleTime and gcTime affect caching behavior and when you'd tune each one.</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>19. Implement optimistic updates with React Query for a mutation that could fail -- show the TypeScript code using onMutate, onError, and onSettled callbacks, demonstrate what happens visually when the server rejects the update, and explain why the rollback pattern requires saving a snapshot of the previous cache state.</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>20. Build a custom hook that manages a WebSocket connection — show the TypeScript implementation that handles connection lifecycle, reconnection logic, cleanup on unmount, and avoids stale closure bugs when accessing current state inside event handlers. Explain the specific closure trap and how the ref pattern or useEffectEvent solves it?</summary>

<!-- Answer will be added later -->

</details>

## Practical — Forms & Modern APIs

<details>
<summary>21. Build a multi-step form with validation using React Hook Form and a schema validation library (Zod or Yup) -- show the TypeScript code for the form setup, per-step validation, error display, and submission handling. Explain why React Hook Form's uncontrolled approach performs better than Formik's controlled approach for large forms, and what breaks if you mix controlled and uncontrolled patterns.</summary>

<!-- Answer will be added later -->

</details>

## Practical — Debugging & Troubleshooting

<details>
<summary>22. You're adopting React Server Components and hitting hydration mismatch errors and unexpected 'use client' boundaries -- show a concrete example of a component tree that causes these errors, walk through how to identify which components are server vs client using error messages and React DevTools, and show the before/after code restructuring that correctly places the 'use client' boundary so server-fetched data flows to client interactive elements without serialization issues.</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>23. A useEffect callback is logging stale state values even though the state has clearly updated — walk through why this happens (the closure captures the value at render time), how to identify stale closure bugs using console logging and the React DevTools hooks inspector, and show the different fix patterns (dependency array correction, ref pattern, functional state updates) with tradeoffs of each?</summary>

<!-- Answer will be added later -->

</details>

---

## Experience-Based Questions

These questions test real-world experience. Prepare by mapping them to your own projects and situations.

<details>
<summary>24. Tell me about a time you had to significantly improve the performance of a React application — what were the symptoms, how did you profile and identify the bottlenecks, what changes did you make, and what was the measurable impact?</summary>

<!-- Answer framework will be added later -->

</details>

<details>
<summary>25. Describe a time you chose a state management approach for a complex feature or application — what were the requirements, what options did you evaluate, what did you pick and why, and would you make the same choice today?</summary>

<!-- Answer framework will be added later -->

</details>

<details>
<summary>26. Tell me about a time you debugged a subtle React bug that was hard to reproduce — what were the symptoms, how did you narrow down the root cause, and what was the fix?</summary>

<!-- Answer framework will be added later -->

</details>

<details>
<summary>27. Describe a time you introduced a new pattern, library, or architectural change to a React codebase — how did you evaluate it, how did you get team buy-in, and how did the migration go?</summary>

<!-- Answer framework will be added later -->

</details>
