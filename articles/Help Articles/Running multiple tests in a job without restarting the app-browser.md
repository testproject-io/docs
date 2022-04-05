---
description: >-
  in this article we will learn how to run multiple tests in a job without
  restarting the application or browser.
---

# Running multiple tests in a job without restarting the app/browser

First we need to create a test. i used the youtube website for this example:\


![](https://downloads.intercomcdn.com/i/o/197758642/e1d151edb5f5ad5f47560fec/2020-04-03\_14h09\_35.png)

i have created a simple test with a few steps. then i duplicated the test, added some steps and disabled (you can delete them as they have no use) the first ones:\


![](https://downloads.intercomcdn.com/i/o/197759218/25e547be9b8a383683c32c53/2020-04-03\_14h12\_03.png)

as you can see, the navigation step is disabled (does not apply in a mobile test), so the test will not try to open the website.\
now we need to create a job by clicking the add new job option in the project toolbar:\


![](https://downloads.intercomcdn.com/i/o/197759911/5b135f430079b2bd34060c36/2020-04-03\_14h14\_38.png)

and when you get to the 3rd step in creating a job you will notice this switch below:\


![](https://downloads.intercomcdn.com/i/o/197760413/22ccbf0dfea7ee00cb449c4f/image.png)

or if using a mobile test:

![](https://downloads.intercomcdn.com/i/o/197760747/e1c72a355243573b2894b24e/image.png)

now just drag and drop your tests to the job on the right:\


![](https://downloads.intercomcdn.com/i/o/197761341/07c48a3a10d4aac58bb76216/image.png)

and you are good to go, you can now run the job.

\
