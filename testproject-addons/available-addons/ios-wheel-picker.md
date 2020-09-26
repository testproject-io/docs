# iOS Wheel Picker

You can use the [iOS Wheel Picker](https://addons.testproject.io/ios-wheel-picker) Addon to automate iOS wheel picker elements.

![](../../.gitbook/assets/1%20%282%29.png)

The elements are of type **XCUIElementTypePickerWheel** and can be scrolled to select various options.

![](../../.gitbook/assets/2%20%282%29.png)

The Addon contains 4 actions:

1. Scroll Picker Wheel
2. Scroll Picker Wheel to Value
3. Scroll PickerWheel using Offset
4. Select Picker Wheel Option

Let's review all 4 actions.

## Scroll Picker Wheel

The Scroll Picker Wheel action will scroll the picker wheel a set amount of times either forward or backwards as indicated by the two input fields.

The **Order** field can receive either ‘**next’** or ‘**previous’** indicating the direction and **Scrolls** field will receive the number of scrolls to perform.

![](../../.gitbook/assets/3%20%283%29.png)

In the following example, the left picker wheel was scrolled from the starting value of 8, to 10:

![](../../.gitbook/assets/4%20%283%29.png)

## Scroll Picker Wheel to Value

This action will scroll the wheel either forward or backwards until the input text is contained in the current option selected by the wheel.

The first parameter again being the direction of the scroll and the second being the **Text** in the wheel option we are searching for.

![](../../.gitbook/assets/5%20%283%29.png)

The following example will scroll the right picker wheel backwards **until it contains** 25:

![](../../.gitbook/assets/6%20%283%29.png)

## Scroll Picker Wheel using Offset

This action will scroll the picker wheel either forward or backwards using **the** **ratio of the picker wheel height you want the click to happen.**

![](../../.gitbook/assets/7%20%283%29.png)

## **Select Picker Wheel Option**

This action only has one parameter, being **Option**. This parameter is **the option to select from the wheel.**

The wheel will be scrolled in any direction to find the option if possible.

![](../../.gitbook/assets/8%20%282%29.png)

The following example will select 20 in the left picker wheel immediately, even if it is not currently visible:

![](../../.gitbook/assets/9%20%282%29.png)

