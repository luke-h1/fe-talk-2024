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

## A safer way of releasing software

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


<!-- at the moment I work for sky bet
been there for just under a year now, been a developer for about two years and a QA engineer for about 2 years before that. Today we're going to be talking about feature flags and why you might want to use them -->
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


<!-- Before we get into feature flags and why they're great, I wanted to talk a little bit on how most of us deliver software. I'll try not to bore you, sure we all hear enough about agile and scrum practices at work. We usually get a feature requested or a business need come thru, we then refine that with a BA or a project manager (business analyst), development happens, QA gets involved make sure its ok and then we release it. But what happens when things go wrong or we need to move faster. Perhaps your backend dev goes on holiday for 3 weeks and all your frontend is work is ready to go but you haven't got any api endpoints to hit. Or maybe the big feature you deployed to production blows everything up and causes a horrible experience for your users. Well this is where feature flags can help you out and take a lot of stress out of everyone's day -->

---

## What are feature flags?

You can think of feature flags like light switches.

<img src="/homer-light-switch.gif" class="m-2" />


<!-- feature flags are a way to control the visibility of features in your app. They're a way to programatically features on and off in your app. They're usually paired with weighting algorithms allows you to release in small increments. you don't want to release a feature to 100% of your users, you want to slowly release. Now that we know what a feature flag is, who uses them?
-->

--- 
---

## Example

add an example of turning a feature flag on and off here - via a gif perhaps. rework the section here to transition into benefits and then who uses them

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


<!-- This is one of my favorite things to do with feature flags. Most feature flag providers have a way of overriding a disabled feature flag. So you can release your work under a disabled feature flag and use something such as a query parameter or a cookie to allow your QA engineers, stakeholders view the work in production without potentially releasing something broken to your users -->


---
layout: comparison
---

## Benefits

Percentage rollouts

<img src="/perc.png" class="m-1" />

You can release your feature to a percentage of your users instead of everyone all at once


<!-- Instead of activating a feature for all users at once, we can activate in in segments to a growing percentage of users. We might decide to roll a feature out in 25% increments or we may be a bit more risk averse and only release to 5% of users at a time to see if something goes wrong. We split the user base into different cohorts - one with the feature flag enabled 25% and one with the feature flag disabled 75%. This requires some sophisticated management of state and is not so easily implemented. That's why it's best to rely on services such as LaunchDarkly, aws cloudwatch evidently etc. The crux of the problem is that you need some way of identifying a user. Not so hard if you've got user authentication as you can just determine the total users of your service and then do some maths to get 10%. But if you're just running a public website, it's harder to determine what buckets to put a user in -->


---
layout: comparison
---

## Benefits

Segmented rollouts

<img src="/perc.png" class="m-1" />

Admins, Moderators, certain teams etc.


<!-- Perhaps you want to release to certain groups only, and see if your feature has a positive impact -->


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
<!-- Feature flags are very prevelant in the industry. Just to name a few Airbnb, GitHub, Netflix. Risk Mitigation: It helps them reduce risk and saves them lots of money. For a lot of these companies 10 - 15 minutes of service disruption means lots of dollars lost. Feature flags are usually combined with some sort of weighting algorithm so that features are rolled out gradually to percentages of users instead of everyone all at once. If a feature goes bang, then we're not affecting 100% of our user base. Performance: Your new feature might be calling some other services and businesses will use feature flags to slowly roll out a feature -->


---
---

# Feature flag code patterns

<!-- we're going to go over the two primary patterns for creating feature flags and then we're going to wrap up with a quick demo on how it would be used in the real world -->

<img src="/giphy.gif" class="w-78" />

--- 
---

## General structure of a feature flag

```ts{2|3|4|5|6|7|9}

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

const featureFlags = {
  newFeature: {
    enabled: true,
    percentage: 10,
  },
   useNewApi: {
    enabled: true,
    percentage: 100,
    description: "Whether to use the new API. Setting to false will use the old API in case of issues.",
    overides: {
      cookie: "new-api=true",
    }
  },
};
export default featureFlags;
```
</div>


::b::

<div v-click="2">

> Using a third party service such as config cat or your own feature flag API

