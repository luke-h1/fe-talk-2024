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

<p class='mb-6 text-pink'> A safer way of releasing software
</p>

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
    Typescript, DevOps, anything frontend :) 
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
I'm a dev, working at sky betting and gaming at the mo. I've been a dev for about two years and a QA engineer for about the same amount of time before that. Love anything frontend or devops related. Got my socials there if you wanna continue the conversation or have any questions. During the talk if you have a question, stick your hand up and I'll try to answer it as best as I can. Obviously we'll try to keep conversations succinct so we don't get off track but if they start to get a bit too long, we can always chat after the talk.
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


<!-- align to left -->
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
background on software delivery, quick explanation of feature flags and a/b tests, who uses them, general code patterns and how to structure flags and a/b tests in your project and we're gonna finish off with a real world example
-->

---
layout: comparison
clicks: 7
---

## Software delivery

<div v-click="1">
<p class='text-green'>Feature / need ✅</p> 
</div>

<div v-click="2">
<p class='text-green'>refine + estimate ✅</p>
</div>

<div v-click="3">
<p class='text-green'>development happens ✅</p>
</div>

 
<div v-click="4">
<p class='text-green'>testing ✅</p>
</div>


<div v-click="5">
<p class='text-green'>release to prod ✅</p>
</div>


<div v-click="6">
<p class='text-red'>Kaboom 🧨 💣</p>
</div>

<div v-click="7">
<p class='text-red'>Slow 🐌</p>
</div>

<!--
Before we get into feature flags and why they're great, I wanted to talk a little bit on how most of us deliver software. We usually get a feature requested or a business need come thru, we then refine that with a BA or a project manager (business analyst), development happens, QA gets involved make sure its ok and then we release it. This process works great alebit a little slow 90% of the time. But what happens when things go wrong or we need to move faster. Perhaps your backend dev goes on holiday for 3 weeks and all your frontend is work is ready to go but you haven't got any api endpoints to hit. Or maybe the big feature that works fine in staging blows everything up when you deploy it to production and causes downtime for everyone. Well this is where feature flags can help you out and take a lot of stress out of everyone's day
-->

---
layout: two-cols
clicks: 1
---

## Feature flags 🤔 ???

<img src="/homer-light-switch.gif" class="m-2 w-70 h-70" />


::right::

<div v-click='1'>

```typescript
const HomePage = () => {
  const newFeature = false;


  return newFeature ? <NewFeature /> : <OldFeature />;
}
```
</div>

<style>
  .slidev-layout {
    --slidev-code-font-size: 0.7rem;
    --slidev-code-line-height: calc(0.7rem * 1.5);
  }
</style>

<!--
feature flags are a way to control the visibility of features in your app. They're a way to programatically features on and off in your app. All a feature flag is at its core is a true or false value. we flip the switch and we get light we flip it again and the lightbuld goes off.
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
A/B testing is a way to expose your users to two different versions of a feature. We conduct an a/b test by running an experiment and that usually involves two variants, a control group (user has the existing functionallity) and an experiment group (user sees the new feature). In the context of feature flags and the scope of this talk, we're just using a/b testing to control what percentage of users see our new feature.
-->

---

## a/b test flow

<img src='/ff-ex.png' class='w-350' />

<!--
So as a quick example, this is the typical flow of a feature flag paired with a/b testing. Very similar to the last diagram. We have a new feature, if the feature flag is off, we show the existing functionality. If it's on, we show the new feature. But the difference is we then use an a/b test to control the amount of users that see this feature. So in this case 40% of our userbase sees the new functionality and 60% see the old functionality.
-->

---
layout: two-cols
---

## a/b test example

<img src='/amazon-rec-1.png' class='w-350' />

<!--
As a real world example, I got this show recommended to me on Amazon.I doubt this is how this works in real life but let's pretend. The poster for this show could be controlled under a feature flag along with an a/b test based on what the marketing department wants to do. They might be testing whether people click the show from the homepage based on the poster. If lots of people click this image, they might keep that feature flag turned on and release this to 100% of users. Otherwise they might try different posters to see what people like best. This way they're able to dynamically control what content a user sees or doesn't see while not having to talk to developers too much. Bear in mind it takes a bit of work to setup proper analytics and monitoring for this kind of thing, but once you've got that down, it's a great way to keep track of what your users like and don't about your site.
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
Feature flags are a great way to temporarily expose your users to things such as alternate designs, new color schemes to see if that drives higher click rates etc. Here we've got two designs, one with a black button and one with a bright red button. You can combine this with releasing to a small subsets of users to test whether user's like the first design or the last design
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
maybe your app is undergoing maintenance or the backend that you're talking to is broken and you don't want to show users broken functionsality, bannering your site with a feature flag while you're fixing things would be a great option for that. So our site might normally look like this, and when we enable the error banner flag, our site might look like this
-->

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

