---
description: >-
  This article will help you fix your locators to follow W3C guidelines and
  avoid errors in the executions
---

# Fix Invalid Argument invalid locator error on Agent 3.4.0+ (Appium 2.0)

If you are experiencing the following error after updating the Agent to version 3.4.0 on your mobile executions follow this article to quickly fix your locators.

```log
TimeoutException: Timeout occurred while trying to perform the action. invalid argument: invalid locator
```

Since Appium 2.0 has started following W3C guidelines, the following locators on mobile need to change (ID, Class name, Name) to meet the requirements:

This is how you can fix them:

* ID --> is now a CSS selector, add '**#**' before value.
* Class name-> is now a CSS selector, add '**.**' before value.
* Name --> is now a CSS selector, no change is required (_note)_.

Other related errors you might encounter:

**1.**

```log
TimeoutException: Timeout occurred while trying to perform the action. invalid argument: invalid locator
```

![](https://downloads.intercomcdn.com/i/o/422119802/1153e7fa2fac16d88ac2b68a/image.png)

**2.**

```log
Action failed using following locators:
ID=textElementTimeoutException: Timeout occurred while trying to perform the action. invalid argument: invalid locator(Session info: chrome=91.0.4472.114)Build info: version: '3.141.59', revision: 'e82be7d358', time: '2018-11-14T08:17:03'System info: host: 'DESKTOP-SGJR97F', ip: '172.22.144.1', os.name: 'Windows 10', os.arch: 'amd64', os.version: '10.0', java.version: '13.0.1'Driver info: io.appium.java_client.AppiumDriver
```

![](https://downloads.intercomcdn.com/i/o/422119988/353af66c49d19c8ea6ff8835/image.png)

If you experience any issues feel free to contact us here:

Mail:

[support@testproject.io](mailto:support@testproject.io)

Forum:

[https://forum.testproject.io/](https://forum.testproject.io)
