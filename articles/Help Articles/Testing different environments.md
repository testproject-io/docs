---
description: >-
  In this article we will utilize Data Driven capabilities to test on different
  environments.
---

# Testing different environments

First we will create a CSV file from the test we wish to run on multiple testing environments.

On the right side of the test, we have 3 dots, click on them and click on **Data Source Template**.

![](<../../.gitbook/assets/image (563).png>)

After that we have the **ApplicationURL** header, here we will insert our different testing environment URLs

![](<../../.gitbook/assets/image (455).png>)

Now we shall attach this Data Source to the test.

Go to the Data Sources Tab and add the CSV file we just edited.

![](<../../.gitbook/assets/image (521).png>)

Give it a name and create.

Now when we run the test, we will select '**Use Data Source**'

And choose the one we just uploaded.

There we go, now our test will execute on all the different testing environments we listed.

We can always edit and add more in the future in case it is needed.

Happy Testing!

\
