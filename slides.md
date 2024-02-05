---
theme: ./theme
fonts:
  sans: Comfortaa
highlighter: shiki
class: text-center
lineNumbers: false
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
transition: slide-left
css: unocss
title: Feature Flags
---

# Feature Flags

## Light switches for your apps

---

## What are feature flags?



You can think of feature flags like light switches

<!-- Put simply, feature flags are a way to control the visibility of features in your app. You can think of them like light switches for your app. 

You can turn them on or off, and you can even dim them to control the percentage of users who see the feature. -->

<!-- they allow you to progamatically turn features on and off -->

<img src="/homer-light-switch.gif" class="m-2" />


<!-- gif -->


---
layout: comparison
clicks: 2
---

## Examples


A/B Testing

::a::

<div v-click="1">
<img src="/black-button-feature.png" class="m-1" />
</div>

::b::

<div v-click="2">
<img src="/red-button-feature.png" class="m-1" />
</div>

--- 
layout: comparison
clicks: 2
---

## Examples

<!-- maybe your app is undergoing maintenance and you don't want to show users broken functionsality, banner your site with a feature flag  -->

Error Banners

::a::

<div v-click="1">

<img src="/normal-site.png" class="m-1" />
</div>

::b::

<div v-click="2">
<img src="/error-site.png" class="m-1" />
</div>


---
---

## Examples

Release only to internal teams via overrides

<!-- maybe your features are ready but you want to release to production without releasing to everyone. You can use overrides to release to internal teams only -->

<!-- a lot of feature flag providers will allow you to override the value of a feature flag so it can be tested internally -->

```typescript 

window.cookie = 'new-button-feature=true'

```

---
---

## Examples

Quickly roll back a feature in production

<!--  Disable your changes in seconds without having to roll back or forward fix a deployment, which could take 10 - 15 minutes -->

<img src="/roll-back.gif" class="m-2" />

---
---

# You're in good company

Many companies use feature flags to control the visibility of features in their apps.

<!-- It helps them release faster and safer as well as pull features back in the event of something breaking -->

## TODO: add fade in logo animation of companies

```ts {1|2|3|4}
Airbnb 
Netflix
Facebook
Google

```

<!-- Now that we've gone over the basics of what a feature flag is and who uses it, why would you want to use a feature flag in your app -->

---
layout: center
---

# Benefits

## Why use feature flags in your app?

---

## TODO: need to add some examples / make different slides for each point

<!-- now we know about the basic concepts of a feature flag, why would we want to use this? -->

1. Safeguard releases

<!-- safeguard releases by being able to quickly roll back a feature if it causes errors -->

2. Staff shipping - release to internal only members
<!-- 
better QA and testing by being able to test features in production via an override such as a query parameter or cookie
 -->

3. Able to quickly react to issues in production 
<!-- 
  Disable your changes in seconds without having to roll back or forward fix a deployment, which could take 10 - 15 minutes
 -->

4. Allows you to release your code little and often 

<!-- 
  Commonly we work on big features and release them all at once. This can be cumbersome as we need to line up backend features with frontend features. With feature flags we can release our code little and often and not have to worry about the frontend and backend being in sync. If the backend isn't quite ready, we can release the frontend code and turn the feature on when the backend is ready
 -->

---
---

# The anatomy of a feature flag

```ts{2|3|4|5|6|7}

{
  "name": "new-feature",
  "description": "A new feature",
  "enabled": true,
   "overides": {
    "cookie": "new-feature=true",
   }
}

```

---
layout: center
---
## Implementing feature flags with hooks

```typescript{2|4|5|8}
const myComponent = () => {
  const { enabled, overrides } = useFeatureFlag('new-feature');

  if (enabled || overrides.cookie === 'new-feature=true') {
    return <NewFeature />
  }

  return <OldFeature />
}

```

---
layout: center
---

# How to implement feature flags

## This would not be very interesting without... renderers! {v-click}

---
layout: quote
---


# What's a Renderer?

> A renderer keeps an external _output_ in sync with a reactive value.

---
layout: center
---

# Responsibilities

1. Subscribe to a reactive value
2. Schedule an update to the output
3. If appropriate, coordinate updates for efficiency

---

# The Debug Renderer

## Useful for Demonstration

```ts {1,2|4,5|7-9|11|12|13|all}
const counter = Cell(0);
const increment = () => counter.current++;

const text = document.createTextNode(counter.current);
document.body.appendChild(text);

const button = document.createElement('button');
button.textContent = '++';
button.addEventListener('click', increment);

DEBUG_RENDERER.render(counter, {
  render: () => text.textContent = counter.current,
  schedule: queueMicrotask
});
```

