# How to check the checkbox's state

For checking a checkbox’s state and clicking on it only if it’s unchecked, you can create the following steps:

* Hover the checkbox element, press double-shift on your keyboard to capture it, and use the “Get Attribute Value” action.

![](<../../.gitbook/assets/image (489) (1).png>)

* Set the AttributeName input field to “checked” which will indicate if the checkbox is checked or not. save the output value into a parameter (is\_chceked) for further use.

_(Notice: if the checkbox is checked, the “checked” attribute value will be “true” otherwise, the value will be an empty string)_

![](<../../.gitbook/assets/image (555).png>)

* Create a new step, that performs a “Click” action on that checkbox, add a condition to this step, the condition will validate the “is\_checked” parameter value and will execute the “Click” step only if the “is\_checked” parameter value is not empty.

1. Click on the “Advanced Options”

![](<../../.gitbook/assets/image (566).png>)

1. Scroll down to the “Conditions” section, set the parameter to “is\_checked”, the condition to “Equals”, and leave the last field empty, so the condition will check whether the value is empty or not.

![](<../../.gitbook/assets/image (537) (1).png>)

This way, the “Click” step will be executed only if the condition is met, otherwise, it will be skipped.\
﻿Using these two test steps, you can click on a checkbox only if it’s unchecked.
