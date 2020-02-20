# Steps Widget

A test in TestProject is composed of a number of tests steps. These steps can be automatically added to the test when working with the test recorder or they can be manually added using the Add Step plus icon at the bottom of the test widget. In either case the steps widget can be accessed by clicking on the test step of interest. 

### Test Step Widget

When creating a new test step there are a number of options on the steps widget

![Steps Widget](../../.gitbook/assets/image%20%2877%29.png)

### Comments

Comments about the test step can be entered in section one. This can be helpful for clarifying what the intention of the test step is or can be a place to leave a message for team mates with information that might helpful when running this step in the future.

### Step Type

Section 2 is where the step type is set. By default a newly create test step will be set to the Element Action type, but steps can also by set to direct actions \(not on a particular element\) or to run another test.

![Change Step type](../../.gitbook/assets/image%20%28160%29.png)

### Actions

The options in the third section will depend on the step type that is selected. If the step type is Element Action this section will have options to choose the element and the action. If the step type is Action, it will only have an option to choose the action and if the step type is Test, it will have an option to choose the test to run. Detail on the available actions can be found [_here_](../available-actions.md)_._

### Failure Behavior

The next section defines what will happen when the test step fails. The default behavior of a test step when it fails is to use whatever settings are in place for the entire test, but this can be overridden to either fail the test, continue the test or try to recover the test

![Failure Behavior Options](../../.gitbook/assets/image%20%28154%29.png)

This section also gives an option to define when screenshots will be taken. Screenshots can be an effective way to help with debugging test failures and so the default is to take one whenever the test step fails, but this can also be modified to take one every time the step is run, only when it passes or never. 

![When to Take a Screenshot](../../.gitbook/assets/image%20%2849%29.png)

### Step Pauses

Sometimes a test step will need to wait until something on the page is ready before it is is executed. Usually TestProject will take care of this implicitly and so the default Test Pause option is None and then test steps default to using this which means the step will execute as soon as the element is is acting on in ready. However, if there is a reason for a particular test step to wait before executing, this option can be overridden to pause for a set amount of time either before or after the test step executes.

![Pause Before Step Execution](../../.gitbook/assets/image%20%28119%29.png)

If the element a step is acting on cannot be found the step will eventually time out. The default time for this is set at the test level, but can be overridden on a step by step basis if needed.

![Override Step Timeout](../../.gitbook/assets/image%20%2888%29.png)

The is also an option to specify how many time to repeat a test step and an option to invert the test step. Inverting the test step means that if the step fails \(for example if the element could not be found\), that will be consider a pass for this test step.