<!--
This is one of my favorite things to do with feature flags. Most feature flag providers have a way of overriding a disabled feature flag. So you can release your work to production under a disabled feature flag and use something such as a query parameter or a cookie to allow QA engineers, stakeholders etc. view the work in production without the rest of your users seeing it
-->

---
layout: comparison
---

## Benefits

Percentage rollouts

<img src="/perc-rollout.png" class="m-1" />

You can release your feature to a percentage of your users instead of everyone all at once

<!--
We've touched on this a bit already and this is what we'll be using a/b testing for. Instead of activating a feature for all users at once, we can activate features in segments to a growing percentage of users. We might decide to roll a feature out in 25% increments or we may be a bit more risk averse and only release to 5% of users at a time to see if something goes wrong. This works on spliting your user base into different cohorts - one with the feature flag enabled 25% and one with the feature flag disabled 75%. This requires some sophisticated management of determining how many users you have and is not so easily implemented. You can do some rough maths to implement your own a/b testing platform but it won't be 100% accurate (we'll get into that a bit later). That's why it's best to rely on an established feature flag service such as LaunchDarkly, aws evidently things which instrument your application and determine how many users you have
-->

---
layout: comparison
---

## Benefits

Segmented rollouts

<img src="/segment-rollout.png" class="m-1" />

Admins, Moderators, certain teams etc.

<!--
Similar to percentage based rollouts but we are exposing features to users with specific attributes.This could be something such as only releasing to admins, paid users, users in a certain region etc.
-->

---
clicks: 8
layout: comparison
---

## Who uses them?


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

<div v-click="5">
<img src='/spotify-logo-1y.jpg' class="m-1 w-20" />
</div>
</div>

<div class='mt-5'>

<div v-click="6">
 <Star /> Risk mitigation 💰
</div>
<div v-click="7">
 <Star /> Roll out big features incrementally 🚀
</div>
<div v-click="8">
 <Star /> Performance 🚦
</div>
</div>

<!--
Feature flags are very prevelant in the industry. Just to name a few Airbnb, GitHub, Netflix. Risk Mitigation: It helps them reduce risk and saves them lots of money. For a lot of these companies 10 - 15 minutes of service disruption means lots of cash gets burned
-->

---

# Feature flag code patterns

<!-- we're going to go over the two primary patterns for creating feature flags + a/b tests and then we're going to look at a quick demo on how it would be used in the real world. -->

<img src="/giphy.gif" class="w-78" />


---

## General structure of a feature flag

```ts{2|3|4|5|6,7,8|9}

{
  "name": "new-feature",
  "description": "A new feature",
  "enabled": true,
   "overides": {
    "cookie": "new-feature",
    "value": "true"
   },
}

```


---
clicks: 2
layout: comparison
---

## Implementation

::a:: 
<div v-click="1">

> Using a central file in your codebase to store your feature flags

<br />
<br />


```typescript
// src/feature-flags.ts

const featureFlags: FeatureFlag[] = [
  {
    name: 'redesign-2024',
    description: 'new redesigned page',
    enabled: false,
    overrides: {
    name: 'show-redesign-2024',
    value: true,    
  },
},
];
export default featureFlags;
```
</div>


::b::

<div v-click="2" class="mt-6">

> Using a third party service such as posthog or your own feature flag API

<br />

```typescript
// src/feature-flags.ts

const MyComp = () => {
  const newFeat = fetchFromService('new-feature');
  return newFeat ? <NewFeat /> : <OldFeat />;
};
```
</div>