<style>
  .slidev-layout {
    --slidev-code-font-size: 0.8rem;
    --slidev-code-line-height: calc(0.8rem * 1.5);
  }
</style>

---

# The React Renderer

```tsx {1,2|5|7|8|all}
const counter = Cell(0);
const increment = () => counter.current++;

function Component() {
  return useReactive(() => {
    return <>
      {counter.current}
      <button onClick={increment}>++</button>
    </>;
  });
}
```

---

# The Preact Renderer

```tsx {1,2|5-8|all}
const counter = Cell(0);
const increment = () => counter.current++;

function Component() {
  return <>
    {counter.current}
    <button onClick={increment}>++</button>
  </>;
}
```

---
layout: center
---

# Um, Module State?

## I want each component to have its own state!

---

# Reusable State

```ts
const Counter = Resource(() => {
  const cell = Cell(0);

  return {
    get count() { return cell.current; }),
    increment: () => cell.current++
  };
});
```

---

# In the React Renderer

```tsx
function Component() {
  const counter = use(Counter);

  return useReactive(() => {
    return <>
      {counter.count}
      <button onClick={counter.increment}>++</button>
    </>;
  });
}
```

---

# In the Preact Renderer

```tsx
function Component() {
  const counter = use(Counter);

  return <>
    {counter.count}
    <button onClick={counter.increment}>++</button>
  </>;
}
```

---
layout: center
---

# Cleanup

## Where Resources Start to Get Interesting

---

# Cleanup Handlers

```ts
const Stopwatch = Resource(({ on }) => {
  const now = Cell(Date.now());

  const interval = setInterval(() => {
    now.current = Date.now();
  }, 1000);

  on.cleanup(() => clearInterval(interval));

  return now;
});
```

---
clicks: 4
---

<style>
div.code.slidev-vclick-hidden {
  display: block;
  opacity: 1 !important;
}

div.code:not(.slidev-vclick-hidden) .react {
  opacity: 0.3;
}
</style>

# Rendering

<div class="code" v-click>
  
```tsx {2|5|4,6|all}
function Component() { 
  const now = use(Stopwatch);

  return useReactive(() => { // [!code react]
    return <>{now.current}</>;
  }); // [!code react]
}
```

</div>

<Preact at="4" />

---
layout: center
---

# Composing Resources

## ♾️ Universally ♾️ {v-click}

---
layout: comparison
clicks: 5
---

# Composing Resources

::a::

<div v-click="0">


```ts 
const Stopwatch = Resource(({ on }) => {
  const now = Cell(Date.now());

  const interval = setInterval(() => {
    now.current = Date.now();
  }, 1000);

  on.cleanup(() => clearInterval(interval));

  return now;
});
```

</div>

<div v-click="1">

```ts 
const FormattedNow = Resource(({ use }) => {
  const now = use(Stopwatch);
  const formatter = new Intl.DateTimeFormat();

  return Formula(() => {
    return formatter.format(now.current);
  });
});
```

</div>

::b::

<div class="stick" v-click="2">

```tsx {all|2|4,6|1,2,5} {at:2}
function Component() { 
  const now = use(FormattedNow);

  return useReactive(() => { // [!code react]
    return <>{now.current}</>;
  }); // [!code react]
}
```

</div>

<Preact at="5" />

<style>
  .slidev-vclick-target {
    transition: opacity 0.2s ease-in-out;
  }

  .slidev-vclick-prior:not(.stick) {
    opacity: 0.3;
  }
</style>

---
layout: center
---

# Services

## Resources that live as long as the app

### <Star /> No, you do not want to use module state. {v-click}

---
layout: code-sections
clicks: 6
---

# Services

## You can turn any resource into a service.

::a::

## The App

```tsx {0|1,5,7|all|0|all}
import { Starbeam } from '@starbeam/react';

function App() {
  return (
    <Starbeam>
      <Clock />
    </Starbeam>
  );
}
```

::b::

## Any Component

```tsx {0|0|0|1,4|all} {at:0}
import { useService } from '@starbeam/react';

function Clock() {
  const now = useService(FormattedNow);

 return <>The time is: {now}</>;
}
```

::footer::

- The `FormattedNow` resource will be created the first time a component uses it, and will be cleaned
up when the app is unmounted. {v-click=4}
- Since the `FormattedNow` resource used the `Stopwatch` resource, the stopwatch will also be
  cleaned up when the app is unmounted. {v-click=5}
- This is what we mean by "universal reactivity": you were able to describe a reactive system without
  reference to a framework, and then render it using a framework. {v-click=6}
{.one-at-a-time}

