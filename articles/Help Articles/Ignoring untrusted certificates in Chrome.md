---
description: >-
  In this article we will utilize Job Custom Capabilities to bypass untrusted
  certificates in while executing a Job on Chrome
---

# Ignoring untrusted certificates in Chrome

In case your tests are blocked by the warning of an untrusted certificate, selenium offers arguments to pass to the driver which can bypass it so the tests can continue executing.

First, we will create a Job:

![](<../../.gitbook/assets/image (514).png>)

Now we shall Select Web, Chrome as the Browser, and the agent who shall execute the Tests.

![](<../../.gitbook/assets/image (473).png>)

![](<../../.gitbook/assets/image (504).png>)

Next, after we create the Job, we will drag all the tests we wish to execute inside the Job:

![](<../../.gitbook/assets/image (511) (1).png>)

Now we will set the Custom Capabilities:

![](<../../.gitbook/assets/image (498).png>)

We will add the following to the capabilities:

```json
"goog:chromeOptions": {
    "args": ["--ignore-untrusted-certificate"]
  }

```

![](<../../.gitbook/assets/image (465) (1).png>)

And that is it, once we run the Job, these capabilities will be set, and the tests will run without the warnings.

\
