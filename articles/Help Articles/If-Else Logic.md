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

![](https://downloads.intercomcdn.com/i/o/264659988/e95698c5e3b7a61acab4ad74/image.png)

![](https://downloads.intercomcdn.com/i/o/264660112/627c597e3c53b12591089e86/image.png)

And in the Step Menu:

![](https://downloads.intercomcdn.com/i/o/400264050/61deed18064465740c0d42ea/image.png)

#### If/Else example based on label text <a href="#ifelse-example-based-on-label-text" id="ifelse-example-based-on-label-text"></a>

Let's take simple scenario that check for a text label, IF the text we got is the text that is expected we execute the next step, ELSE we ignore it.

For example, we will take the text of the following Label:

![](https://downloads.intercomcdn.com/i/o/264746699/a449bbcfc8db46f4242c4c1d/image.png)

Hover over the element, press double shift to freeze it, in Actions pick Get Text:

![](https://downloads.intercomcdn.com/i/o/264746930/7655a78bdb5e3d13ffdf839e/image.png)

Save the text into a Parameter.

![](https://downloads.intercomcdn.com/i/o/264747215/ea9eb41f61b8ab6a924635f1/image.png)

Next, lets create a step that will type text to a TextArea only if the text is Equal to "TestProject"

![](https://downloads.intercomcdn.com/i/o/264844137/0f9eca3429e650cdabefea8d/image.png)

And add the condition in the step:

![](https://downloads.intercomcdn.com/i/o/264747974/9c5918f26435aea36b4224da/image.png)

If the text is NOT equal, the step will not execute and will be shown in grey.

![](https://downloads.intercomcdn.com/i/o/264749406/72a559635381fdeee192aa4e/image.png)

In the reports, it will look like so:

![](https://downloads.intercomcdn.com/i/o/264752180/684f74032b92fc562a242010/image.png)

#### **If/Else with different test flows** <a href="#ifelse-with-different-test-flows" id="ifelse-with-different-test-flows"></a>

Now let's take another scenario that evaluate the **sum of 2 values** operation and **IF** we get the wanted result, trigger flow A (Sub Test A) ELSE triggers flow B (Sub Test B)

1. Sum 1+2 and save the result to "**value"** parameter
2. If value = 3 "flow A"
3. Else flow B

Here how it achieved with TestProject recorder:

![](https://downloads.intercomcdn.com/i/o/264753652/820e6d6c28ffe09bf224e867/image.png)

Now we call subtest A if the value from the previous step was 3:

Press on 'Add test as step':

![](https://downloads.intercomcdn.com/i/o/264753952/aa4c0d23a5c4dd80e8be5e77/image.png)

Search the test name:

![](https://downloads.intercomcdn.com/i/o/264844562/e6963533ba549b2283f25e7b/image.png)

In the advanced options, we will add the condition

![](https://downloads.intercomcdn.com/i/o/264754455/5b6416094910fdf810f859e3/image.png)

And now the step will show the 'if' symbol:

![](https://downloads.intercomcdn.com/i/o/264839379/07eb7ac37bf8c8084f332625/image.png)

To launch Flow B (Subtest B) we will check the opposite condition of the previous step, so we will check if it NOT equal to 3:

![](https://downloads.intercomcdn.com/i/o/264755594/6c663cef3bb1f87cb6499bf9/image.png)

We have achieved If 3 flow A Else Flow B.

In the reports, you will see flow A execute and flow B skipped:

\


![](https://downloads.intercomcdn.com/i/o/264843582/4da28d7d4ca3e5d98b74719e/image.png)
