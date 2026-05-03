---
pubDate: 2026-05-05
author: Renato Fekete
title: useEffect
description: "useEffect - what is it, and when should you use it."
image:
  url: "/src/images/blog/1.jpeg"
  alt: "#"
tags: ["JavaScript", "React"]
---

You've probably written this:

```js
useEffect(() => {
  async function fetchUser() {
    const res = await fetch(`/api/user/${userId}`);
    const data = await res.json();
    setUser(data);
  }

  fetchUser();
}, [userId]);
```

It looks fine. It has a dependency array. But imagine a dropdown where the user selects different user IDs quickly. If the second request resolves before the first, you'll render the wrong user. Here's why.

## What useEffect actually is

useEffect is a React hook that lets you synchronize a component with an external system. That is the official definition.

We use it for connecting to anything that isn't controlled by React.

## Dependency array traps

Probably the most important thing to know about useEffect is the dependency array. It controls when the effect runs.

### No dependency array

```js
useEffect(() => {
  async function fetchUser() {
    const res = await fetch(`/api/user/${userId}`);
    const data = await res.json();
    setUser(data);
  }

  fetchUser();
});
```

It runs after every render.

### Empty dependency array

```js
useEffect(() => {
  async function fetchUser() {
    const res = await fetch(`/api/user/${userId}`);
    const data = await res.json();
    setUser(data);
  }

  fetchUser();
}, []);
```

Runs once after the component mounts.

### Values inside dependency array

```js
useEffect(() => {
  async function fetchUser() {
    const res = await fetch(`/api/user/${userId}`);
    const data = await res.json();
    setUser(data);
  }

  fetchUser();
}, [userId]);
```

It runs only when dependency changes.
