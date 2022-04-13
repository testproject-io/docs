# Steps Widget

A test in TestProject is composed of a number of tests steps. These steps can be automatically added to the test when working with the test recorder, or they can be manually added using the **Add Step** plus icon at the bottom of the **steps** widget. In either case, the steps widget can be accessed by clicking on the test step of interest.

This article will show you the many features that are available for test steps created with the Smart Recorder. If you are still using the legacy recorder, you can see details on those step features in the next section of the documentation [here](broken-reference).

## Test Step Widget

There are 5 main parts to a test step, as shown in the following image.

![5 Parts of a Test Step](<../../.gitbook/assets/image (172).png>)

## Comments

Comments about the test step can be entered in section one. This can be helpful for clarifying what the intention of the test step is, or can be a place to leave a message for teammates with information that might help when running this step in the future.

## Action

The second part of a test step is the action that the step will perform. This can range from clicking on an element to typing in text to element validation and much, much more. If you click on the **action** cell in a test step you can search through all the available actions to find the one that you want. The full list of actions is can also be seen on the [Available Actions](../available-actions.md) page. Validations are also considered to be actions and you can see the full list of them on the [Available Validations](../available-validations.md) page.

## Element

Next up is the element section. This is where you define what element is being acted on. When using the smart recorder, the element locator will be automatically filled in. If you are creating a step manually, you can click on this field to search for the element. For example, if you wanted to find the password element on a page, you could type`pass`into the search bar, and it would find any elements that matched that search. Doing this search on the [TestProject example page](https://example.testproject.io/web/) will give you a result like this:

![Password Elements](<../../.gitbook/assets/image (212).png>)

You can also create your own element if you need to use a custom selector that does not show up in the list. Additionally, you can edit elements by using the Edit Element icon.

![Edit Element](<../../.gitbook/assets/image (173).png>)

This allows you to see which locators the Smart Recorder will use to find the element. The first one in the list is the one it will use by default. But if a test is running and it can't find the element using that locator it will continue on down through that list until it finds a locator that works. You can also add your own locators in here as well if you know of one that will be stable. An example of what this looks like for the password field on the TestProject example page is shown in the following image:

![Element Selectors for Password Field](<../../.gitbook/assets/image (157).png>)

You can see that it will first try to use the `CSS Selector,` but if that doesn't work it will look at a few different `XPATHs` to hopefully find the element for you.

One other item worth noticing about the element field on a test step is that you can click on the **Find Element** magnifying glass and TestProject will highlight where on the page the element is.

![Find Element on Page](<../../.gitbook/assets/image (193) (2) (2).png>)

This is very helpful to check that the locator is working correctly and to see what exactly is going on.

## Input

The fourth section on the step panel is optional, depending on the kind of action you are doing. Some actions like`click`do not require any inputs, while others like`type text`require you to enter the text that you want to be typed. The input fields will automatically appear depending, on the action selected.

## Advanced Options

The final section of the test steps panel is the Advanced Options. There are a number of options in here that allow you to control various aspects of how a step works.

### On Failure Behaviour

This option allows you to specify what you want TestProject to do if the test step fails. You can set up a default option that applies to every test step, and if you want to override that for a specific test, you can. You can choose to **Continue Test** if you want TestProject to run the remaining test steps even if this one fails. You might want to do this if you have some cleanup steps that you want to run for example.

You can, of course, choose the **Fail Test** option, which will fail the test and stop running it if the test step encounters an issue. The **Always Pass** option will make it so that any failures on the test step don't cause the test to fail. You will probably not use this option very often, but there may be times when you need to run something in a test step that you know will fail, and you don't want to cause the test to fail.

TestProject also provides a **Recovery Test** option. This option can be used to help you correct issues dynamically during test execution. For example, if you have a test step that occasionally fails because there is a missing object, you could create a test that will create that object for you, then use the Recovery Test option to choose to run that test. You can then choose what you want TestProject to do after that test runs:

* **Continue Test:** After the recovery test is executed, the current test will continue execution from the following step.
* **Fail Test:** After the recovery test is executed, the execution of the current test will stop with a "Fail" result.
* **Repeat Step:** After the recovery test is executed, the current step will be executed once again. If it passes the second time, the current test execution will continue. If the step will fail the second time (after the recovery), it will not be repeated and the current test will fail.

### Take Screenshot

TestProject can take screenshots of what is happening in your tests. This is really helpful when you are trying to debug failing tests and so this option defaults to **On Failure** which means that TestProject will take a screenshot of the application any time a test step fails. You can turn of taking screenshots completely by using the **Never** option, or you go to the other extreme and take a screenshot after each test step by choosing the **Always** option. The final choice is to take a screen when the test step passes but not when it fails. You can do this with the **On Success** option.

### Conditions

You can define conditions in TestProject that will determine if a test step is run or not. These conditions are evaluated before step execution. If any of the conditions that you define evaluate to false, the step will be skipped.

### Pause

By default, there is no pause between running test steps, but occasionally you will want to have a test step wait before or after running. You can specify the wait time in milliseconds using the **Before** or **After** options.

### Adaptive Wait

TestProject uses adaptive wait technology to ensure that you don't spend any extra time waiting for test steps to finish. Many other UI testing frameworks will require guessing at how long of a wait you should put in so that your test step doesn't fail unnecessarily, but also does not take too long to run. TestProject takes care of this with its adaptive wait technology. You can specify a max amount of time that it will wait (by default 15 seconds) but if a test step finishes in less time, TestProject will move on to the next step.

If you do have a test step that you know is going to be quite slow, you can set the max wait time to a higher value, by turning off the **Use Test Default** option.

### Context

Step context defines where the interaction with your web application happens. It can be the default DOM or an iFrame. The context is defined by a set of locators (like for elements) and when the step is executed, these locators will be taken into consideration before proceeding with the actual step action. In most cases, these are generated automatically while you record and there is no need to worry about it, but if necessary, they can be manually edited. In case there is no context defined on a step, the interaction will happen on the highest possible level of the tested DOM.

### Repeat

There may be times when you want to repeat a step a few times. Perhaps you have a test that needs to have several users and you so you want to click on a 'create new users' button a few times in a row. All you have to do to accomplish this is to specify the number of times you want TestProject to repeat the test step using the repeat option.

### Invert Step Result

Negative testing is an important tool in any tester's toolbox. You may want to create test steps that you expect to 'fail' which would be normal behavior of the application. In this case, you can enable the **Invert Step Result** option so that a failure on that step will be reported as a passing step.
