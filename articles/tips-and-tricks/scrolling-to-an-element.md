# Scrolling to an Element

Many modern web pages have content 'below the fold' and require you to scroll down to see more of the page. When writing test automation it can be a bit tricky to do this kind of scrolling if you are going to run the test on different computers. TestProject will automatically add scrolling to the test steps, but this scrolling is setup to be an absolute value. It will scroll the page up or down by a certain number of pixels. This is fine if the test is always run on the same size screen, but what happens if the test is created on a small laptop screen which requires quite a bit of scrolling and then run on a larger monitor which requires much less scrolling?  If the scroll value is set to an absolute number the test will attempt to scroll by the larger amount that the laptop screen required and could scroll right past the element you are interested in.

## Scroll to Element Addon

This is where the [scroll to element addon](../../testproject-addons/available-addons/scroll-to-element-addon.md) comes in handy. This addon provides us with actions that let us scroll directly to a specified element. As with any other addon, it can be [installed ](../../testproject-addons/installing-community-addons-from-the-store.md)with a simple click and it then provides a number of different ways to specify the element that you want to scroll to.&#x20;

Let's look at an example of how we might use it.

## Example Setup

For this example, we will use the TestProject landing page (testproject.io). If you have not yet used TestProject, check out the documentation on [creating your first test](../../using-the-smart-test-recorder/web-testing/creating-a-web-test-using-the-testproject-recorder.md) and setting up a project. Once you have created a project, start creating a test with [https://testproject.io/](https://testproject.io/) as the application url.  Open that test in the test recorder and it should take you to that page.

## Scrolling to a Given Element

For the purposes of this example, let's say we want to scroll to the Learn More button in the Shared Addons section of the page. This button is about 2/3 of the way down the page. In the test recorded scroll down until you see that button.  You will see that the test recorder has automatically added one or more test steps that say `Scroll window by` and then a value to indicate how much the window should scroll.

![Scroll window commands](<../../.gitbook/assets/image (29).png>)

Instead of using those commands, we want to use one of the `Scroll to element by` commands. In order to do that, click on the blue plus button to add a new test step. Change the type on the step creation panel from Element action to Action, and then in the action section click on the Select action link. Type `scroll` into the search field and it should give you back a list of different commands. From this list select the `Scroll to element by xpath` action. There are of course a number of other ways that you can choose for scrolling to an element, but for this example we will look at getting it by xpath

This action requires you to specify the xpath of the element you want and we can get it by hoovering over the Learn more button on the page and hitting the shift key twice in row in rapid succession (double shift). On the resulting menu, go to the `Attributes` option.  One of the attributes on there should be the xpath of the element. You can copy this by using the `copy to clipboard` icon.

![Copy xpath to clipboard](<../../.gitbook/assets/image (25).png>)

Paste this value into the xpath field for the `scroll to element by xpath` action and save the test step.&#x20;

## Cleaning up the Test

Now, we have created a test step that will scroll to the desired element, but before we consider this test complete we should do a little bit of cleanup. We have all those `Scroll window by` steps that we really don't need anymore, so let's remove them.  We can do this with the `Multiple Select` tool.

![Multiple Select Tool](<../../.gitbook/assets/image (76).png>)

After click on this, you can select the check boxes beside each of the `Scroll window by` test steps and then choose the trash can icon to delete them all in on go.&#x20;

![Delete Multiple Test Steps](<../../.gitbook/assets/image (137).png>)

And with that you have cleaned up and completed the test

## Conclusion

The scroll to element actions allows you to scroll to an element regardless of it's exact position on the page. These actions are easy to use and help to make your tests more robust and able to run on different size and resolution screens. Try it out for yourself and see how easy it is to use!
