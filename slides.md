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

<!--
 at the moment I work for sky bet as a developer. I've been a developer for about two years and a QA engineer for about the same amount of time before that. I use feature flags and a/btesting quite a lot at work and wanted to introduce you to all the cool stuff you can do with them. During the talk if you have a question, stick your hand up and I'll try to answer it as best as I can. Obviously we'll try to keep conversations succinct so we don't get off track but if they start to get a bit too long, we can always chat after the talk. Today we're going to be talking about feature flags and why you might want to use them.
-->

---
layout: center
---

* Software delivery
* What are feature flags
* What is a/b testing
* Industry usage
* Typical code patterns w/ feature flags and a/b tests
* Real world example with PostHog

<!-- background on software delivery, quick explanation of feature flags and a/b tests, who uses them, general code patterns and how to structure flags and a/b tests in your project and we're gonna finish off with a real world example with something called PostHog -->

---
layout: comparison
clicks: 6
---

## How do we deliver software


<div v-click="1">
<p>Feature / need</p> 
</div>

<div v-click="2">
<p>refine + estimate</p>
</div>

<div v-click="3">
<p>development happens</p>
</div>

 
<div v-click="4">
<p>testing</p>
</div>


<div v-click="5">
<p>release</p>
</div>


<div v-click="6">
<p class='text-red'>What happens when something goes wrong at one of these stages?</p>
</div>

<!--
Before we get into feature flags and why they're great, I wanted to talk a little bit on how most of us deliver software. I'll try not to bore you, sure we all hear enough about agile and scrum practices at work. We usually get a feature requested or a business need come thru, we then refine that with a BA or a project manager (business analyst), development happens, QA gets involved make sure its ok and then we release it. But what happens when things go wrong or we need to move faster. Perhaps your backend dev goes on holiday for 3 weeks and all your frontend is work is ready to go but you haven't got any api endpoints to hit. Or maybe the big feature you deployed to production blows everything up and causes a horrible experience for your users. Well this is where feature flags can help you out and take a lot of stress out of everyone's day
-->

---

## What are feature flags?

You can think of feature flags like light switches.

<img src="/homer-light-switch.gif" class="m-2" />

<!--
feature flags are a way to control the visibility of features in your app. They're a way to programatically features on and off in your app and this. They're usually paired with weighting algorithms allows you to release in small increments. you don't want to release a feature to 100% of your users, you want to slowly release and this allows us to deliver safer experiences to our users. 
-->

---
---

# what is a/b testing?

todo


---
clicks: 2
---

## Quick example

<div v-click='1'>

<img src='/feature-example.png' class='w-150' />
</div>


<div v-click="2">
<img src='/amazon-recs.png' class='w-150' />
</div>

<!--
We have a new feature > we control that via a feature flag and based on whether it's enabled we determine whether to present a feature to a user. As an example, here are my amazon recommendations. You can see I'm getting some new show on prime video recommended to me along with fashion and some beauty products. I doubt this is how this works in real life but let's pretend for a bit. These cards could be controlled under a feature flag based on what the marketing department wants to do. Perhaps they are testing whether people click the mr and mrs smith card from the homepage to see if it boosts views. If it boosts views, they might keep that feature flag turned on. Otherwise they might turn it off and find a new way to drive engagement. This way they're able to dynamically control what content a user sees or doesn't see and gather data based on it.
-->

---

## Benefits

<img src="/fargo.gif" class="m-2 w-80" />

<!--
So now we know roughly what a feature flag is and how it might be used, you might be thinking  what's in it for me and my projects? So I've popped together a few examples on what you can use feature flags for
-->

---
layout: comparison
clicks: 2
---

## Benefits


A/B Testing / variant testing

::a::

<div v-click="1">
<img src="/black-button-feature.png" class="m-1" />
</div>

::b::

<div v-click="2">
<img src="/red-button-feature.png" class="m-1" />
</div>

<!--
Feature flags are a great way to temporarily expose your users to things such as alternate designs, new color schemes to see if that drives higher click rates etc. Here we've got two designs, one with a black button and one with a bright red button. You can combine this with staggered rollouts where you release to small subsets of users to test whether user's like the first design or the last design. It's called a/b or variant testing because you're exposing a user to a or b. variant black button or variant red button
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
maybe your app is undergoing maintenance or the backend that you're talking to is broken and you don't want to show users broken functionsality, bannering your site with a feature flag while you're fixing things would be a great option for that
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
This is one of my favorite things to do with feature flags. Most feature flag providers have a way of overriding a disabled feature flag. So you can release your work under a disabled feature flag and use something such as a query parameter or a cookie to allow QA engineers, stakeholders view the work in production without potentially releasing something broken to your users
-->

