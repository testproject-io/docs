# How to create dynamic elements in TestProject

What is a dynamic element?\
\
A dynamic element is an element that its value can be changed dynamically, during run time. For example, let's say we have an unordered-list (ul) element with 100 list items (li). And let's also assume that all the li items are identical beside their text.\
So, to avoid creating 100 different elements, you can easily create a single element, using XPath, and add a parameter to its value for changing the li's text.

#### How to create a dynamic element in TestProject <a href="#how-to-create-a-dynamic-element-in-testproject" id="how-to-create-a-dynamic-element-in-testproject"></a>

Click on the "+" icon to add a new step and then, select the action you want to perform (an action that uses some element).

Then, click on "Create Element":

![](<../../.gitbook/assets/image (465).png>)

To create a new element, fill the below details:

* Name
* Description (optional)
* Select the element's type (input, div, span, etc.)
* Locator strategy (ID, Name, XPath, etc.)
* Provide the locator's value

Between the single quotes in the below screenshot, we are going to add a parameter instead of a static text. To do so, we need to click on the "Use Parameter" icon in the below screenshot:

![](<../../.gitbook/assets/image (551).png>)

To add a parameter to the locator value, we have to create one. Click on the "+" icon to create a new parameter:

![](<../../.gitbook/assets/image (532).png>)

To create a new parameter, fill out the below details:

* Name
* Description (optional)
* Value

Then, click on the "**Save**" button to complete the element creation:

![](<../../.gitbook/assets/image (531).png>)

Then, select the parameter you just created by clicking on it:

![](<../../.gitbook/assets/image (467).png>)

You can see now that the newly created parameter is used in the XPath value. This will make our element a dynamic one!

That's it! To complete the element creation, simply click on the "Save Element" button.

![](<../../.gitbook/assets/image (507).png>)

In this article, we learned how to create a dynamic element that uses a parameter to change its value before/during the test execution. You can of course apply it to other locator types such as: ID, Name, Label, etc.

Happy testing! :)
