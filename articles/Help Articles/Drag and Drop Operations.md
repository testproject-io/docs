---
description: A Complete Practical Guide For Drag and Drop Actions
---

# Drag and Drop Operations

When it comes to automating applications, we want to take advantage of the automation as much as possible so that we do not have to deal with it manually.

Dragging a particular element manually over and over again can be a little bit of a headache😒.

For example:

* Files
* Images
* Videos
* Links

So you might tell yourself, "I wish someone had built an automatic action that would do that for me🤦‍♂️" In all these cases, TestProject provides ways and solutions, drag and drop operations will save us time and help us raise the level of effectiveness of our test.

Let's jump straight to the essence of how to use each and one of them:

### **1) Angular Drag and Drop:** <a href="#h_6aef82caf4" id="h_6aef82caf4"></a>

* When using this addon, all we have to do is to hover our mouse on the element we want to drag, we'll freeze the element (you can do it by pressing double shift) and then click actions and search for "Angular Drag and Drop":

![](../../.gitbook/assets/chrome\_nCMVIPdoZN.png)

*   After you have clicked on the action, you'll have to put the inputs, the inputs are destination attributes, for this example, I'll use XPath.

    We'll have to copy the XPath of the drop destination and then click on the save step:

![](../../.gitbook/assets/chrome\_GEBqF4O2xt.png)

* And that's it, now let's run this step and see how he drags and drops the element to the desired destination:

![](../../.gitbook/assets/chrome\_Md1htrDk0w.gif)

### &#x20;<a href="#h_8c4ed7792c" id="h_8c4ed7792c"></a>

### **2) Drag and Drop by Offset:** <a href="#h_89ca3be344" id="h_89ca3be344"></a>

* When using this addon once again, all we have to do is to hover our mouse on the element we want to drag, we'll freeze the element (you can do it by pressing double shift) and then click actions and search for "Drag and Drop by Offset":

![](../../.gitbook/assets/chrome\_97luFMolMH.png)

* After you have clicked on the action, you'll have to put the inputs, the inputs are coordinates after we put the correct coordinates we'll click save step:

![](../../.gitbook/assets/chrome\_EDVblzVK95.png)

* And that's it, now let's run this step and see how he drags and drops the element to the desired destination:

![](../../.gitbook/assets/chrome\_CynX9iteVL.gif)

### **3) Drag and Drop with Robot:** <a href="#h_247336577a" id="h_247336577a"></a>

*   In general, this addon moves the mouse from start coordinates to destination while holding the left click.

    First, we'll have to add a new step manually:

![](../../.gitbook/assets/chrome\_24kgoNQnGq.png)

* Then in the action section, we'll have to select "Drag and Drop with robot", after that you will see many inputs that you can give coordinates values to the robot after you have filled in the correct coordinates click on save step:

![](../../.gitbook/assets/SdPu9hgQfd.png)

* **If you noticed, we also have the option to add a timeout, some websites avoid dragging elements at a certain speed, so this option lets us choose the movement speed.**
* And that's it, now let's run this step and see how it drags and drops the element to the desired destination:

![](../../.gitbook/assets/chrome\_tVgSN3rYQO.gif)
