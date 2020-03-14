# Swipe and Find Element addon

The Swipe and Find Element addon contains actions for finding an element by swiping vertically or horizontally until the element appears in the view. You can control the direction of the swipe, speed, the area of the swipe gesture and the number of swipes. You can use this addon when you need to interact with elements that are currently not on the page and you need to swipe to get to them. The actions will search if the element already exists in the page before the swipe action occurs. It will only swipe if the element is not present.

### Available Actions

* Swipe to element horizontally
* Swipe to element vertically
* Swipe to element by text horizontally

All of these actions are available for both Andriod and iOS tests

### Inputs

In order to swipe to and element you will need to specify the element that you want to swipe to. If you are using the **Swipe to element by text** action you can specify this using just one input field:

* Text - In this field you can specify the text of the element you want to swipe to

In the case of the other **Swipe to element horizontally** action you need to specify the element using two of the input fields:

* Locator - In this field you will specify the locator strategy that you want to use. Valid inputs for this field are: ID, NAME, CLASSNAME, CSSSELECTOR, LINKTEXT, TAGNAME, XPATH, PARTIALLINKTEXT, ACCESSIBILITYID, ANDROIDUIAUTOMATOR
* LocatorValue - In this field you will specify the value of the locator type that you are looking for

Once you have identified the element that you want to find, you can specify the properties of the swipe that you want to perform. For vertical swipes you will need to specify the following options:

* SwipeDirection - This field specifies which way to swipe. Valid inputs are: UP, DOWN
* BottomMarginPercent - This field specifies the margin from the bottom of the screen as a percent
* TopMarginPercent - This field specifies the margin from the top of the screen as a percent
* MaxSwipes - This fields takes in a number specifying the maximum number of swipes that you want to perform
* TimeoutMilliseconds - This field specifies the amount of time to wait before considering the test step to have timed out. This overrides the test default timeout value

For Horizontal Swipes you will need to specify the following options:

* SwipeDirection - This field specifies which way to swipe. Valid inputs are: Right, Left
* RightMarginPercent - This field specifies the margin from the right side of the element as a percent
* LeftMarginPercent - This field specifies the margin from the left side of the element as a percent
* MaxSwipes - This fields takes in a number specifying the maximum number of swipes that you want to perform
* TimeoutMilliseconds - This field specifies the amount of time to wait before considering the test step to have timed out. This overrides the test default timeout value

