---
description: >-
  This addon provides utility methods for extracting the RGB value that
  represent the color of an image/element. This done by utilizing visual testing
  capabilities.
---

# Get Element Color

## Description 

With this addon, you will be able to extract the RGB value that represent the dominate color of an element/screenshot in Web as well as **Android and IOS**, and if required, to compare with an expected result.

## Web and Mobile

Using the Web Recorder, all the is required is to hover over the element, press double shift, then search for **Get Color From Element** action:

![](../../.gitbook/assets/image%20%28287%29.png)

You can also input the expected result:



![](../../.gitbook/assets/image%20%28283%29.png)

The Action will pass if both RGB values are equal, and will fail either wise.

The output will always have the dominant color.

![](../../.gitbook/assets/image%20%28282%29.png)

This is the same in Mobile\(IOS and Android\), all that is required is to hover over the element, and search the **Get Color From Element** action:

![](../../.gitbook/assets/image%20%28285%29.png)



## Generic

There is also a generic option, which is not bound to a platform and element.

It is exactly the same, just this time it requires a path to the screenshot to evaluate the color.

![](../../.gitbook/assets/image%20%28284%29.png)

The evaluation and result are the same as the element actions, the difference is the source of the image and the type is **Action**.



