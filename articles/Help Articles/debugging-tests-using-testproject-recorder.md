# Debugging Tests using TestProject Recorder

Creating a Test using TestProject Recorder is extremely easy, however, from time to time we might encounter an issue that we need to debug, in this article we are going to cover basic debugging strategies and tips to speed up your work in the Recorder.

### Use the recorder effectively <a href="#h_8cdf47de70" id="h_8cdf47de70"></a>

#### Running specific steps <a href="#h_9c5733a65e" id="h_9c5733a65e"></a>

To debug our tests efficiently sometimes we will need to execute a test to the point the test failed. this is how we can do it in the recorder:

1\) Run from/until here:

We can execute all the steps until 5, or all steps from 5 to the end by clicking on the step context menu:

2\) Select specific steps:

We can execute all the steps selected by hovering on the left side of any step and selecting it.

![](https://downloads.intercomcdn.com/i/o/402949636/ffd6a2c07ac9cda931cc7996/image.png)

we can also hold "SHIFT" to multiple select all the steps from 1 point to another

![](https://downloads.intercomcdn.com/i/o/402951745/77c7451a222a8d92727a5b6c/ynPDkCYMRQ.gif)

#### Make sure you are locators are working <a href="#h_351fd3b91a" id="h_351fd3b91a"></a>

TestProject automatically creates elements with working locators at the time of record.

Sometimes elements are changing from recording to execution, this is how you can check your locators and create new ones if needed:

1\) Use the magnifying glass -

Go into the step and use the magnifying glass to locate the Element on the page

![](https://downloads.intercomcdn.com/i/o/402964907/f2807a2ea1eb3e35eb575174/image.png)

If the element is not detected, go into Edit Element using the pencil sign:

![](https://downloads.intercomcdn.com/i/o/402965590/4b925bfa6cf811e28776700e/image.png)

and now check the other locators:

![](https://downloads.intercomcdn.com/i/o/402966190/cd8fa8be4e5a70dd54e12524/image.png)

To change the priority of the locator use the arrow and move the wanted locator to the top. if there is an unnecessary locator use the X and remove it.

If you are want to change the way TestProject record new elements [**click here**](https://intercom.help/testprojectio/en/articles/5306136-automation-flakiness-quick-fixes#h\_a8716aba59).

#### Use Step execution details to debug your tests <a href="#h_713ca71af9" id="h_713ca71af9"></a>

You can find more information about Step execution details [**here**](https://intercom.help/testprojectio/en/articles/5646653-step-details-and-information).

This window helps to understand which activities lead to the step failing, and it's very important for debugging your tests.

#### Using Switch to window correctly <a href="#h_cb5b2041fd" id="h_cb5b2041fd"></a>

The Recorder automatically creates "switch to window" steps for you, however, it's important to know how to create and manage them. as sometimes you will need to add them manually. For moving between tabs please use a specific index if you want to verify you are on the correct window you can check the URL or use any other method but if you are running the same flow switching to a specific window should be the same.

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/402960317/b058f03861e5100874d49c34/3a07a44ff8819e03bb8d97e3f84d60153406d0b3.jpeg)

_Note that the index starts at 0 (first tab)_

#### Use dynamic Scrolls / Swipes <a href="#h_9b3bbfaca8" id="h_9b3bbfaca8"></a>

When you swipe or scroll down in your application the recorder by default creates a fixed scroll for you, however when running the test on a different browser/resolution the test might behave differently. this is why you should always implement dynamic scrolls/swipes when possible, follow [this article](https://intercom.help/testprojectio/en/articles/5306136-automation-flakiness-quick-fixes#h\_85b0bb423e) to learn more.

### General fixes <a href="#h_cb93d64688" id="h_cb93d64688"></a>

#### Fixing Automation Flakiness issues <a href="#h_5862d0c804" id="h_5862d0c804"></a>

TestProject has a lot of AI tools built into it to stabilize your test, but it's important to know how to use them. You can enable/disable AI tools from the Test Setting or even increase effectiveness. Please follow [**this article**](https://intercom.help/testprojectio/en/articles/5306136-automation-flakiness-quick-fixes) if you running into stability or flakiness issues.
