# How to create dynamic elements in TestProject

What is a dynamic element?\
\
A dynamic element is an element that its value can be changed dynamically, during run time. For example, let's say we have an unordered-list (ul) element with 100 list items (li). And let's also assume that all the li items are identical beside their text.\
So, to avoid creating 100 different elements, you can easily create a single element, using XPath, and add a parameter to its value for changing the li's text.

#### How to create a dynamic element in TestProject <a href="#how-to-create-a-dynamic-element-in-testproject" id="how-to-create-a-dynamic-element-in-testproject"></a>

Click on the "+" icon to add a new step and then, select the action you want to perform (an action that uses some element).

Then, click on "Create Element":

![](https://downloads.intercomcdn.com/i/o/436994001/0433676c657649108aa095b7/image.png)

To create a new element, fill the below details:

* Name
* Description (optional)
* Select the element's type (input, div, span, etc.)
* Locator strategy (ID, Name, XPath, etc.)
* Provide the locator's value

Between the single quotes in the below screenshot, we are going to add a parameter instead of a static text. To do so, we need to click on the "Use Parameter" icon in the below screenshot:

![](https://downloads.intercomcdn.com/i/o/436997872/40820e3ac3c646113d18c93a/image.png)

To add a parameter to the locator value, we have to create one. Click on the "+" icon to create a new parameter:

![](https://downloads.intercomcdn.com/i/o/436999929/b0d94a2909f3a5a5e3c6bc22/image.png)

To create a new parameter, fill out the below details:

* Name
* Description (optional)
* Value

Then, click on the "**Save**" button to complete the element creation:

![](https://downloads.intercomcdn.com/i/o/437001685/859dfcf248ba8a69fbc2b67f/image.png)

Then, select the parameter you just created by clicking on it:

![](https://downloads.intercomcdn.com/i/o/437002714/a685bec2c1a87cbd072925d8/image.png)

You can see now that the newly created parameter is used in the XPath value. This will make our element a dynamic one!

That's it! To complete the element creation, simply click on the "Save Element" button.

![](https://downloads.intercomcdn.com/i/o/437003453/864d9c645054a698509f962e/image.png)

In this article, we learned how to create a dynamic element that uses a parameter to change its value before/during the test execution. You can of course apply it to other locator types such as: ID, Name, Label, etc.

Happy testing! :)
