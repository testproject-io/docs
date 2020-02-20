# How to Deal with Dynamic Elements

Some website use html generation frameworks. These frameworks will often create identifiers that change every time the page is loaded. These are known as dynamic element locators and can be quite tricky to deal with in UI test automation. If the identifiers for a particular element are different each time the page is loaded, how do you find the element that you want on the page? Well, let's talk about a few strategies you can use.

## XPath

If the actual element you want has a dynamic ID or other attributes, you can always us XPath to find that element in the Document Object Model \(DOM\) hierarchy. This method can work, but there are also significant downsides to it as well. There are more details on the benefits and risks of XPath in the documentation section on [_Best Practices for Element Locators_](best-practices-for-element-locators.md#xpath)_._

## Parameters

Sometimes you may be able to parameterize part of the search query you are looking for so that you can match what you looking for with what you have entered. For example, if an element locator is built based on some user input it would of course change depending on that input, but if you parameterize that input you can still find the element. That might all sound a bit confusing so let's take a look at an example of this.

## Dynamic Element Locator Example

This example will be based on the [_TestProject example page_](https://example.testproject.io/web/). If you have not used TestProject before you can see how to setup a project and test in the [_web testing_](../using-the-smart-test-recorder/web-testing/) __ section of the documentation. So with the TestProject recorder open on the example page let's take a look at how we can find dynamic elements.

### Login

First of all let's enter a full name. We can click on the full name box and type in the name we want to use. and the Recorder will automatically add steps for those actions. Now, we will want to use the full name that we just entered to help us find a locator later, so let's just parameterize it right now. If we click on the test step and go to the plus beside the text input field we can add a parameter. 

![Add a parameter](../.gitbook/assets/image%20%28182%29.png)

We can then click on the plus a the bottom of the parameters page to create a new parameter. Give it a name and a value that matches the name entered earlier and then click add to add the parameter. In the input text box, make sure that the new parameter is now being used and delete the previous text if it is still there. Once the parameter is correctly set, click on the check mark at the bottom of the page to apply the changes and then click on save to add them to the test step.

![Apply Parameter Changes](../.gitbook/assets/image%20%28146%29.png)

You can now click on the password field and type in `12345` and hit the login button to complete the login process. As you do these actions the Test Recorder will automatically add steps to the test for you. 

### Verify Full Name

At this point we are taken to the next page and there is a welcome message on this page that says `Hello {FullName}, let's complete the test form`. This element does have an ID that we can use, but let's imagine it does not and see if we can find it use a dynamic query.

First of all we will add a new test step.

![Add a New Test Step](../.gitbook/assets/image%20%2898%29.png)

Then in the Element section we will click on the Select an Element link and then click on the plus at the bottom of the panel to add a new element.

![Add New Element](../.gitbook/assets/image%20%28165%29.png)

Give the new element and name and set the locator to be `XPATH` and then beside the text box click on the plus button.

![Add Locator Parameter](../.gitbook/assets/image%20%2897%29.png)

In the resulting dialogue type the following  `//*[text()="`and then click on the parameter you made during the login steps to select it as the text to search for.  Then complete the string by putting in closing quotation marks and a square bracket. The final string should look like this `//*[text()="FullName"]` where `FullName` is the name of the parameter you created.  Then click Save to apply your changes. 

You will also need to select the element type, and in this case that is just `b`so set that in the element type dropdown.  You can then click on the find button to ensure that the element you created can be found on the page and then hit Add Element to add it to the list. Select this element you just added and then click on select action and search for value. 

Select `Get attribute value` from the search results. If you have not yet used addons you will need to install the `Web Extensions` addon for this. You can see how to install and use addons [_here_](../testproject-addons/using-addons-in-the-testproject-recorder.md) __in the documentation.

In the Attribute name field type in `text` and then in the AttributeValue section, click on select parameter and choose the FullName parameter you made above and then click on the Create button to create that test step.

## Conclusion. 

Dynamic locators can be a bit tricky to find and use, but thanks to the flexibility and power of TestProject, pages using this kinds of locators and be tested from within this tool. By using parameters or xPath and sometimes even by combining the two strategies together you can successfully find and interact with the elements you want.