---
layout: comparison
---

## Benefits

Percentage rollouts

<img src="/perc.png" class="m-1" />

You can release your feature to a percentage of your users instead of everyone all at once

<!--
Instead of activating a feature for all users at once, we can activate features in segments to a growing percentage of users. We might decide to roll a feature out in 25% increments or we may be a bit more risk averse and only release to 5% of users at a time to see if something goes wrong. This works on spliting your user base into different cohorts - one with the feature flag enabled 25% and one with the feature flag disabled 75%. This requires some sophisticated management of state and is not so easily implemented. That's why it's best to rely on an established feature flag service such as LaunchDarkly, aws cloudwatch evidently etc. The crux of the problem is that you need some way of identifying a user in order to determine what cohort to put them in. Not so hard if you've got user authentication as you can just determine the total users of your service and then do some maths to get 10%. But if you're just running a public website, it's harder to determine what buckets to put a user in and it needs a bit of thought on how you want to proceed with that.
-->

---
layout: comparison
---

## Benefits

Segmented rollouts

<img src="/perc.png" class="m-1" />

Admins, Moderators, certain teams etc.

<!--
Perhaps you want to release to certain groups only, and see if your feature has a positive impact. Similar to percentage based rollouts but we are exposing feature to users with specific attributes. Such as only paid users, admins, etc.
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
Feature flags are very prevelant in the industry. Just to name a few Airbnb, GitHub, Netflix. Risk Mitigation: It helps them reduce risk and saves them lots of money. For a lot of these companies 10 - 15 minutes of service disruption means lots of cash gets burned. Feature flags are usually combined with some sort of weighting algorithm so that features are rolled out gradually to percentages of users instead of everyone all at once. If a feature goes bang, then we're not affecting 100% of our user base. Performance: Your new feature might be calling some other services and businesses will use feature flags to slowly roll out a feature
-->

---

# Feature flag code patterns

<!-- we're going to go over the two primary patterns for creating feature flags and then we're going to look at a quick demo on how it would be used in the real world -->

<img src="/giphy.gif" class="w-78" />


---

## General structure of a feature flag

```ts{2|3|4|5|6,7,8|9}

{
  "name": "new-feature",
  "description": "A new feature",
  "enabled": true,
   "overides": {
    "cookie": "new-feature=true",
   },
   "percentage": 10
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
    name: 'talks',
    description: 'Whether to show the talks page',
    enabled: false,
    overrides: {
    name: 'show-talks',
    value: true,    
  },
    percentage: 10,
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
Using a central file in your codebase. Simple way of getting started with feature flags.We've got somesimple fields here, the feature name, a description, whether it's enabled,some way of overriding the feature flag (in this case we're using a cookie) and finally a percentage (bear in mind this will only work if you have some way of doing maths and figuring out how to identify a user) 
. If after this talk you're wondering which one to use, ask yourself this question:
Do I need to be able to change the feature flag without a code change? If the answer is yes, then you should use a third party service. If the answer is no, then you can use a central file in your codebase to store your feature flags.
-->

---
layout: comparison
---

Central file based feature flag implementation


```typescript
// src/feature-flags.ts

export const featureFlags: FeatureFlag[] = [
  {
    name: 'talks',
    description: 'Whether to show the talks page and navigation item',
    enabled: false,
    overrides: {
      name: 'show-talks',
      value: true,
    },
    percentage: 10,
  },
];
```


---

Central file based feature flag implementation


```typescript{2|4|6|7|9|11,12,13|15|17,18|20}
// src/useFeatureFlag.ts
import featureFlags from '@frontend/utils/featureFlags';

const AllowedFeatureFlags = ['new-feature', 'another-feature'] as const;

type AllowedFeatureFlag = typeof AllowedFeatureFlags[number];