<br />

```typescript
// src/feature-flags.ts

const MyComp = () => {
  const newFeat = fetchFromService('new-feature', false);
  return newFeat ? <NewFeat /> : <OldFeat />;
};
```
</div>


<!-- If after this talk you're wondering which one to use, I'd suggest asking yourself this question:
Do I need to be able to change the feature flag without a code change? If the answer is yes, then you should use a third party service. If the answer is no, then you can use a central file in your codebase to store your feature flags. For simplicity we're going to be using a file based feature flag -->


--- 
layout: comparison
---


Central file based feature flag


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
---

---
layout: center
--- 

# Real world example

<img src="/cat-laptop.gif" class="w-78"  />

<!-- Now that we know a bit what a typical feature flag looks like, let's look at a real world demo with config cat-->



--- 
layout: center
--- 

## Our awesome blog site is going live 🥳🎉

<img src="/blog-page.png" class="w-78"  />

<!-- our goal with this exercise is to control this blog site with a feature flag. Perhaps we have a grand opening of our website and we want to do a big reveal at lunch time -->


--- 
layout: center
--- 
## Config cat

<img src="/config-cat.png" class="w-78"  />


<!-- To achieve this, we'll be using config cat. config cat is a really good feature flagging service. It also a generous free tier and other goodies that we're going to take a quick look at -->


--- 
--- 

## Creating a feature flag


<!-- so to create a feature flag in config cat, it's really simple. We just need to give it a descriptive name, a key (this is what will be used in our frontend code) and a bit of metadata -->

<img src="/create-ff-2.png" class="w-350"  />

TODO: make a gif of this perhaps / more interactive

---
--- 

## Add any percentages or segmentation you want to use

<img src="/percentage.png" class="w-350"  />


<!-- if you only want to expose it to certain amount of users, you can control the percentages as well as create user segments -->

--- 
clicks: 4
--- 

## Add the SDK to your project  

<!-- this is probably the simplest part I'd argue, it's super easy to get started. All we do is install the dependency, import it, and then move on to data fetching. We get the feature flag we want by calling `getValueAsync`, with a default value of false if the API call to config cat fails for any reason and then return the flag along with the posts -->

<div v-click="1">

```typescript
pnpm i configcat-js-ssr
```

</div>


<div v-click="2">

```typescript
import * as configcat from "configcat-js-ssr";
```
</div>

<div v-click="3">

```typescript 
export const getServerSideProps: GetServerSideProps<Props> = async () => {
  const client = configcat.getClient(process.env.NEXT_PUBLIC_CONFIGCAT_SDK_KEY);

  // default value of false if the API call fails
  const enableBlogFeature = await client.getValueAsync("blogFeature", false);
  const posts = getSortedPosts();

  return {
    props: {
      enableBlogFeature,
      posts,
    },
  };
};
```
</div>


--- 
--- 

## Using the feature flag to determine what to show

```typescript 
export default function Home({ posts, enableBlogFeature }: Props) {
  return (
    <>
      {enableBlogFeature ? (
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
      ) : (
        <div className="card">
          <h2>Feature is off</h2>
        </div>
      )}
    </>
  );
}
```

<!-- Now we pass posts and enableBlogFeature feature flag down to our page. If the feature flag is enabled we show the blog posts if not we just let the user know that the feature is disabled -->


--- 
layout: comparison
clicks: 2
--- 

## Result 


::a:: 

<div v-click="1">
<img src="/blog-page.png" class="w-78"  />
</div>

::b::
<div v-click="2">
<img src="/feature-off.png" class="w-78"  />
</div>


--- 
--- 

# Finito / Question time



### Resources:


Slides 
- https://fe-talk-2024.vercel.app/ + https://github.com/luke-h1/fe-talk-2024


Feature flagging services 
- self hosted feature flagging service - https://unleash.github.io/
- Config cat - https://configcat.com/
- Launch Darkly - https://launchdarkly.com/


Repositories
- Slides - TODO
- Redis self-hosted feature flag service - https://github.com/luke-h1/feature-flag-next
- Config cat example - https://github.com/luke-h1/config-cat-next