<style>
  .one-at-a-time {
    list-style: none;
    height: 3em;
    position: relative;
  }

  .one-at-a-time li {
    --slidev-transition-duration: 0.2s;
    transition: 
      opacity var(--slidev-transition-duration) ease-in-out, 
      transform var(--slidev-transition-duration) ease-in-out,
      left var(--slidev-transition-duration) ease-in-out,
      top var(--slidev-transition-duration) ease-in-out;
    top: 0;
    left: 0;
    margin: 0;
    padding-block: 0.5em;
    transform: scale(1);
    opacity: 1;

  }

  .one-at-a-time li:not(.slidev-vclick-current) {
    position: absolute;
    opacity: 0;
    left: 30%;
    transform: scale(0);
  }
</style>

---
layout: center
---

# Clear Errors and Debugging Infrastructure

## We'll see an example of this in a moment

---
layout: code-sections
---

# A More Elaborate Example

::a::

```js
export class Database {
  #tables = reactive.object({});

  define(table) {
    this.#tables[table] = new Table();
    return this;
  }

  get(table) {
    return this.#tables[table];
  }
}
```

::b::

```js
export class Table {
  #rows = reactive.Map();

  rows = () => [...this.#rows.values()];
  ids = () => [...this.#rows.keys()];

  create(row) {
    this.#rows.set(row.id, row);
  }

  read(id) {
    return this.#rows.get(id);
  }

  update(id, callback) {
    this.#rows.set(callback(this.#rows.get(id)));
  }

  delete(id) {
    this.#rows.delete(id);
  }
}
```

---
layout: section
---

# DEMO TIME!

---
layout: center
---

# Why is it Fast?

## Demand-Based Revalidation {v-click}

---

# What It's Not

<v-click>

## It's not push-based.

The benefit of push-based reactivity is granular updates. One downside is that you can't just use
normal programming patterns to compute your data. All push-based reactivity systems require you to
use their combinators to build computations.

Rx.js and Signals are good examples of push-based reactivity.

> With demand-based revalidation, there are no hard references from cells to formulas, and no need
> to communicate changes through intermediate layers.


</v-click>

---

# What It's Not

## It's not recomputation-based.

The benefit of recomputation-based reactivity is that it feels like normal programming. The downside
is that the framework needs to run the user's code again to determine whether any updates are needed.

React is a good example of recomputation-based reactivity.

> With demand-based revalidation, it's possible to determine whether an update is needed without
> re-evaluating the user's code, which can be arbitrarily expensive.

---

# Demand-Based Revalidation

Demand-based revalidation was originally developed for the Glimmer rendering engine, and was
inspired by HTTP caching.


<div class="note">

<Star /> HTTP caching is a form of demand-based revalidation! {.note}

</div>

We originally developed the algorithm because we _desperately needed to speed up initial rendering_,
but _could't afford to regress on updating performance_ (which was very fast due to our push-based
updating model). {v-click}

<style>
  em {
    font-style: normal;
    color: var(--slidev-theme-accents-red);
  }

 .note  {
    color: var(--slidev-theme-accents-blue);
  }
  blockquote {
    margin-top: 1em;
  }
</style>

---

# Demand-Based Revalidation

<div>

That algorithm inspired Rust's Salsa, which powers Rust Analyzer and several JavaScript tools.

</div>

![Salsa](/salsa.png)

<style>
   :deep(div.my-auto) {
    display: grid;
    grid-template:
      "h1 image" max-content
      "body image" 1fr /
      1fr 3fr;
    column-gap: 3em;
    grid-template-columns: 1fr 1fr;
  }

  h1 {
    grid-area: h1;
  }

  div {
    grid-area: body;
  }

  p:last-child {
    grid-area: image;
  }
</style>

---

# The Basic Idea

1. All reactive state is stored in cells, which keep a revision number.
2. Computations ultimately read from cells, so computations also have a revision number: the maximum
   revision number of the cells that were used in the computation.
3. To determine whether a computation is up-to-date, we compare the computation's current revision
   number to its revision number the last time we used its value.

**Critically**, this gives us the ability to **revalidate a computation without re-running it**.

> This lets you write natural code to build up your expressions, while still getting the granuality
> benefits of push-based systems.

<style>
strong {
  color: var(--slidev-theme-accents-red);
}

blockquote p {
  color: var(--slidev-theme-accents-blue);
}
</style>

---

# Coming Soon

- Element Modifiers
- Production Mode
- Significant Internal Refresh
- Vue renderer

## On the Horizon

- Debugging Tools
- Svelte renderer


---

# Quick Hits

- What is a Framework, At Least According to Starbeam?
- Why is a renderer not an Effect?
- How is demand-based revalidation different from signals?

---
layout: cover
---

# Thank you!

## Any Questions?