const useFeatureFlag = (name: AllowedFeatureFlag): boolean => {
  const featureFlag = featureFlags.find(flag => flag.name === name);

  if (!featureFlag) {
    return false;
  }

  const cookie = parseCookie(featureFlag?.overrides.name);

  const isCookieOverrideSet =
    cookie?.name === featureFlag?.overrides.name && cookie?.value === 'true';

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
We import our array of feature flags. Firstly we've got some typescript definitions here that just restrict what we're allowed to pass to the useFeatureFlag hook., and then try to find the flag that the user passed to the hook. If we can't find it, we return false just to be safe. If we have found a flag, we try to look for a cookie based on the override object that we set on the feature flag to see if someone is trying to provide a cookie to view the feature when it's off. If the cookies name and value matches what we set in the feature flag array earlier, we return true. Otherwise we return whatever the enable value of the feature flag is.
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
---


---
--- 

todo: a/b testing code patterns



---
layout: center
---

# Real world example

<img src="/cat-laptop.gif" class="w-78"  />

<!--
Now that we know a bit what a typical feature flag looks like, let's look at a real world demo with posthog
-->

---
layout: center
---

## Our client wants an engineering blog to be added to their site

<img src="/blog-page.png" class="w-350"  />

<!--
We have a problem. Our client wants to make a grand reveal of their new blog feature on their site. It's going to be super popular and everyone is going to love it. But they want the ability to turn it on themselves, almost like a ribbon cutting. Our goal with this exercise is to control this new feature with a feature flag.
-->

---
layout: center
---

## Posthog

<img src="/posthog.png" class="w-350"  />

<!--
To achieve this, we'll be using posthog. Posthog is a really good feature flagging and a/b testing platform. It also a generous free tier and other goodies that we're going to take a quick look at
-->

---

## Creating a feature flag


<!-- so to create a feature flag in posthog, it's really simple. a key (this is what will be used in our frontend code), We just need to give it a descriptive name, and what users we want to release to. we can also release to certain segments of users based on lots of things built into posthog such as browser version, region or something unique such as their user ID -->


<img src="/create-posthog.png" class="w-350"  />


---
layout: center
---

The current state of our client's codebase


```typescript 
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
Before we get started with integrating our app with posthog, let's have a peak at the current state of play. Our codebase is fairly simple, for demo purposes. We just have a homepage that loops over some posts and displays them in a list with a link to go to the blog post. For anyone unfamiliar with Next.js, we fetch our posts in this `getServerSideProps` function. All this does is fetch data at runtime on the server side before we render any html. We then pass that data (in this case our posts) to our HomePage component. Turn turn this page into something that's controlled by our client via a feature flag, it's super simple
-->

---
clicks: 2
---

## Add the SDK to your project  

<!-- The first thing we need to do, is add the posthog sdk to our project. All we do is install the dependency, and add our API keys to environment variables
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

## Using the feature flag to determine what to show

```typescript{1|4|6|7,8,9,10,11,12|16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32}
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
Now we pass posts and enableBlogFeature feature flag down to our page. If the feature flag is enabled we show the blog posts if not we just let the user know that the feature is disabled
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


---

Overrides ????


<img src='/hmm.gif' class='w-100' />

<!--
This is great and everything, we have our feature flag setup, but what if we want our testers to be able to verify this works or perhaps our client wants to check it out and make sure everything is to there liking? like we mentioned before a little earlier in the talk, we can override feature flags without turning them on for everyone.
-->

---
clicks: 1
---

Toolbar

<div v-click="1">
<img src="/toolbar.png" class='w-70' />
</div>

<!--
in posthog we have this thing called the toolbar. The toolbar is a widget like tool you can allow posthog to embed in your website.
-->

---

<div class='mt-15'>
<img src="/auth-urls.png" class='w-750' />
</div>

<!--
if we click into this we can see we have these authorised URLs. You can see I've got a few of my domains here as I use posthog for my website. Since we've authorised it for localhost, let's visit our client's website and see what shows up
-->

---

<!-- Potential for this to be a live demo - check instead -->
<SlidevVideo  controls>
  <!-- Anything that can go in a HTML video element. -->
  <source src="/live-example.mp4" type="video/mp4" />
</SlidevVideo>


---

# Thanks!

### Resources:


Slides 
- https://fe-talk-2024.vercel.app/ + https://github.com/luke-h1/fe-talk-2024


Feature flagging services 
- self hosted feature flagging service - https://unleash.github.io/
- Config cat - https://configcat.com/
- Launch Darkly - https://launchdarkly.com/
- Posthog - https://posthog.com/


Repositories
- Slides - TODO
- Redis self-hosted feature flag service - https://github.com/luke-h1/feature-flag-next
- Config cat example - https://github.com/luke-h1/config-cat-next
