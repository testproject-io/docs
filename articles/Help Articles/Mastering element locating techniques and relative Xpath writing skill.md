---
description: A complete practical guide for writing correct Xpath in any situation
---

# Mastering element locating techniques and relative Xpath writing skill

### **Disclaimer** <a href="#disclaimer" id="disclaimer"></a>

In this practical guide we will not go thru the very beginning or explaining what is Xpath. This is fully practical tutorial to increase your effectiveness and speed in writing Xpath in difficult cases and for dynamically generated locators on your page.

**Disassembling the element**

Just picking some subject element to have a closer look at the parts it's built from.

I will use __ [_https://material.angular.io/_](https://material.angular.io) __ page as i think it's pretty good for the examples of difficult to find elements.

We will need Chrome Developer Tools (or similar in another browser, but i will use this one)

![](../../.gitbook/assets/2020-06-29\_12h02\_11.gif)

We need to hit an element inspection tool and then click on element we want to inspect (to see this element in HTML page with all it's properties and where it's located in the page)

![](../../.gitbook/assets/2020-06-29\_12h17\_20.gif)

Now let's have a closer look to element we selected.

![](<../../.gitbook/assets/image (538).png>)

Here's the copy of this element in html format

```html
<a _ngcontent-ity-c49="" mat-button="" routerlink="guides"
class="mat-focus-indicator docs-navbar-hide-small docs-button mat-button mat-button-base" tabindex="0" aria-disabled="false"
href="/guides">
```

_The parts from which element is built from :_

1. **Tag name** (the very first text value in our element is a tag name - here it's **a**)
2. **Attribute name** (name of the attribute is some text value, it might be separate or in format attribute="some value". For example in this element **href**)
3. **Attribute value** (the value of attribute,in Chrome dev tools comes orange colored, comes after **=** sign, in "" marks. Here attribute **href** has the value **"/guides"**)\
   _Attributes might come without values (like **\_ngcontent** in this example)_

#### \<text ... - Tag Name **NAME = "VALUE" or NAME - attributes**  <a href="#text----tag-namename--value-or-name---attributes" id="text----tag-namename--value-or-name---attributes"></a>

### **Build Xpath** <a href="#build-xpath" id="build-xpath"></a>

Just remember simple rule - _**always start from //**_

Next after // we need to tell what kind of element to search by writing a Tag Name of element, like that **//a** or we can set to search all element with **//\***

_Our element is **a** , so first part of our Xpath is //a_

After //a we can make search more accurate, by telling which attributes should our element contain with opening \[ ] .

//a\[]

Remember the href attribute? Attribute in xpath should start with @

_**//a\[@href]**_

But we can make it even more accurate, providing a value of attribute

_**//a\[@href='/guides']**_\
By the way it is almost the same as _**//\*\[@href='/guides']**_

After one element we can look into child element from this one.. or parent

Just remember the syntax :

#### Parent element of selected element <a href="#parent-element-of-selected-element" id="parent-element-of-selected-element"></a>

_**//a\[@href='/guides']//parent::**and here everything repeats from beginning - tag name, attribute.._

_**//a\[@href='/guides']//parent::nav\[@aria-label='Top Toolbar']**_

#### Child element of selected element <a href="#child-element-of-selected-element" id="child-element-of-selected-element"></a>

For child it looks more compact

_**//a\[@href='/guides']//span\[text()='Guides'] -** with **text()** we can search for text value instead of attribute_

#### Order of same elements <a href="#order-of-same-elements" id="order-of-same-elements"></a>

You have few similar elements but need to pick exact one of them?

_**(//a)\[1] -** for exact order | **(//a)\[last()] -** for the last element | **(//a)\[last()-2] -** expressions_

#### Dynamic ID or CLASSNAME <a href="#dynamic-id-or-classname" id="dynamic-id-or-classname"></a>

You have an id with some dynamic part in it which always changes?

Let's say you have an id or class that looks like **id="user.name-13"**\
We can cut a part from this id with **contains** expression

Like this **//\*\[contains(@id,'user.name')]**

#### Difference between Mobile and Web elements <a href="#difference-between-mobile-and-web-elements" id="difference-between-mobile-and-web-elements"></a>

Text - in Web, text locator is **text()** in Mobile - **@text**

For id in Android we use - **@resource-id** in Web just - **@id**
