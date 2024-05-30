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

<p class='mb-6 text-pink'>A safer way of releasing software</p>

#### Frontend Sheffield May 2024


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
    TypeScript, DevOps, anything frontend :)
    </p>
  </div>
  

  <div class="flex gap-4 items-center mt-4 text-sm">
    <ph-linkedin-logo class="c-gray-500" />
    <a href="https://www.linkedin.com/in/lukehowsam/">lukehowsam</a>
  </div>
   <div class="flex gap-4 items-center mt-4 text-sm">
    <ph-twitter-logo class="c-gray-500" />
    <a href="https://twitter.com/LukeH_1999">LukeH_1999</a>
  </div>

  <div class="flex gap-4 items-center mt-12 text-sm">
    <ph-github-logo class="c-gray-500" />
    <a href="https://github.com/luke-h1">luke-h1</a>
  </div>
  <div class="flex gap-4 items-center mt-4 text-sm">
    <ph-globe class="c-gray-500" />
    <a href="https:/lhowsam.com">lhowsam.com</a>
  </div>
</div>

::right::
<img src="/luke.jpeg" class="rd-full w-28  ml-auto" />

<!--
Hiya, I'm Luke. I'm a software dev at the mo I've been a dev for about two years and a QA engineer for about the same amount of time before that. Love anything frontend or devops related. Got my socials there if you wanna continue the conversation or have any questions. During the talk if you have a question, stick your hand up and I'll try to answer it as best as I can. Obviously we'll try to keep conversations succinct so we don't get off track but if they start to get a bit too long, we can always chat after
-->

---
clicks: 2
layout: two-cols
---

<div v-click='1'>
<h2>Feature Flags</h2>
<img src='/simpsons-flag.gif' class='w-100' />
</div>

::right::

<div v-click='2'>
<h2>A/B testing</h2>
<img src='/a-or-b-simpsons.gif' class='w-100' />
</div>

<!--
Today we're going to be talking about feature flags + a/b testing and why you might want to use them in your projects
-->

---
layout: center
clicks: 7
---

## Topics


<div class='text-left'>
  <div v-click="1">
  <Star /> Software delivery 🚚
  </div>

  <div v-click="2">
  <Star /> What are feature flags ⛳️
  </div>

  <div v-click="3">
  <Star /> What is a/b testing 🧪
  </div>

  <div v-click="4">
  <Star /> Benefits 🎉
  </div>

  <div v-click="5">
  <Star /> Industry usage 🏢
  </div>

  <div v-click="6">
  <Star /> Code patterns 🧑‍💻
  </div>

  <div v-click="7">
    <Star /> Real world example 🌍
    </div>
</div>

<!--
background on software delivery, quick explanation of feature flags and a/b tests, why you might want to use them, what companies use them, how to structure feature flags and a/b tests in your project and then we're gonna finish off with a real world example
-->

---

# Software delivery

<!--
Before we get into feature flags and why they're great, I wanted to talk a little bit on how most of us deliver software.
-->

---

# Software delivery

## Feature / need

<img src='/app.webp' width='500' />

<!--
We usually get a feature requested or a business need come thru
-->

---

# Software delivery 

## Refine and estimate

<img src='/refine.gif' width='500' />

<!--
We then go over that work with someone like a Business analyst to estimate how much effort its going to take to implement
-->

---

# Software delivery

## Development happens

<img src='/build-it.gif' width='500' />

<!--
We build the actual thing. We write the code, the unit tests and get people to review it.
-->

---

# Software delivery

### QA / testing happens


<img src='/inspect.gif' width='500' />

<!--
Once we've built the thing, QA engineers get involved. We usually deploy the feature to staging and then the testers make sure we developers haven't done anything stupid.
-->

---

# Software delivery

### Release


<img src='/deploy-it.gif' width='500' />

<!--
Last but not least, we release to production
-->

---

# Software delivery 

### Kaboom ?? 🧨

<img src='/fallout-gif.gif' width='500' />

<!--
But what happens when things go south?
-->

---

# Software delivery 


### Panic

<img src='/error-graph.png' width='1500' height='1000' />

<!--
maybe the big feature that works fine in staging blows everything up when you deploy it to production and it ends up causing a load of errors and downtime for your users.
-->

---

# Software delivery

## Holidays 🏖 😎️

<img src='/backend.gif' />

