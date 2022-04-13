---
description: >-
  In this article we will learn how to extract test steps between tests and
  projects using multi-select and nested Tests.
---

# Transferring test steps between Tests or Projects

First we go to the Editor or the recorder of the test you want to extract the steps from:

![](<../../.gitbook/assets/image (507) (1) (1) (1).png>)

We will now select all the steps we want to extract and move between tests or projects.

For example:

![](<../../.gitbook/assets/image (491) (1).png>)

Now we shall click on the '**Group steps into test**' button.

![](<../../.gitbook/assets/image (549) (1) (1).png>)

This will extract those steps into a auto generated test with a name of your choosing.

It will make those steps as nested test inside your test so no need to worry they will still execute.

Now we go back to our Tests folder, we will see the test we just generated.

![](<../../.gitbook/assets/image (500) (1).png>)

Now if we just want another test to use those steps we can just call it as a nested test.

By adding a Test as a step:

![](<../../.gitbook/assets/image (470) (1) (2).png>)

To use those steps on a different project we shall click on the 3 dots near the test in your Tests page.

![](<../../.gitbook/assets/image (516) (1).png>)

And click on Copy to project

![](<../../.gitbook/assets/image (466) (1) (1).png>)

Now in the project we moved those steps into we can call that test as a nested test wherever we want those steps to execute, like seen above.

Happy testing!
