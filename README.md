# Stale Closures in React useEffect with useState

This repository demonstrates a common, yet subtle, bug in React applications involving stale closures within `useEffect` hooks when used with `useState`.

The issue arises because the value captured by the closure in `useEffect` is not guaranteed to be the most up-to-date value of the state variable.  The state update might not be fully reflected by the time the effect runs.

**Bug:** The `console.log` inside the `useEffect` hook may sometimes display an outdated value of `count`. This is because the `useEffect`'s dependency array `[count]` only checks for changes in `count` *after* the current render cycle is completed, leading to a closure containing a stale value of `count` in some cases.

**Solution:**  A functional update to `setCount` can prevent this issue. Using the previous state value inside the update function guarantees that you use the most recent state.