<!--
Or maybe it's a problem that's more subtle. Your backend developer goes on holiday for 3 weeks and all the frontend UI updates you've done are ready to go to production but the backend work isn't done. So instead of releasing it, you have to wait until they're back. block prod release pipeline.
-->

---

# Software delivery

## Performance

<img src='/slow-simpsons.gif' />

<!--
Maybe you want build a new feature. You deploy it to staging, looks fine, but ends up being really slow in production.
-->

---
layout: two-cols
clicks: 3
---

# Software delivery 

## Consequences


<img src='/slow.gif' width='450' />


::right::
<div class='mt-50'>
  <div v-click='1'>
  <Star />
  Holidays
  </div>
  <div v-click='2'>
  <Star />
  Differences in environments
  </div>
  <div v-click='3'>
  <Star /> Performance 
  </div>
</div>

<!--
and so how most of us deliver software can be quite vulnerable to these things. If any of the aformented things goes wrong, our full team is unavailable, our environments act different, or we have performance issues. It all comes crumbling down. We have to roll back, forward fix or wait around until our full team is back.
-->

---

# Software delivery

## Users

<img src='/no-nice.gif' />

<!--
and this isn't a great experience for users.
-->

---

# A better way

<img src='/a-solution.gif' />

<!--
Fortunately a lot of companies have had these exact problems. And this is where feature flags can help. They make a lot of the problems we've just talked about a lot less likely to happen and provide you with a lot of other cool things that we're gonna talk about
-->

---
layout: two-cols
clicks: 1
---

## What are Feature flags 🤔

<img src="/homer-light-switch.gif" class="w-80 h-80" />


::right::

<div v-click='1' class='mt-12'>

```typescript
const HomePage = () => {
  const newFeature = false;


  return newFeature ? <NewFeature /> : <OldFeature />;
}
```
</div>

<style>
  .slidev-layout {
    --slidev-code-font-size: 0.75rem;
    --slidev-code-line-height: calc(0.75rem * 1.5);
  }
</style>

<!--
Feature flags are a way to programatically turn features on and off in your app. All a feature flag is at its core is a true or false value. we flip the switch and we get one feature, we flip it back and we get another. Very much like a light switch. So here we have a boolean `newFeature`. If it's true, we render the new component, otherwise we render the old component. That's all there is to it
-->

---

# Feature flags 

<img src="/ff-flow.png" class='w-350' />

<!--
so this is the typical flow that happens with a feature flag. We have some new feature. We then have that controlled under a feature flag. If the feature flag is off, users see the old feature. if it's on, they see the new feature
-->

---

# what is a/b testing?

<img src="/ab-testing.png" class="w-150" />

<!--
A/B testing is a way to expose your users to two different versions of a feature. We conduct an a/b test by running an experiment and that usually involves two variants, a control group (user has the existing functionality) and an experiment group (user sees the new feature). In the context of feature flags and the scope of this talk, we're just using a/b testing to control what percentage of users see our new feature. more avenues
-->

---

## a/b test flow

<img src='/ff-ex.png' class='w-350' />

<!--
So as a quick example, this is the typical flow of a feature flag paired with a/b testing. Very similar to the last diagram. We have a new feature, if the feature flag is off, we show the existing functionality. If it's on, we show the new feature. But the difference is we then use an a/b test to control the amount of users that see this feature. So in this case 40% of our userbase sees the new functionality and 60% see the old functionality.
-->

---

## Benefits

<img src="/fargo.gif" class="m-2 w-100" />

<!--
So now we have a bit of background on feature flags, you might be thinking what's in it for me and my projects? So we're going to go thru a few examples
-->

---
layout: comparison
clicks: 2
---

## Benefits


A/B testing

::a::

<div v-click="1">
<img src="/black-button-feature.png" class="m-1" />
</div>

::b::

<div v-click="2">
<img src="/red-button-feature.png" class="m-1" />
</div>

<!--
Feature flags are a great way to temporarily expose your users to things such as alternate designs, new color schemes to see if that drives higher click rates etc. Here we've got two designs, one with a black button and one with a bright red button. You can combine this  with releasing to a small subsets of users with a/b testing to assert whether user's like the first design or the last design
-->

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

<!--
maybe your app is undergoing maintenance or the backend that you're talking to is broken and you don't want to show users broken functionality, bannering your site with a feature flag while you're fixing things would be a great option for that. So our site might normally look like this, and when we enable the error banner flag, our site might look like this
-->

---
layout: comparison
clicks: 2
---

## Benefits

Staff / internal releases

