# Expanding UI Automation Capabilities with Javascript

The powerful tools TestProject provides around finding and using elements will be what you need for most application, but there are times when you might need to do something that goes beyond what can be done with built in element locators. In that case you may want to consider using Javascript to help you accomplish the task at hand. 

## Javascript Addons

There are some handy ways to use javascript in TestProject and to access them you need to have a couple of [addons](../testproject-addons/using-addons-in-the-testproject-recorder.md) installed. The Web Extensions addon will give you the ability to execute javascript directly against the page you are one and the Javascript Actions addon will give you access to some built in javascript actions like clicking with javascript that can be useful.

## Example Using Javascript

Let's take a look at an example to see what it looks like to use these actions. For this example we will use a very [simple example page](http://the-internet.herokuapp.com/add_remove_elements/) where we can click on buttons to add and remove elements from the page. If you have not yet setup a project, you can follow the documentation on [creating a web test](../using-the-smart-test-recorder/web-testing/) to see how to get started. For this example the URL used in the test will be [http://the-internet.herokuapp.com/add\_remove\_elements/](http://the-internet.herokuapp.com/add_remove_elements/). 

### Execute Javascript Directly

The first thing we will look at is executing javascript directly on the page. Usually you will not want to do this as you can be modifying the page from how it presenting to users or you can be interacting with it in ways that interactive users will not be. However, sometimes there are cases were you may have a specific need that requires you to be able to interact directly with javascript on the page or that requires you to run some custom javascript on the page. In these case you can use the Execute Javascript action in TestProject. 

On the page we are looking at, there is a button that we can click to add a new element to the page. If we inspect that element, we can see that it calls a javascript method called `addElement()`. 

![addElement\(\)](../.gitbook/assets/image%20%28141%29.png)

We could of course just setup TestProject to click directly on the button, but in order to demonstrate using the Execute Javascript action, let's take a look at how we could call this method directly from our test.

In order to use the Execute Javascript action we need to add a test step and then set the step Type to Action.

![Set Step Type to Action](../.gitbook/assets/image%20%28143%29.png)

We can then search for javascript in the actions and select the Execute Javascript option. Notice that this action come from the web extensions addon.

![Execute Javascript Action](../.gitbook/assets/image%20%2860%29.png)

This addon will now allow us to specify the javascript code that we want to run. In our case we want to run the `addElement()` method, so we can type that into the code input parameter for this addon. The `addElement()` method does not have any arguments, so we can leave that field blank.

![Execute addElement method](../.gitbook/assets/image%20%2893%29.png)

With that we can click on Create to create the test step and then run the test to see what happens.

![Run Test](../.gitbook/assets/image%20%28184%29.png)

When we do that, you can see that it has added a new button to the page

![Delete Button Added](../.gitbook/assets/image%20%28155%29%20%281%29.png)

Let's try doing one more thing with directly executed javascript. Let's set a hidden attribute on that Delete button we just created.  To do this we will once again create a new test step with the type set to Action and the Action itself set to Execute JavaScript. Now to modify the element attribute with Javascript we need to somehow get the element. We can find out some information about the element by freezing it and then looking at it's attributes.

To freeze and element we just hoover over it and hit shift twice quickly. We can then go to the Attributes option and see what attributes this element has.

![Element Attributes](../.gitbook/assets/image%20%28140%29.png)

To get this element with Javascript we can use the class and access it `document.getElementsByClassName()` method. Since this method returns a list, we need to index it to get the first element and then call the `setAttribute()` method on that element. Putting that all together the javascript code that we will need to execute to hide this button will look like this:

```text
document.getElementsByClassName("added-manually")[0].setAttribute("hidden", true);
```

We can put that code directly into the step in TestProject

![Execute Javascript](../.gitbook/assets/image%20%28187%29.png)

If we then run this step, the Delete Button will be hidden.

### Javascript Click

Now that we have a hidden element on the page, imagine that you wanted to be able to click on it. You clearly can't use the regular click mechanism in TestProject to that since that only works for elements that are visible to users. However, the element is still on the page \(even if it is hidden\) and so we can interact with it through javascript. We could setup another javascript action step to do this, but let's look at another way we can do this.

First of all, we will add another test step and leave the Type as Element Action. We then need to select the element, but since it is not visible on the page we will need to find it in another way. We can do this with the Element Explorer

![Element Explorer](../.gitbook/assets/image%20%2854%29.png)

If we then drill down into the on page elements we can find the hidden Delete button

![Hidden Delete Button](../.gitbook/assets/image%20%2891%29.png)

Clicking on this will bring up the menu options for this element and we can then copy the xpath to use in our test step. We can then close the element explorer and return to the Create Step panel and click on select element. We can then use the plus at the bottom of that panel to add a new element.

![Add a New Element](../.gitbook/assets/image%20%28132%29%20%281%29.png)

We can name the element, set the type to Button and use the XPATH locator. We can then paste in the xpath that we copied and add the element to our project.

![Create New DeleteButton Element](../.gitbook/assets/image%20%28150%29.png)

The element is then immediately available to choose in the select element panel and so we can click on it to use that element in our test step. The remaining thing is to choose the step action. We can't just click on this element since it is hidden, but let's try sending a click using javascript. We can search for javascript and then choose the Click \(using JavaScript\) action which is included in the Javascript Actions addon.

![Javascript Click Action](../.gitbook/assets/image%20%2811%29.png)

At this point we can run this step and the button gets 'clicked' even though it is hidden. This can be verified by checking in the Element Explorer, where the Delete Button element will no longer be available. 

So we can see that although you probably won't usually want to do things like click on a hidden button, there are ways to do things like this with javascript if you really need to. TestProject's javascript addons give you the ability to work with details like this if the testing you are doing requires it.

