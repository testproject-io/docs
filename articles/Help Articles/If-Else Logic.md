---
description: >-
  Here we'll give a brief overview on how to create if/else statements using the
  TestProject platform.
---

# If-Else Logic

#### If-Else with TestProject Recorder <a href="#if-else-with-testproject-recorder" id="if-else-with-testproject-recorder"></a>

**Note: You need agent version 0.65 and above,** [**click here to download Latest**](https://app.testproject.io/#/download)**.**

With TestProject Conditions feature, you can set up a Condition to check **BEFORE** the execution of the step, thus achieving the 'If' statement.

You can find the Conditions here:

In the Recorder, locate the required step and click on the Advanced Options

![](<../../.gitbook/assets/image (522) (1).png>)

![](<../../.gitbook/assets/image (511) (1) (1).png>)

And in the Step Menu:

![](<../../.gitbook/assets/image (545) (1).png>)

#### If/Else example based on label text <a href="#ifelse-example-based-on-label-text" id="ifelse-example-based-on-label-text"></a>

Let's take simple scenario that check for a text label, IF the text we got is the text that is expected we execute the next step, ELSE we ignore it.

For example, we will take the text of the following Label:

![](<../../.gitbook/assets/image (568) (1).png>)

Hover over the element, press double shift to freeze it, in Actions pick Get Text:

![](<../../.gitbook/assets/image (485) (1).png>)

Save the text into a Parameter.

![](<../../.gitbook/assets/image (552) (1).png>)

Next, lets create a step that will type text to a TextArea only if the text is Equal to "TestProject"

![](<../../.gitbook/assets/image (465) (1) (1).png>)

And add the condition in the step:

![](<../../.gitbook/assets/image (551) (1) (1).png>)

If the text is NOT equal, the step will not execute and will be shown in grey.

![](<../../.gitbook/assets/image (451).png>)

In the reports, it will look like so:

![](<../../.gitbook/assets/image (475) (1) (1).png>)

#### **If/Else with different test flows** <a href="#ifelse-with-different-test-flows" id="ifelse-with-different-test-flows"></a>

Now let's take another scenario that evaluate the **sum of 2 values** operation and **IF** we get the wanted result, trigger flow A (Sub Test A) ELSE triggers flow B (Sub Test B)

1. Sum 1+2 and save the result to "**value"** parameter
2. If value = 3 "flow A"
3. Else flow B

Here how it achieved with TestProject recorder:

![](<../../.gitbook/assets/image (547) (1) (1).png>)

Now we call subtest A if the value from the previous step was 3:

Press on 'Add test as step':

![](<../../.gitbook/assets/image (556) (1) (1).png>)

Search the test name:

![](<../../.gitbook/assets/image (521) (1).png>)

In the advanced options, we will add the condition

![](<../../.gitbook/assets/image (553) (1).png>)

And now the step will show the 'if' symbol:

![](<../../.gitbook/assets/image (478) (1) (1).png>)

To launch Flow B (Subtest B) we will check the opposite condition of the previous step, so we will check if it NOT equal to 3:

![](<../../.gitbook/assets/image (557) (1).png>)

We have achieved If 3 flow A Else Flow B.

In the reports, you will see flow A execute and flow B skipped:

![](<../../.gitbook/assets/image (484) (1).png>)