::a::

<div v-click="1">

<img src='/cookie-1.png' />
</div>

::b::

<div v-click="2">

<img src='/url-param.png' />

</div>

<!--
This is one of my favorite things to do with feature flags. Feature flag can be overriden. This means we can release our work to production under a disabled feature flag and use something such as cookie or a query parameter to let our stakeholders or engineers to take a look at the work without us releasing it to everyone. This fixes the issue of having nightmares in production when something acts completely different. Safety net
-->

---
layout: comparison
---

## Benefits

Percentage rollouts

<img src="/perc-rollout.png" class="m-1" />

You can release your feature to a percentage of your users instead of everyone all at once

<!--
We've touched on this a bit already and this is what we'll be using a/b testing for. Instead of activating a feature for all users at once, we can activate features in small percentages We might decide to first release to only 25% of users and then keep an eye on our monitoring and analytics to see if anything goes wrong. This works on spliting your user base into different cohorts - one with the feature flag enabled 25% and one with the feature flag disabled 75%.
-->

---
layout: comparison
---

## Benefits

Segmented rollouts

<img src="/segment-rollout.png" class="m-1" />

Admins, Moderators, certain teams etc.

<!--
Similar to percentage based rollouts but we are exposing features to users with specific attributes. This could be something like only releasing to paid users, only users in a certain region and things like that
-->

---

## Benefits 

Dev tools 

<img src='/fe-sheff-debug.png' />

<!--
With feature flags we can turn on certain tools in production to help us debug issues more easily (e.g. more verbose logging, forcing certain behavior changes in our app like changing the date and time, or forcing errors to see how our app handles them and things like that)
-->

---
layout: comparison
clicks: 1
---

## Who uses them?

<div class="gap-8 flex items-center flex-row justify-center">
  <img src="/airbnb.png" class="m-1 w-20" />
  <img src="/netflix.svg" class="m-1 w-20" />
  <img src="/gh.png" class="m-1 w-20" />
  <img src='/google.png' class="m-1 w-20" />
  <img src='/spotify-logo-1y.jpg' class="m-1 w-20" />
</div>

<div v-click='1'>

<ul class='mt-8'>
<li>
   Risk mitigation 💰
</li>
<li>
   Small rollouts 👩‍🔬
</li>
</ul>
</div>

<!--
Feature flags are very prevelant in the industry. Airbnb, GitHub, Netflix, all the big dogs. It helps them reduce risk and saves them lots of money. For a lot of these companies 1 - 2 minutes of service disruption means lots of money gets lost and most importantly people's trust in a product. A lot of these companies run their projects in a microservice style and it can sometimes be hard to judge how changes affect their application as a whole. That's why using feature flags paired with a/b tests is a no brainer for them.
-->

---

# Code patterns 

<img src='/code-patterns.gif' />

<!--
Now that we're all a bit familiar with feature flags, we're going to go over the two primary patterns for creating feature flags and then we're going to look at a quick demo on how you would use that in the real world. We'll also touch a little on a/b testing with this as well.
-->

---
clicks: 2
---

# Feature flag code patterns

<div v-click="1">
  <Star /> Self hosted
</div>

<div v-click="2">
  <Star />Using an SDK/service
</div>

<!--
There's generally two patterns to getting feature flags into your app. Building it yourself or using a platform like launchdarkly or posthog. We'll first be looking at a self-hosted example and then we'll move onto using an sdk
-->

---

## self hosted feature flag

```ts{2|3|4|5|6,7,8,9}

{
  "name": "new-feature",
  "description": "A new feature",
  "enabled": true,
   "overides": {
     "cookie": "new-feature",
     "value": process.env.OVERRIDE_SECRET
   },
}

```

<!--
Let's start by thinking about what we want to store. We need a name, some metadata about what it's used for, whether it's enabled and finally some way of manually enabling the feature flag (in this case a cookie).
-->

---
layout: comparison
---

## Self hosted

```typescript
// src/feature-flags.ts

export const featureFlags: FeatureFlag[] = [
  {
    name: 'redesign-2024',
    description: 'Redesigned page for 2024',
    enabled: false,
    overrides: {
      name: 'redesign-2024',
      value: process.env.OVERRIDE_SECRET,
    },
  },
];
```

<!--
To emphaize this a bit more, this is just a central file that lives somewhere in your codebase we're not going to be making any api calls or anything like that. We have an array of feature flags here that we're exporing and this just lives in our src folder
-->

