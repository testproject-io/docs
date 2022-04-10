# How to create a locator



1. First, try to edit the element like in the image below,

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/491252338/33b946c5fa11952f11de07ad/875bd74c0bcefb227e37f36d7954d9a112e766d5.png)

To check your locators use the magnifying glass\
﻿(notice the element must be present on the page when checking a locator):

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/491252358/8ccfbc23ea4fbabb562b1326/c90abeffa1079bd7ce0a645dbbbe61c4ffd141f8.png)

If another locator is more consistent make it your primary locator, push it to the top with the arrows next to the magnifying glass.

1. Check for a unique attribute and search the button by that locator,

you can make your custom locator like this for example:\
﻿**using Xpath** `//*[@attribute="value"]`

For instance, my locator for Amazon looks like this:\
﻿**using Xpath** `//*[@id="add-to-cart-button"]`

However, you can use TestProject built-in locator generator like this:

by pressing double shift on any element you can freeze it and then extract multiple XPath

![](https://downloads.intercomcdn.com/i/o/345808887/31cae38fc016512f4ecf8347/image.png)
