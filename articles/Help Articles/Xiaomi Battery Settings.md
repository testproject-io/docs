---
description: >-
  if you're experiencing issues with running mobile tests on Xiaomi devices,
  please check out this article.
---

# Xiaomi Battery Settings

When automating tests on Xiaomi devices, the device's background power consumption setting may be interfering with our automation app.

You will need to disable this setting, by **disabling Xiaomi's UIAutomator battery usage control.**

You can do this by heading to your device's **settings**:

![](<../../.gitbook/assets/image (541) (1).png>)

Then **battery & performance**:

![](<../../.gitbook/assets/image (453) (1).png>)

Select _**Manage apps battery usage:**_

![](<../../.gitbook/assets/image (560) (1).png>)

Select _**Choose apps**_ from _**Manage apps' battery usage**:_

![](<../../.gitbook/assets/image (457) (1).png>)

__

Select _**Installed apps** _ and choose **UIAutomator,** and then tap _**No restrictions:**_

![](<../../.gitbook/assets/image (475) (1).png>)

\