---

## Self hosted

```typescript{2|4|5|7,8,9|11|13,14|16}
// src/useFeatureFlag.ts
import featureFlags from '@frontend/utils/featureFlags';

const useFeatureFlag = (name: string): boolean => {
  const featureFlag = featureFlags.find(flag => flag.name === name);

  if (!featureFlag) {
    return false;
  }

  const cookie = getCookie(featureFlag.overrides.name);

  const isCookieOverrideSet =
    cookie.name === featureFlag.overrides.name && cookie.value === featureFlag.overrides.value;

  return featureFlag.enabled || isCookieOverrideSet;
};

```

<style>
  .slidev-layout {
    --slidev-code-font-size: 0.87rem;
    --slidev-code-line-height: calc(0.87rem * 1.5);
  }
</style>

<!--
And we're gonna create a little hook to use this file in our components. Import our array of feature flags. We accept a name as a param and then we try to find the flag that the user passed to the hook. If we can't find it, we return false. At this point we've found a flag. Our next job is to look for a cookie to see if someone is trying to override the feature flag. If the cookies name and value match what we set in the override object, we store the boolean in isCookieOverrideSet. and then we just return an iffy statement that returns true if the feature flag is enabled or if the override is set
-->

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
    --slidev-code-font-size: 1.3rem;
    --slidev-code-line-height: calc(1.3rem * 1.5);
  }
</style>

<!--
And then this is how we use that hook. If `newfeature` is true we show the new functionality otherwise we present the old functionality
-->

---
layout: center
---

# Real world example

<img src="/cat-laptop.gif" class="w-78"  />

<!--
Now that we've looked at self hosting, let's look at using an SDK instead.
-->

---
layout: center
---

## Posthog

<img src="/posthog.png" class="w-350"  />

<!--
To achieve this, we'll be using posthog. Posthog is a really good feature flagging and a/b testing platform. it's got generous free tier and other good stuff that we're going to take a quick look at
-->

---
layout: quote
---

# Our client wants an engineering blog to be added to their site

<img src="/blog-page.png" class="w-120"  />

<!--
We have a problem. Our client wants to make a grand reveal of their new blog page. They're projected to get 100k users and everyone is going to love it. But they're not sure if their website can handle the traffic. So our goal with this exercise is to control this new feature with a feature flag and a/b test it to a small percentage of users to make sure this amazing blog isn't going to blow up their site
-->

---

## Creating a feature flag

<img src="/create-new-one.png" class='h-90' />

<!--
So to create a feature flag in posthog, it's really simple. We need a key (this is what will be used in our frontend code), a descriptive name and whether to enable the feature flag. I've not included it here but you can schedule when you want the feature flag to be enabled and disabled
-->

---

## Creating a feature flag

<img src="/condition-set.png" />

<!--
and finally what users we want to release to. This is called a release condition in posthog and we can release to users based on lots of things built into posthog such as browser version, region or something unique such as their user ID if you have authentication
-->

---
layout: section
---

The current state of our client's codebase


```typescript{5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25|27,28,29,30,31,32,33,34}
interface Props {
  posts: Post[];
}

export default function HomePage({ posts }: Props) {
  return (
    <Layout home>
      <section className={clsx(utilStyles.headingMd, utilStyles.padding1px)}>
        <h2 className={utilStyles.headingLg}>Blog</h2>
        <ul className={utilStyles.list}>
          {posts &&
            posts.map((post) => (
              <li className={utilStyles.listItem} key={post.id}>
                <Link href={`/posts/${post.id}`}>{post.title}</Link>
                <br />
                <small className={utilStyles.lightText}>
                  <Date dateString={post.date as unknown as string} />
                </small>
              </li>
            ))}
        </ul>
      </section>
    </Layout>
  );
}

export const getServerSideProps: GetServerSideProps<Props> = async (ctx) => {
  const posts = getSortedPosts();
  return {
    props: {
      posts,
    },
  };
};
```

<style>
  .slidev-layout {
    --slidev-code-font-size: 0.6rem;
    --slidev-code-line-height: calc(0.6rem * 1.5);
  }
</style>

<!--
Before we get started with integrating posthog into the codebase, let's have a peak at the current state of play. Our codebase is fairly simple, for demo purposes. We just have a homepage that loops over some posts and displays them in a list with a link to go to the blog post. For anyone unfamiliar with Next.js, we fetch our posts in this `getServerSideProps` function. All this does is fetch data at runtime on the server side before we render any html. We then pass that data (in this case our posts) to our HomePage component. Let's turn this page into something that's controlled via a feature flag.
-->

