---
description: >-
  if you're experiencing issues with running mobile tests on Xiaomi devices,
  please check out this article.
---

# Xiaomi Battery Settings

When automating tests on Xiaomi devices, the device's background power consumption setting may be interfering with our automation app.

You will need to disable this setting, by **disabling Xiaomi's UIAutomator battery usage control.**

You can do this by heading to your device's **settings**:

![](https://downloads.intercomcdn.com/i/o/222194163/37996aee22842b11ace77957/1.png)

Then **battery & performance**:

![](https://downloads.intercomcdn.com/i/o/222194213/715ac37f971432e6f9da707d/2.png)

Select _**Manage apps battery usage:**_

![](https://downloads.intercomcdn.com/i/o/222194350/74e5d1b5e09112b76b3ee631/3.png)

Select _**Choose apps**_ from _**Manage apps' battery usage**:_

![](https://downloads.intercomcdn.com/i/o/222194641/490ea5e5936a4b22e420d22c/4.png)

Select _**Installed apps** _ and choose **UIAutomator,** and then tap _**No restrictions:**_

\


![](https://downloads.intercomcdn.com/i/o/222195076/40fb31b8a0423a76ed941ab8/5.png)
