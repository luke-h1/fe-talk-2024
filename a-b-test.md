
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

