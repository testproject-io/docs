# How to Create Custom XPath with Text, Label, Class, etc.

In TestProject, you have the option to create custom XPath locator based on one or more properties. For example, an input element with class of: active, can be located using this XPath: //input\[@class = 'active'].

In lack of other unique locator such as: ID, Name, etc, you might need to use XPath. Since absolute XPath is considered unreliable, you can create a custom XPath that will keep your test robust, reliable and easy to maintain.

In this article, we are going to learn how to create an element using custom XPath.\


Let's try to locate the "Full Name" text box using its place holder value, which is: "Enter your full name".&#x20;

![](<../../.gitbook/assets/image (468).png>)

On the placeholder attribute, you have 3 buttons. The right one, will open the "Element locator" tool with the XPath value of the element based on the placeholder:

![](<../../.gitbook/assets/image (492).png>)

In the "Element Locator" pop-up window, we can see the generated XPath value we got. You can click on "Evaluate" to identify this element in the page and check if it's a unique identifier or not. By clicking on the "Save Element" button, you can easily create a new element that would be identified using the generated XPath value.

![](<../../.gitbook/assets/image (476).png>)

That's it! You now have a new element that you are locating using a smart XPath value :)
