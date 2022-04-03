---
description: A complete practical guide for creating a dynamic loop
---

# Dynamic loop

When automating an application, sometimes you will need to loop through an undefined number of elements and perform actions with them. For example:

* Getting all elements text and saving the data into a CSV file.
* Check if each one of the elements contains a specific text.
* Sum all elements values.

In all these cases, we can create a loop using the same logic that will be explained in this article.

You can take a look at the following example and adapt it to your test case.

In this example, I will create a loop that gets all the “Price” values, and I’ll sum them:

* The first step will be finding a locator that matches all the elements that will be used in the loop. To achieve this, we can create a locator using the Locator tab and the element inspector and verify the locator using the 'evaluate' button.

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/435511778/319907e2508eff35cb0ec4e7/7bb093a72f4e55c060f6ec5488d2d80697e044eb\_2\_690x332.png)

* Then, we will need to manually add a step that counts the number of elements and store the value into a _**PROJECT** PARAMETER_ (that has a default value equals 35 - or any numeric value that will allow us to start the loop):

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/435511784/ff73376842b5d882b8aea6d9/50f878a893b6f1cb9cf9c383778b6aa5f36221ce\_2\_284x500.png)

*   The next step will be getting the value of the element and storing it into a parameter using a **** [**dynamic locator**](https://intercom.help/testprojectio/en/articles/3572418-how-to-create-dynamic-elements-in-testproject).

    NOTE: The element locator must depend on the parameter we have created in the first step.

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/435511787/f0a54e0dc0e53274e1f6a31a/259917392c8166295ae653f4e9b42c323e0b7305\_2\_225x500.png)

* Then, as we want to sum all values, we’ll create a new parameter called “Total\_value” with default value “0”, and we will add a step that calculates the sum using the "mathematical expression" action:

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/435511797/823faf86bca29413f56f00e2/cf5ea68df6a1b06fda1ffe87643016b2eb35140f\_2\_281x500.png)

* Now, let's **reduce '**1**'** from the parameter “Number\_of\_elements\_total” :

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/435511804/431c96e6b1ca60a2817a63e0/4c76a28060e28d546e4c490d628cd7a34d7e0900\_2\_282x500.png)

* After adding all these steps, we are ready to create the loop.\
  To achieve that, first, we will need to group our steps into a test (except the one that counts the number of elements) and give it a name (let’s call our subtest “Get values and sum”).\
  _**NOTE: Once you group the steps, there is no “ungroup” option, so I suggest duplicating all steps and making sure it works before deleting the duplicated steps.**_

This is how you can group the steps into a subtest:\


![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/435511809/a4eabc0f43b59e7c7150db00/799696b700f72bfaf4a0bec7caa38226fe650ed6\_2\_334x500.png)

*   Now, let’s add a loop to this subtest with a condition. We can achieve that by opening the advanced options of this subtest:\




![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/435511815/d1b2a03bbb75743eaacc62e6/e9b48986167193686318ca33eca61e921c2036a1.png)

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/435511820/14e0d24b0f2de9eace6026ca/c4a2b84055597a9da13a90889c4e1b09224ba139\_2\_262x500.png)

That’s it; the test is ready to be executed. Simply adapt the loop to your needs.😃

Happy testing! :)

\
