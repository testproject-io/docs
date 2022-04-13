# How to create a locator



1. First, try to edit the element like in the image below,

![](<../../.gitbook/assets/image (560).png>)

To check your locators use the magnifying glass\
﻿(notice the element must be present on the page when checking a locator):

![](<../../.gitbook/assets/image (492).png>)



If another locator is more consistent make it your primary locator, push it to the top with the arrows next to the magnifying glass.

1. Check for a unique attribute and search the button by that locator,

you can make your custom locator like this for example:\
﻿**using Xpath** `//*[@attribute="value"]`

For instance, my locator for Amazon looks like this:\
﻿**using Xpath** `//*[@id="add-to-cart-button"]`

However, you can use TestProject built-in locator generator like this:

by pressing double shift on any element you can freeze it and then extract multiple XPath

![](<../../.gitbook/assets/image (470).png>)
