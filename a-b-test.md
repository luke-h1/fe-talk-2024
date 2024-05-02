
---
clicks: 4
---
## a/b testing code patterns


<div v-click="1">
  <Star /> Self hosted
</div>

<div v-click="2">
  <Star /> Using a service such as LaunchDarkly or PostHog
</div>



<!-- I've split this into two different sections. Self hosted and using a service. The main reason I've done this is that self hosting can be a decent option if you're in a hurry and want to quickly build something that does the There are a few caveats to building your own a/b testing service that I'm going to warn you about as we get into examples-->


---
---

```typescript 
import redis from "@/util/redis";
import type { NextApiRequest, NextApiResponse } from "next";

export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse
) {
  const KEY = 'new-design-experiment';

  // would need to set custom redis keys if we were running multiple experiments
  switch (req.method) {
    case "GET":
      const response = (await redis.get(KEY)) || "0";
      console.info("[GET counter]: Retreived count", response);
      return res.status(200).json({ count: response });

    case "POST":
      const count = await redis.incr(KEY);
      console.info("[POST counter]: Incremented count", count);
      return res.status(200).json({ count });

    default:
      return res.status(405).end();
  }
}

```
<!-- I'm going to start off this example with the server side logic we need to persist our a/b test. If you've never done server side js, don't worry it's super simple. All we have here is a Next.js API route handler. This provides us with a http endpoint that we can make requests to. The main reason we're using it is to retrieve and store information in something called redis. Redis is just a key value database, if you've never used it you can think of it like a js object that you can store data in. We have two endpoints here, get and post. All the get endpoint does is retrieve the count of how many users have seen our new feature. The post endpoint increments the count by one. We're using this to persists how many users have seen our new feature. -->

---
---

```typescript{5|6|7|10|11|13|15|17|18|20|24|25,26,27,28|29}
import { useEffect, useState } from "react";
import Cookies from "js-cookie";

const useAbTesting = () => {
  const [variant, setVariant] = useState<"control" | "experiment">("control");
  const cookieName = "new-redesign-experiment-2024";

  useEffect(() => {
    const getAndSetVariant = async () => {
      let abTest = Cookies.get(cookieName);
      const { count } = await fetch("/api/experiment").then((res) => res.json());

      const TOTAL_USERS = 100;

      const FIFTY_PERCENT_OF_USERS = TOTAL_USERS / 2;

      if (!abTest && parseInt(count) < FIFTY_PERCENT_OF_USERS) {
        Cookies.set(cookieName, "experiment");

        const res = await fetch("/api/experiment", {
          method: "POST",
        }).then((res) => res.json());

        setVariant("experiment");
      } else {
        Cookies.set(cookieName, "control");
        setVariant("control");
      }
      return variant;
    };

    getAndSetVariant();
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, []);
};
export default useAbTesting;
```

<!-- Now here we have our hook where we're going to make use of those api endpoints. So the first thing we're doing in this hook is setting two state variables, variant and setVariant. Variant can either be control (the user who doesn't see the feature) and experiment (the user who sees the new functionality). Next up we are running a useEffect on mount, so this will run when the page loads once. And now into the main part. We have this function called 'getAndSetVariant'. The first thing we do is try to get a cookie from the users browser. This will either be a cookie that has the value 'control' or 'experiment' if it exists and null if it doesn't. The next thing we do is make a call to our API endpoint. This returns us our user count in redis. The next thing we're doing may look odd. We've got a constant here specifying how many users we have. This is just a random number for demo purposes but you could work this out by looking at your website's analytics to get a rough mean value on your monthly users. We're going to be running an experiment with 50% of our user base so let's divide 100 by 2 to get 50%. Now if we don't have the ab test cookie and the count in redis is less than fifty percent of users, we will: first set the cookie with the value of experiment, make an api call to increment the count in redis and finally set the variant to experiment. And finally we just return the variant. So to put a long story short, this way redis will fill up with 50 users (half of our users) who are then opted into the experiment. We can use this logic elsewhere in our app to do a/b testing with -->

