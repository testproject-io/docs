# Using TestProject with iFrames

From a browser's perspective, an iframe, or inline frame, is an html document embedded inside of another html document. They can be helpful for encapsulating html on a part of page, but they can also be a bit tricky to use in test automation.

## Finding Elements

When most test automation framework are looking for elements on a page, they will only look for the element in the current document. This means that if the element you want is inside of an iframe, it won't find it since that iframe is considered to be a separate document. 

TestProject's Smart Recorder, on the other hand, can deal with iFrames seamlessly. Simply click through your test scenario as you usually would and when you run the test, TestProject's AI will handle the iframe switch for you seamlessly. 

If you are still using the old test recorder in TestProject, you might need to manually create steps that navigate you into the iFrame.  

## iFrame Example \(For Legacy Test Recorder\)

If you have not yet setup a project and test, you can learn how to create them in the documentation section on [web testing](../using-the-smart-test-recorder/web-testing/). For this example, set up a test that navigates to this URL: [http://the-internet.herokuapp.com/iframe](http://the-internet.herokuapp.com/iframe) . This is an example page that we can use to practice working with iframes. 

Start up the test recorder and for this example let's see if we can type something in the editor text box. Normally with the test recorder you can just click on the element on the page you want to interact with and the test recorder will add a test step with that element and action. However, in this case the editor text box is inside an iframe so \(if you are using the legacy recorder\) when you try to click on it you will see that no test step is added.

### Navigate to iFrame

In order to actually interact with an element inside the iframe, you will first need to tell TestProject to navigate into that iframe. In order to do this you can use the Switch to iFrame action. This action is available through the Element Extensions addon. More information on installing and using addons can be found in the documentation [here](../testproject-addons/using-addons-in-the-testproject-recorder.md). 

![iFrame action from Element Extensions Addon](../.gitbook/assets/image%20%2899%29.png)

This action, will allow you to navigate into the iframe, but in order to do that you will need to let it know what element on the page is the iframe in which you are interested. You can find the iframe id on the page using the Element Explorer.

![iframe ID in Element Explorer](../.gitbook/assets/image%20%2818%29.png)

Once you have found the ID you can close the element explorer and return to the Create Step panel and click on select element. On the next panel we can search for elements, but since the iframe has not yet been added to the test, you can use the plus at the bottom of this panel to add a new element.

![Add a New Element](../.gitbook/assets/image%20%28132%29%20%281%29.png)

Name the element to something like iframe and set the element type to be a generic web element. For the locator, use ID and then in the text box type in the ID you found in the Element Explorer.

![Create iframe element](../.gitbook/assets/image%20%2895%29%20%281%29.png)

You can then click on the Create button to create this element and add it your test step. Once you have done that, use the more option beside the test step and choose the Run Until Here option.

![More Menu](../.gitbook/assets/image%20%2887%29.png)

### Locate Elements in an iFrame

Now that you are inside the iFrame you can start to interact with elements on this part of the page. The test recorder still won't record the clicks and interactions on the screen, but we can easily find the elements we want using the Element Explorer. 

![iFrame Element](../.gitbook/assets/image%20%28117%29%20%282%29.png)

You can see that the id of the element is tinymce and then from the menu for this element we can select Actions and then Clear Contents to add a step that will clear the contents of the cell.

![Clear Contents Action](../.gitbook/assets/image%20%28134%29%20%281%29.png)

Once you hit create to create the step, you can follow a similar process to create a test step that lets you type in the text you want, but using the Type text action.

## Conclusion

iFrames can be a bit challenging to deal with in UI test automation, but you can see that by using the switch to iFrame action in combination with other tools like the Element Explorer, you are able to execute the actions you want. 

Even better, if you switch to using the new Smart Test Recorder, you can let TestProject do all the heavy lifting for you and interact with elements inside of iFrames as seamlessly as you do any other element on a page. Maybe now is a good time to switch to the new Smart Recorder!

