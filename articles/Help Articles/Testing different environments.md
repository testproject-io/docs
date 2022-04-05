---
description: >-
  In this article we will utilize Data Driven capabilities to test on different
  environments.
---

# Testing different environments

First we will create a CSV file from the the test we wish to run on multiple testing environments.

On the right side of the test, we have 3 dots, click on them and click on **Data Source Template**.

![](https://downloads.intercomcdn.com/i/o/216421513/90c074d96256c136526793ce/image.png)

After that we have the **ApplicationURL** header, here we will insert our different testing environments URLs

![](https://downloads.intercomcdn.com/i/o/216421927/d47ed321ee8a6ba59a65f6fb/image.png)

Now we shall attach this Data Source to the test.

Go to the Data Sources Tab and add the CSV file we just edited.

![](https://downloads.intercomcdn.com/i/o/216422314/eab9d426c17d7a7d295fd1c4/image.png)

Give it a name and create.

Now when we run the test, we will select '**Use Data Source**'

And choose the one we just uploaded.

There we go, now our test will execute on all the different testing environments we listed.

We can always edit and add more in the future in case it is needed.

Happy Testing!

\
