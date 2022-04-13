---
description: Best tips and tricks to stabilize your tests and jobs
---

# Automation Flakiness - quick fixes

### **How can I detect and fix Automation Flakiness?** <a href="#h_cbc97b255f" id="h_cbc97b255f"></a>

If you run your job or test multiple times and it tends to run successfully most of the time but sometimes fails without any particular reason (you haven't changed anything on your application and you don't have a bug), you might be suffering from automation flakiness.

Automation Flakiness is a known phenomenon in the test automation world, and it can be caused by multiple factors, some of them are: various loading time, elements that changing their location/shape, different execution targets, steps that didn't perform their destiny, or just lack of knowledge in how to build test automation correctly.

In TestProject we investing a lot of time and effort to give you the tools to reduce automation flakiness to a minimum and help even inexperienced test automation engineers to create rock-solid tests.

There are three different AI-based services that are running inside of the TestProject desktop agent, the primary goal is to detect automation failures that are origin in automation flakiness and fix them.

The **Adaptive wait** - balance the loading time

The **Automation assistant -** fix steps that didn't perform their original purpose

The **Self-Healing** - fix element locators changes

This quick-fix guide will help you to utilize these AI-based tools to reduce your flakiness and even get rid of it altogether.

#### **1) Switch the Adaptive wait and execution speed to Patient/Slow** respectively <a href="#h_81991e9941" id="h_81991e9941"></a>

Q: Why switching Adaptive wait to "Patient"?

A: Sometimes different loading times of elements or pages can affect our test

especially in heavy applications, no worries "Patient" Adaptive Wait **doesn't affect** the test speed if the application is loading as expected, it will just be more graceful if something takes more time then expected (for an element to be in the right state or for the page to fully load, etc).

Q: Switch execution speed to "Slow"?

A: simply because some of the web applications (especially these who were created in old technologies) weren't built for very fast execution, they can handle standard human interaction ("Slow" in machines world) however very fast clicks and types will break them very easily, some clicks can even be missed by the browser/app

How can we change that?

From the Test settings Tab like in the image below:

![](<../../.gitbook/assets/image (562).png>)

**Please make sure that the Automation Assistant is enabled.**

#### **2) Dividing long Tests and Jobs into smaller segments** <a href="#h_25e50f28f8" id="h_25e50f28f8"></a>

Q: Why should we divide long test cases?

A: Dividing the test will give us more control in our flow and also will decrease the chances of flakiness as actions like **restarting the browser** and **refreshing the session** which will remove cash collected during execution are happening more frequently.

It will also help the browsers to consume fewer resources such as less: memory, CPU, network. so we get a more stable flow overall.

Q: Why should we divide big jobs with a lot of test cases?

A: Dividing the job will allow us more control with finding the issue, as well as the additional benefit of a test case not failing an entire flow but a small part of that job.

How can we do it?

We can simply duplicate our tests and jobs and remove as many steps or tests from them as required until we reach the wanted length.

#### 3) Different environment variables - Desired Capabilities <a href="#h_1a44f993e4" id="h_1a44f993e4"></a>

Q: How do different environment variables affect me?

A: Sometimes different browsers and applications can be affected by resolution or languages, for example.

for instance, running chrome in headless will open it by default on 800X600 resolution, which in most cases won't be the resolution that you recorded your test, this might affect the application layout and thus cause our locators to be invalid. XPath is especially sensitive to such changes.

To overcome these issues we can set Desired Capabilities in our Jobs to set a more consistent environment.

How do set it up?

Follow these steps:

![](<../../.gitbook/assets/image (474).png>)

Here are some capabilities you can use for example:

```json
{
  "goog:chromeOptions": {
    "args": [
      "--ignore-certificate-errors",
      "--start-maximized",
      "--disable-notifications",
      "--disable-popup-blocking",
      "--disable-infobars",
      "--lang=en",
      "--window-size=1920,1080"
    ]
  }
}
```

#### &#x20;4) Make sure the environment is isolated as possible <a href="#h_57670b645f" id="h_57670b645f"></a>

make sure that outside sources aren't affecting your flow, things like:

a)

Drastic changes in the internet connection speed - can cause both your application and the agent to miss actions

b)

Make sure the operating system is not updating or running other operations in the background that can cause a conflict with the TestProject agent.

c)

**Don't use the machine** while the agent is executing tests.

#### 5) Specific steps or a specific type of steps are failing your flow <a href="#h_a8716aba59" id="h_a8716aba59"></a>

If a certain step or a certain event is consistently failing your flow please try the following:

a)

Create a more dynamic strategy to find the element.

You can either do it for the specific step manually by creating a more unique XPath for instance, or you can do it for the application level,

This is how you change the strategies for Elements Locators in your application:

![](<../../.gitbook/assets/image (515).png>)

![](<../../.gitbook/assets/image (542) (1).png>)

You can add custom locator strategies for your Application or you cancel certain strategies, You can also choose a different priority to the locator's strategy.

b)

Try to change the type of the step, for example:

normal click -> click using javascript.

scroll to element -> scroll to XPath.

#### 6) Don't record/use fixed scrolls and fixed swipes steps <a href="#h_85b0bb423e" id="h_85b0bb423e"></a>

In TestProject we allow to record steps such as scrolls up/down with your mouse on the web application and swipes up/down/right/left on mobile applications.

However, it will result in a fixed amount of distance in our scrolls/swipes, this distance can change between devices which can result in flakiness.

The best practice to scroll or swipe to an element is by using built-in actions like:

**WEB**

[https://addons.testproject.io/js-actions/scroll-to-element-with-javascript](https://addons.testproject.io/js-actions/scroll-to-element-with-javascript)

[https://addons.testproject.io/scroll-to-element](https://addons.testproject.io/scroll-to-element)

**Mobile**

[https://addons.testproject.io/swipe-and-find-element](https://addons.testproject.io/swipe-and-find-element)

Q: Why it's better to use built-in action for scroll/swipe vs recording steps by mimicking these operations manually?

A: fixed scrolls/swipes are bounded to a resolution of the app as it was during the recording (in pixels) if the resolution of the application is changing by different screen sizes or different mobile devices your test might run flaky.

A: some time elements that you are looking at might change their appearance, in some cases appearing after XX amount of swipes/scrolls and on a second run after YY amount of swipes/scrolls. While using the built-in actions will adjust the needed amount of swipes/scrolls automatically until it will find the element the recorded swipes/scrolls will do a fixed number of actions.

\
