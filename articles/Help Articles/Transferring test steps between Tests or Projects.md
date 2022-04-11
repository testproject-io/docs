---
description: >-
  In this article we will learn how to extract test steps between tests and
  projects using multi-select and nested Tests.
---

# Transferring test steps between Tests or Projects

First we go to the Editor or the recorder of the test you want to extract the steps from:

![](https://downloads.intercomcdn.com/i/o/219714363/3a72011064fb5d48173ea52c/image.png)

We will now select all the steps we want to extract and move between tests or projects.

For example:

![](https://downloads.intercomcdn.com/i/o/219714912/e6c4abf807c2f4a161257fc8/image.png)

Now we shall click on the '**Group steps into test**' button.

![](https://downloads.intercomcdn.com/i/o/219715207/18037b5759986c3f68d8fd60/image.png)

This will extract those steps into a auto generated test with a name of your choosing.

It will make those steps as nested test inside your test so no need to worry they will still execute.

Now we go back to our Tests folder, we will see the test we just generated.

![](https://downloads.intercomcdn.com/i/o/219715796/ac45a25a351ea78261d4ceb2/image.png)

Now if we just want another test to use those steps we can just call it as a nested test.

By adding a Test as a step:

![](<../../.gitbook/assets/image (470) (1).png>)

To use those steps on a different project we shall click on the 3 dots near the test in your Tests page.

![](https://downloads.intercomcdn.com/i/o/219716350/e7204bbf85fa885593088eef/image.png)

And click on Copy to project

![](https://downloads.intercomcdn.com/i/o/219716469/97ff61a23c5b60f5f171be18/image.png)

Now in the project we moved those steps into we can call that test as a nested test wherever we want those steps to execute, like seen above.

Happy testing!
