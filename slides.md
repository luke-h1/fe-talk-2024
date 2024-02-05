---
theme: ./theme
fonts:
  sans: Comfortaa
highlighter: shiki
class: text-center
lineNumbers: true
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
transition: slide-left
css: unocss
title: Feature Flags (FE Sheffield May)
---

# Feature Flags

## Light switches for your apps

---
layout: two-cols

---

<div class="mt-8">
  <h1 class="!c-white !text-5xl !pt-8">
    Luke Howsam
  </h1>

  <div class="c-gray-400 mt-8">
    <p>
    Software Developer at Sky Betting & Gaming.
    </p>
    <p>
    Typescript, DevOps, anything frontend 😉
    </p>
  </div>

  <div class="flex gap-4 items-center mt-12 text-sm">
    <ph-github-logo class="c-gray-500" />
    <a href="https://github.com/luke-h1">luke-h1</a>
  </div>
  <div class="flex gap-4 items-center mt-4 text-sm">
    <ph-globe class="c-gray-500" />
    <a href="https:/lhowsam.com">lhowsam.com</a>
  </div>
  <div class="flex gap-4 items-center mt-4 text-sm">
    <ph-linkedin-logo class="c-gray-500" />
    <a href="https://www.linkedin.com/in/lukehowsam/">lukehowsam</a>
  </div>
</div>

::right::
<img src="/luke.jpeg" class="rd-full w-28  ml-auto" />


<!-- at the moment I work for sky bet
been there for just under a year now, been a developer for about two years and a QA engineer for about 2 years before that. and today we're going to be talking about feature flags and why you might want to use them -->

---


## What are feature flags?


You can think of feature flags like light switches

<img src="/homer-light-switch.gif" class="m-2" />


<!-- 
Put simply, feature flags are a way to control the visibility of features in your app. You can think of them like light switches for your app
they allow you to progamatically turn parts of your application on and off.

You can turn them on or off, and you can even dim them to control the percentage of users who see the feature. Now that we know what a feature flag is, who uses them?
-->

---
clicks: 4
layout: fact
---

## Who uses them?


<!-- It helps them release faster and safer as well as pull features back in the event of something breaking -->


<div class="flex items-center gap-8">
<div v-click="1">
<img src="/airbnb.png" class="m-1 w-20" />
</div>

<div v-click="2">
<img src="/netflix.svg" class="m-1 w-20" />
</div>

<div v-click="3">
<img src="/gh.png" class="m-1 w-20" />
</div>

<div v-click="4">
<img src='/google.png' class="m-1 w-20" />
</div>
</div>


<!-- Feature flags are very prevelant in the industry. They help minimize risk quite a lot especially when your working on a big application. Just to name a few Airbnb, GitHub, Netflix use them for various reasons -->


---
--- 
## Benefits

<img src="/fargo.gif" class="m-2 w-80" />


<!-- You might be thinking this is great and everything but what's in it for me and my projects? So I've popped together a few examples on what you can use feature flags for -->



---
layout: comparison
clicks: 2
---

## Benefits


A/B Testing

::a::

<div v-click="1">
<img src="/black-button-feature.png" class="m-1" />
</div>

::b::

<div v-click="2">
<img src="/red-button-feature.png" class="m-1" />
</div>



<!-- Feature flags are a great way to temporarily expose your users to things such as alternate designs, new color schemes to see if that drives higher click rates etc. You can combine this with staggered rollouts where you release to small subsets of users -->

--- 
layout: comparison
clicks: 2
---

## Benefits

Error Banners

::a::

<div v-click="1">

<img src="/normal-site.png" class="m-1" />
</div>

::b::

<div v-click="2">
<img src="/error-site.png" class="m-1" />
</div>

<!-- maybe your app is undergoing maintenance or the backend that you're talking to is broken and you don't want to show users broken functionsality, banner your site with a feature flag would be a great option for that -->

---
layout: comparison
clicks: 2
---

## Benefits

Staff / internal releases

::a::

<div v-click="1">

```typescript 

window.cookie = 'new-button-feature=true'

```
</div>

::b::

<div v-click="2">

```typescript 
 https://my-awesome-site.com?new-button-feature=true
```

</div>


<!-- This is one of my favorite things to do with feature flags. Most feature flag providers have a way of overriding a disabled feature flag. So you can release your work under a disabled feature flag and use something such as a query parameter or a cookie to allow your QA engineers, stakeholders view the work in production without potentially releasing something broken to your users. -->

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

# How to implement feature flags


<div v-click>
<img src="/yipee.gif" class="m-2 w-150" /> 
</div>
---
clicks: 2
layout: comparison
---
## Implementation

There's many ways to implement a feature flag. We're going to be looking at two ways

::a:: 
<div v-click="1">

> Using a central file in your codebase to store your feature flags

<br />
<br />


```typescript
// src/feature-flags.ts

const featureFlags = {
  newFeature: true,
  anotherFeature: false,
};
export default featureFlags;
```
</div>


::b::

<div v-click="2">

> Using a third party service such as LaunchDarkly or your own feature flag API

<br />

```typescript
// src/feature-flags.ts

const MyComp = () => {
  const newFeat = fetchFromApi('new-feature');
  return newFeat ? <NewFeat /> : <OldFeat />;
};
```
</div>


<!-- If after this talk you're wondering which one to use, I'd suggest asking yourself this question:
Do I need to be able to change the feature flag without a code change? If the answer is yes, then you should use a third party service. If the answer is no, then you can use a central file in your codebase to store your feature flags. For simplicity we're going to be using a file based feature flag -->

---
layout: full
---
## Let's implement a feature flag

```typescript
// src/feature-flags.ts

export const featureFlags: FeatureFlag[] = [
  {
    name: 'new-feature',
    description: 'A new feature',
    enabled: true,
    overrides: {
      cookie: 'override',
    },
  },
];

```

---
layout: center
---

# How to implement feature flags

## Now we have our feature flags, how do we use them?


---
layout: quote
---


# Let's create a hook 

```typescript 
// src/useFeatureFlag.ts

const AllowedFeatureFlags = ['new-feature', 'another-feature'] as const;

type AllowedFeatureFlag = typeof AllowedFeatureFlags[number];

const useFeatureFlag = (name: AllowedFeatureFlag): boolean => {
  const cookie = parseCookie('new-feature');
  
  const flag = featureFlags.find((flag) => flag.name === name);
  return flag.enabled || cookie.value === 'my-secret-value';
};
 

```

<style>
  .slidev-layout {
    --slidev-code-font-size: 0.8rem;
    --slidev-code-line-height: calc(0.8rem * 1.5);
  }
</style>
<!-- we use a cookie parsing library to check for the existense of a cookie to override the feature. We then use our hook with the name of the feature we're looking for and are then providing a boolean value to the override dependening on whether we have an override cookie present or not -->


---
layout: center
---

# All together now

```typescript 
 const MyComponent = () => {
  const newFeature = useFeatureFlag('new-feature');
  return newFeature ? <NewFeature /> : <OldFeature />;
 }

```
<style>
  .slidev-layout {
    --slidev-code-font-size: 0.8rem;
    --slidev-code-line-height: calc(0.8rem * 1.5);
  }
</style>
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