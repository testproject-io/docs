---
description: A complete practical guide for defining custom attributes to an application
---

# Setting Application's Custom Attributes

In many cases, you would like to set application custom attributes to facilitate the operation of automation tools.

While recording tests, elements are created automatically using default locator strategies (e.g. id, name, text, xPath etc.) By performing this action, **in case these attributes exist in the elements**, it will make the recorder build locators using these attributes as the first priority, in addition to the default ones.

you can find this feature in your project, under the 'Applications' tab:

![](https://downloads.intercomcdn.com/i/o/246218395/5450e12f450d1037bd6228f6/image.png)

Using this feature, all tests which use this specific application will use the default attributes to create its locators.

here is an example of setting up custom attributes on YouTube:

**- setting up custom attributes**

![](https://downloads.intercomcdn.com/i/o/253117469/fefe2a326a5ef8e423ef396d/image.png)

**- as you can see, the recorder has created an Xpath locator based on the class attribute as its first priority.**

\


![](https://downloads.intercomcdn.com/i/o/253124597/5acf82a32788bd5749e94e0f/image.png)
