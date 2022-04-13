---
description: >-
  in this article we will learn how to run multiple tests in a job without
  restarting the application or browser.
---

# Running multiple tests in a job without restarting the app/browser

First, we need to create a test. We will use the youtube website for this example:\


![](<../../.gitbook/assets/image (452) (1) (1).png>)

After creating a simple test with a few steps, we will duplicate the test, add some steps, and disable the first ones(you can delete them as they have no use) :\


![](<../../.gitbook/assets/image (477) (1) (1) (1).png>)

As you can see, the navigation step is disabled (does not apply in a mobile test), so the test will not try to open the website.\
Now, we need to create a job by clicking the add new job option in the project toolbar:\


![](<../../.gitbook/assets/image (535).png>)

And when you get to the 3rd step in creating a job, you will notice this switch below:\


![](<../../.gitbook/assets/image (474) (1) (1).png>)

or if using a mobile test:

![](<../../.gitbook/assets/image (542) (1).png>)

now drag and drop your tests to the job on the right:\


![](<../../.gitbook/assets/image (530).png>)

And you are good to go; you can now run the job.

\
