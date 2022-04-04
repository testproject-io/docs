---
description: >-
  In this article we will utilize Job Custom Capabilities to configure a custom
  proxy while executing a Job.
---

# How to execute tests with a configured proxy

In case you want to execute your tests with a pre defined proxy, selenium offers arguments to pass to the driver which you can configure with them your custom proxy.

First, we will create a Job:

![](https://downloads.intercomcdn.com/i/o/295442379/de5854f43113eba9584c14cf/image.png)

Now we shall Select Web, your desired browser, and the agent who shall execute the Tests.

![](https://downloads.intercomcdn.com/i/o/295442767/0ab8354eb59f39bfa2877fa1/image.png)

![](https://downloads.intercomcdn.com/i/o/295442929/5f3455338c3adf5095413d9d/image.png)

Next, after we create the Job, we will drag all the tests we wish to execute inside the Job:

![](https://downloads.intercomcdn.com/i/o/295443300/1f52ca5d1cfb496628e5b623/image.png)

Now we will set the Custom Capabilities:

![](https://downloads.intercomcdn.com/i/o/295443500/f4d46ac8b72ae1fc006fc826/image.png)

We will add the following to the capabilities:

```
"proxy": {
    "autodetect": false,
    "httpProxy": "HOSTNAME:PORT",
    "proxyType": "manual"
}
```

\


![](https://downloads.intercomcdn.com/i/o/306887358/a6ced0fb519a0535fed3ca74/proxy.png)

And that is it, once we run the Job, this capabilities will be set, and the tests will run with the configured proxy.
