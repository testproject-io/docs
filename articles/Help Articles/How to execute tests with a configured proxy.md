---
description: >-
  In this article we will utilize Job Custom Capabilities to configure a custom
  proxy while executing a Job.
---

# How to execute tests with a configured proxy

In case you want to execute your tests with a pre defined proxy, selenium offers arguments to pass to the driver which you can configure with them your custom proxy.

First, we will create a Job:

![](<../../.gitbook/assets/image (491).png>)

Now we shall Select Web, your desired browser, and the agent who shall execute the Tests.

![](<../../.gitbook/assets/image (552) (1).png>)

![](<../../.gitbook/assets/image (508).png>)

Next, after we create the Job, we will drag all the tests we wish to execute inside the Job:

![](<../../.gitbook/assets/image (507) (1).png>)

Now we will set the Custom Capabilities:

![](<../../.gitbook/assets/image (506) (1).png>)

We will add the following to the capabilities:

```json
"proxy": {
    "autodetect": false,
    "httpProxy": "HOSTNAME:PORT",
    "proxyType": "manual"
}
```

\


![](<../../.gitbook/assets/image (540).png>)

And that is it, once we run the Job, this capabilities will be set, and the tests will run with the configured proxy.