---
clicks: 2
---

## Add the SDK to your project  



<div v-click="1">
```typescript
pnpm i posthog-js
```
</div>

<div v-click="2">

```typescript
// .env

NEXT_PUBLIC_POSTHOG_KEY="your-api-key"
NEXT_PUBLIC_POSTHOG_HOST="your-region"
```
</div>

<!--
Let's get on with adding posthog to our project. The first thing we need to do, is add the posthog sdk to our project. All we do is install the dependency, and add our API keys to environment variables.
-->

---

## Adding feature flags

```typescript{1|4|6,7,8,9,10,11,12,13,14|16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34}
import { useFeatureFlagEnabled } from "posthog-js";

export default function Home({ posts }: Props) {
  const blogEnabled = useFeatureFlagEnabled("blog");

  if (!blogEnabled) {
    return (
      <Layout>
        <div className="card">
          <h2>Come back at 12PM for the grand opening 🥳</h2>
        </div>
      </Layout>
    );
  }

  return (
    <Layout home>
      <section className={clsx(utilStyles.headingMd, utilStyles.padding1px)}>
        <h2 className={utilStyles.headingLg}>Blog</h2>
        <ul className={utilStyles.list}>
          {posts &&
            posts.map((post) => (
              <li className={utilStyles.listItem} key={post.id}>
                <Link href={`/posts/${post.id}`}>{post.title}</Link>
                <br />
                <small className={utilStyles.lightText}>
                  <Date dateString={post.date as unknown as string} />
                </small>
              </li>
            ))}
        </ul>
      </section>
    </Layout>
  );
}
```

<style>
  .slidev-layout {
    --slidev-code-font-size: 0.5rem;
    --slidev-code-line-height: calc(0.5rem * 1.5);
  }
</style>

<!--
So the first thing we need to do is to import the `useFeatureFlagEnabled` hook from posthog. And this does exactly what it's name says. We pass it the feature flag key that we created earlier and it will return a true or false value. If it's not enabled or the API call fails we show a message telling users to come back at 12
-->
---
layout: comparison
clicks: 2
---

## Result

::a:: 

<div v-click="1">
<img src="/blog-page.png" class="w-158"  />
</div>

::b::
<div v-click="2">
<img src="/grand-opening.gif" class="w-158"  />
</div>

<!--
And that it, we've now got a feature flag controlling the visibility of our blog page. If it's enabled we show our posts or we show a message teasing users to come back later
-->

---
clicks: 1
---

A/B tests?

<div v-click="1">
<img src='/release-condition-1.png' class='w-300' />
</div>

<!--
We just need to go back to our dashboard in posthog and alter the amount of users we want release to. It does this by instrumenting your application and working out roughly how many users are using your website. One caveat to this is that from what I've heard it takes a few days to work that out so you might not get the most accurate results straight away.
-->

---

Overrides?


<img src='/hmm.gif' class='w-100' />

<!--
And last but not least overrides. So we've delivered our feature, client is happy and we have our feature flag and a/b test all working, but our client wants to check it out and make sure everything is to their liking on production before we start percentage releasing.
-->

---
clicks: 1
---

Toolbar

<div v-click="1">
<img src="/tb.png" class='w-130' />
</div>

<!--
In posthog we have this thing called the toolbar. The toolbar is a little widget that you embed in your website and it allows you to override feature flags on and off dead easily.
-->

---

<div style="position: relative; padding-bottom: 56.25%; height: 0;"><iframe src="https://www.loom.com/embed/d1225ed7ebdf4f23a697b61f289ed5b0?sid=a4757ff3-9ff3-4048-b808-8dec8bdc8e5d" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

<!--
Enabling this for our site is super easy. All we need to do is give it access to our site and then we can override our feature flags on and off.
-->

---

## Thanks!

Slides 
- https://feature-flags-24.talks.lhowsam.com 
- https://feature-flags-24.talks.lhowsam.com/presenter


### Resources:

Repositories
- Redis self-hosted feature flag service - https://dub.sh/rdabtest
- Posthog example - https://dub.sh/lhabtest

Feature flagging services 
- self hosted feature flagging service - https://unleash.github.io/
- Config cat - https://configcat.com/
- Launch Darkly - https://launchdarkly.com/
- Posthog - https://posthog.com/
