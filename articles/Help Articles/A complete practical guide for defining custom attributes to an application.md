---
description: A complete practical guide for defining custom attributes to an application
---

# Setting Application's Custom Attributes

In many cases, you would like to set application custom attributes to facilitate the operation of automation tools.

While recording tests, elements are created automatically using default locator strategies (e.g. id, name, text, XPath etc.) By performing this action, **in case these attributes exist in the elements**, it will make the recorder build locators using these attributes as the first priority, in addition to the default ones.

you can find this feature in your project, under the 'Applications' tab:

![](<../../.gitbook/assets/image (540) (1).png>)

Using this feature, all tests which use this specific application will use the default attributes to create its locators.

here is an example of setting up custom attributes on YouTube:

**- setting up custom attributes**

![](<../../.gitbook/assets/image (562) (1).png>)

**- as you can see, the recorder has created an Xpath locator based on the class attribute as its first priority.**

![](<../../.gitbook/assets/image (538).png>)
