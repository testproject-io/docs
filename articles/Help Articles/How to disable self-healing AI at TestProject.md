---
description: In this article I will show you how to turn off Self-Healing for Mobile/Web.
---

# How to disable self-healing AI at TestProject

**About Self-healing AI-powered feature at TestProject.**

The self-healing helps stabilize tests by using multiple locator strategies on while locating elements. That means that if the element locator was changed or identified badly in the first place, fallback strategies will be used to execute the test.

**Possible reasons for disabling the self-healing feature**

* Defining "Strongly type" for element
* When we map the element manually
* When we want to limit the element with a single and specific locator strategy
* Auto generated elements with high similarity of attributes on elements

**Fully disabling the self healing on all steps for a specific element**

To completely disable the self-healing on a specific step in your tests, all you need is to follow these simple steps:

Open the advanced step settings for the step you wish to disable the self-healing.

![](<../../.gitbook/assets/image (523).png>)

Inside the step, press on edit element (pencil icon) and remove all alternative locators found by TestProject, leavening the desired locator only.

![](<../../.gitbook/assets/image (472).png>)

It will shut down the self healing feature and indicate to TestProject's self-healing AI engine that this specific step shouldn't be exacted with alternative strategies.

* **important note** , some of the self-healing capabilities will still be applied, such as adaptive wait and element prediction appearance, but these have a  very low chance to affect your automation negatively.
* Yet, if you want to disable the adaptive wait feature (not recommended), you can set the default time for adaptive to 0ms.

To disable the adaptive wait:

In your test, click on the three dots and click on settings:



Set the adaptive wait to 0:

![](https://downloads.intercomcdn.com/i/o/259446317/b0779b8b1e4433a567366586/image.png)