<!--
Using a file in your codebase. Simple way of getting started with feature flags. We've got some simple fields here, the feature name, a description, whether it's enabled,some way of overriding the feature flag (in this case we're using a cookie)
-->

---
layout: comparison
---

file based feature flag implementation


```typescript
// src/feature-flags.ts

export const featureFlags: FeatureFlag[] = [
  {
    name: 'redesign-2024',
    description: 'Redesigned page',
    enabled: false,
    overrides: {
      name: 'redeisgn-2024',
      value: true,
    },
  },
];
```


---

file based feature flag implementation


```typescript{4|5|7,8,9|11|13,14|16}
// src/useFeatureFlag.ts
import featureFlags from '@frontend/utils/featureFlags';

const useFeatureFlag = (name: string): boolean => {
  const featureFlag = featureFlags.find(flag => flag.name === name);

  if (!featureFlag) {
    return false;
  }

  const cookie = parseCookie(featureFlag.overrides.name);

  const isCookieOverrideSet =
    cookie.name === featureFlag.overrides.name && cookie.value === 'true';

  return featureFlag.enabled || isCookieOverrideSet;
};


```

<style>
  .slidev-layout {
    --slidev-code-font-size: 0.6rem;
    --slidev-code-line-height: calc(0.6rem * 1.5);
  }
</style>

<!--
We import our array of feature flags and then try to find the flag that the user passed to the hook. If we can't find it, we return false just to be safe. If we have found a flag, we try to look for a cookie based on the override object to see if someone is trying to provide a cookie to view the feature when it's off. If the cookies name and value matches what we set in the feature flag array earlier, we return true. Otherwise we return whatever the enable value of the feature flag is.
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


---
clicks: 4
---

## a/b testing code patterns


<div v-click="1">
  <Star /> Self hosted
</div>

<div v-click="2">
  <Star />Using a service such as LaunchDarkly or PostHog
</div>


---
layout: center
---

# Real world example / a/b testing with posthog

<img src="/cat-laptop.gif" class="w-78"  />

<!--
Now that we know a bit what typical feature flags and a/b tests looks like and how to use it, let's look at a real world demo with posthog
-->

---
layout: center
---

## Our client wants an engineering blog to be added to their site

<img src="/blog-page.png" class="w-120"  />

<!--
We have a problem. Our client wants to make a grand reveal of their new blog feature on their site. They're projected to get 100k users and everyone is going to love it. But they're not sure if their website can handle the traffic. So our goal with this exercise is to control this new feature with a feature flag and a/b test it to a small percentage of users to make sure this amazing blog isn't going to blow up their site
-->

---
layout: center
---

## Posthog

<img src="/posthog.png" class="w-350"  />

<!--
To achieve this, we'll be using posthog. Posthog is a really good feature flagging and a/b testing platform. It's a generous free tier (about a million free requests a month or something like that) and other goodies that we're going to take a quick look at
-->

---

## Creating a feature flag

<!-- So to create a feature flag in posthog, it's really simple. We need a key (this is what will be used in our frontend code), a descriptive name, and what users we want to release to. This is caleld a release condition in posthog and we can also release to certain segments of users based on lots of things built into posthog such as browser version, region or something unique such as their user ID if you have authentication -->


<img src="/create-posthog.png" class="w-350"  />


---
layout: center
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

<!-- Let's get on with adding posthog to our project. The first thing we need to do, is add the posthog sdk to our project. All we do is install the dependency, and add our API keys to environment variables.
-->

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
So the first thing we need to do is to import the `useFeatureFlagEnabled` hook from posthog. And this does exactly what it's name says. We pass it the feature flag key that we created earlier and it will return a true or false value. If the flag is disabled we return a message to the user saying come back at 12pm for the grand opening. Otherwise we return the list of blog posts as we did before.
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
clicks: 2
---

What about a/b testing?

<div v-click="1">
<img src='/release-condition-1.png' class='w-100' />
</div>

<!--
We just need to go back to our console in posthog and alter the release condition to the amount of users we want release to. It does this by instrumenting your application and working out roughly how many users are using your website. One caveat to this is that from what I've heard it takes a few days to work that out so you might not get the most accurate results straight away.
-->

---

Overrides?


<img src='/hmm.gif' class='w-100' />

<!--
And last but not least overrides. So we've delivered our feature, the client is happy, we have our feature and a/b test all working, but our client wants to check it out and make sure everything is to there on production. Like we mentioned before a little earlier in the talk, this isn't a problem.
-->

---
clicks: 1
---

Toolbar

<div v-click="1">
<img src="/toolbar.png" class='w-70' />
</div>

<!--
in posthog we have this thing called the toolbar. The toolbar is a little widget that you embed in your website.
-->

---

<div class='mt-15'>
<img src="/auth-urls.png" class='w-750' />
</div>

<!--
All we have to do is give it access to embed into our site. Since we've authorised it for localhost, let's visit our client's website and see what shows up
-->

---

<SlidevVideo  controls>
  <source src="/live-example.mp4" type="video/mp4" />
</SlidevVideo>

<!--
You can see we've got a little widget that allows to turn the feature flag on super easily.
-->

---

## Thanks!

Slides 
- https://feature-flags-24.talks.lhowsam.com


### Resources:

Repositories
- Slides - https://dub.sh/felho + 
- Redis self-hosted feature flag service - https://dub.sh/rdabtest
- Posthog example - https://dub.sh/lhabtest

Feature flagging services 
- self hosted feature flagging service - https://unleash.github.io/
- Config cat - https://configcat.com/
- Launch Darkly - https://launchdarkly.com/
- Posthog - https://posthog.com/
