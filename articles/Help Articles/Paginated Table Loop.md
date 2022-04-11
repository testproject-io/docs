---
description: A complete practical guide for creating a dynamic loop on Paginated Tables
---

# Paginated Table Loop

When automating an application, sometimes you will need to loop through a **paginated table** and perform actions on its elements.

There are different possible scenarios where you might want to test a paginated table.

In this article, we will elaborate on 3 test cases and bring examples of how to achieve each of them.

### **1) Specific Row** <a href="#h_215c48c642" id="h_215c48c642"></a>

The first test case that we will elaborate on is a scenario in which we want to perform actions on a specific row of the table.

For example:

* Find a specific text and store its value.
* Find a specific row and check its values.
* Find a specific row and verify one of its columns value.

In all these cases, the big challenge presented by a paginated table is the fact that the desired row may not be present on the current page - and we don't know which page to find it on.

You can take a look at the following example and adapt it to your test case.

In this example, I will create a loop to find a specific name and store the text into a parameter:

*   The first step will be finding a unique locator that matches only the desired element. To achieve this, we can create a locator using the Locator tab and the element inspector and verify the locator using the 'evaluate' button.

    (In this example, I build my unique locator using the element text. You can read more about locating techniques [_**here**_](https://intercom.help/testprojectio/en/articles/4206256-mastering-element-locating-techniques-and-relative-xpath-writing-skill)).
* Then, using the unique locator, I will add a step with the action "**Get text(if visible)**" and **store the value into a **_**project parameter**_(let's call it "Name\_text").

![](<../../.gitbook/assets/image (1) (2).png>)

* After that, I will add a step that clicks on the "Next" button if it is visible(using the action "Click if visible")

![](<../../.gitbook/assets/image (2) (2).png>)

* After adding these steps, we are ready to create the loop.\
  To achieve that, first, we will need to group our steps into a test and give it a name (let’s call our subtest “Paginated Table Loop”).\
  _**NOTE: Once you group the steps, there is no “ungroup” option, so I suggest duplicating all steps and making sure it works before deleting the duplicated steps.**_

This is how you can group the steps into a subtest:

![](<../../.gitbook/assets/image (3) (1).png>)

* Now, let’s add a loop to this subtest with a condition. We can achieve that by opening the advanced options of this subtest:

![](<../../.gitbook/assets/image (4) (1).png>)

* We will add a loop that repeats the subtest the maximum times we might need it to perform the "Click" action to find the element. At the same time, we will add a condition that stops repeating the subtest if the element is found. This is how you can achieve it:

![](<../../.gitbook/assets/image (5) (1).png>)

That’s it; the test is ready to be executed. Simply adapt the loop to your needs - you can perform actions in any column of this row once you find the element.

### **2) Specific Column** <a href="#h_26fe16bc2a" id="h_26fe16bc2a"></a>

The second test case that we will elaborate on is a scenario in which we want to perform actions on specific column(s) of the table.

For example:

* Getting all emails and saving the data into a CSV file.
* Check if each one of the elements contains a specific text.
* Calculate the average age.

In all these cases, we have already covered how to achieve them in our article on "[_**dynamic loops**_](https://intercom.help/testprojectio/en/articles/5819795-dynamic-loop)".

The only difference is that, in the case of paginated tables, in addition to the dynamic loop that performs the desired actions on each page, we also have to add a dynamic loop that goes from one page to the next.

To achieve that, we will face each page of the table separately.

* The first step will be going to the first page of the table and **creating only there** the dynamic loop you want to perform using the mentioned [_**guide**_](https://intercom.help/testprojectio/en/articles/5819795-dynamic-loop).

Once the test is created(for the first page of the table) - we only need to add a loop to perform the same test over each page.

* To achieve that, we have to **group as a step** all the steps of the dynamic loop created.
* After that, I will add a step that clicks on the "Next" button if it is visible(using the action "Click if visible") :

![](<../../.gitbook/assets/image (6) (1).png>)

* Then, we have to **group as a step** again the subtest and the "click if visible" action.
* Finally, we will open the new subtest, open the "advanced options" and add to the "REPEAT" field the number of pages our table has(or more).

That’s it; the test is ready to be executed. Simply adapt the loop to your needs.😃

### **3) Checking if the pagination is presented correctly** <a href="#h_94360d1b8e" id="h_94360d1b8e"></a>

Another test case that may be relevant is to check if the division of the table into pages is being presented correctly.

For example:

Let's say we want to check if the first ID of each of the ten first pages is actually in its correct position.

For this demo pagination table:\
﻿[https://codepen.io/yasser-mas/pen/pyWPJd](https://codepen.io/yasser-mas/pen/pyWPJd)

Have a look at this shared test:

[https://app.testproject.io/#/shared-tests/with-me?s\_token=8KMVcoyh\_0yzsjE4dJ2\_Bg](https://app.testproject.io/#/shared-tests/with-me?s\_token=8KMVcoyh\_0yzsjE4dJ2\_Bg)

Step two calls a nested test withten0 iterations (10 pages):

![](<../../.gitbook/assets/Screen Shot 2021-07-21 at 21.06.05.png>)

And this is the inner test:

![](<../../.gitbook/assets/Screen Shot 2021-07-21 at 21.06.26.png>)

That’s it; the test is ready to be executed. Simply adapt the loop to your needs.😃
