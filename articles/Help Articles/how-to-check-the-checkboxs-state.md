# How to check the checkbox's state

For checking a checkbox’s state and clicking on it only if it’s unchecked, you can create the following steps:

* Hover the checkbox element, press double-shift on your keyboard to capture it, and use the “Get Attribute Value” action.

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/491163995/5a03130caa6db409faeabfac/36a7e9a3e9324ea1f2b807f3c274cea3cc7915d6\_2\_690x221.png)

* Set the AttributeName input field to “checked” which will indicate if the checkbox is checked or not. save the output value into a parameter (is\_chceked) for further use.

_(Notice: if the checkbox is checked, the “checked” attribute value will be “true” otherwise, the value will be an empty string)_

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/491164007/5c205eceb1378787c258876c/d7bc93558c23b84eafd9b8a47ba58048cb93ea78.png)

* Create a new step, that performs a “Click” action on that checkbox, add a condition to this step, the condition will validate the “is\_checked” parameter value and will execute the “Click” step only if the “is\_checked” parameter value is not empty.

1. Click on the “Advanced Options”

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/491164020/df66a22002c493e628c79b47/07ed460ad3c9633fcd7892d85b2e51d7e79adc0d.png)

1. Scroll down to the “Conditions” section, set the parameter to “is\_checked”, the condition to “Equals”, and leave the last field empty, so the condition will check whether the value is empty or not.

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/491164031/1bc6b2fc76557916cec3b7f1/e39704a6ebfe1bcc54b253d9e9420e5dee873a5b.png)

This way, the “Click” step will be executed only if the condition is met, otherwise, it will be skipped.\
﻿Using these two test steps, you can click on a checkbox only if it’s unchecked.
