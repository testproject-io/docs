# Best Practices for Element Locators

Element locators are a key part of any test automation being done through the UI. They are used to find the different parts of the page and allow us to interact with a page programmatically. Elements, of course, are the many different piece that are used to make up a web page. The definition of the elements on the page tell the browser how to render the page and element locators are just ways to find a particular element on a page.

When writing test automation you will usually need to find and use many different elements. There are several different element locators that are available and there are pros and cons to using each one. In order to have test automation succeed in the long run you need to be able to effectively manage the elements you are using in your test. Test Project provides [great tools](element-mangement.md) for doing this which help with maintaining tests and keeping them up to date over time, but they aren't enough. Any UI automation work needs a good locator strategy to reduce the ongoing work that it takes to keep the tests up to date as the code changes, so let's take a look at some of the element locators and the pros and cons of using them.

##  Unique IDs

In general the best possible element locator is a unique ID identifier. If an element has a unique ID you should probably use that to find the element. There is one thing to be aware of here though. Some websites will use code generation frameworks to create the html elements. In this case it may assign a unique ID to an element, but that ID could change when you refresh the page and [the code is regenerated](how-to-deal-with-dynamic-elements.md). So when looking for unique IDs you need to find unique IDs that are also consistent or static. Usually this means the IDs will have been created explicitly by the developers. If an element does not have unique IDs, you may be able to ask the developers on the team to add them. 

In general you will have much more stable UI test automation if you are able to find the elements you want using unique ID identifiers so it is worth trying to get those added to the code if you can. However, sometimes this is not possible to do if you don't have access to the code or the developers working on it. In that case there are of course other ways to find the elements you want and each of these ways have some things to consider.

## XPath

XPath is a way to find elements based on where they are in the Document Object Model \(DOM\) hierarchy. This is a great way to get a unique identifier since the path to a particular element on a page is going to be unique, but there is one big challenge with this in terms of maintaining your tests going forward. Since the XPath locator for an element usually includes a lot of the element hierarchy on the page, any changes to the page hierarchy \(for example, due to changing the page layout\), will make that XPath invalid. 

One of the main advantages to using XPath locators is the fact that they are unique. This means that your tests won't accidentally select the wrong element when they are running. However, the downside to using them is that they can easily become invalid if the page is changing. A good rule of thumb when it comes to using XPath is that you should only use it if there are no other unique identifiers on an element. 

If you do decide to use an XPath locator, there are a couple of things to keep in mind. The first thing is to try and keep the length of the path as short as possible. You want to find the closest element in the hierarchy that has a unique identifier and build your XPath from there. The shorter the XPath, the less likely it is to break. The other thing to remember is that you want it to be start with an element that has a unique identifier. The whole point of using XPath locators at all is that they give you a unique path, but that advantage is lost if the starting point of the path is not unique.

Since the general rule of thumb is to not use XPath unless there are no unique identifiers let's talk about a few more ways to locate an element.

## Class

Often an element will have a class associated with it. If the class name is unique for that element this can work as a good locator. When doing this you want to use a unique locator and so if an element has a couple of classes on it, try to pick the one that will be most likely to be only used by that element. Sometimes a class might be only used by one element when creating the test, but later on other elements are added to the page that use that same class which can cause confusion when running the test. 

## Element Attributes

If an element does not have a unique ID or class, you can look for other attributes of the element that might be unique. These can include things like the element name, or for certain kinds of elements, the text  or link text, and any other attributes that an element might have. 

## CSS Selectors

CSS Selectors are usually used by a page to determine the kind of styling to use on an element. They aren't usually meant to be used as locators, but if there are no other unique identifiers, they can sometimes be a way to identify a particular element on a page. As with XPath, CSS selectors often include some degree of hierarchy in them and so they can have some of the brittleness associated with XPath selectors. They are also susceptible to change since styling on the page may change. Since they are not primarily intended to element locators they can sometimes be changed without consideration for tests that might be using them, so you do want to be careful in using them as element locators

## Element Locators in TestProject

TestProject makes it easy to use these best practices to find element locators. You can learn more about elements and how to use and mange them in TestProject by going to the documentation section on [finding and using elements](../using-the-smart-test-recorder/finding-and-using-elements/).

