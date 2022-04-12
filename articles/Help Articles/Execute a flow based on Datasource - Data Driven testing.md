---
description: CSV, Data driven tests, Datasources.
---

# Execute a flow based on Datasource - Data Driven testing

Sometimes we want to preconfigure which flows or parts of our main tests should be executed. We can do it dynamically based on our application, but sometimes there is

**A much simpler solution**.

This solution includes True/False values on your CSV file that you upload to TestProject as a data source, you can then use this data-source to run your tests, you will have option to determine which sub-tests the main test should execute.

For example this is my **main test:**

![](<../../.gitbook/assets/image (537).png>)

These are the parameters:

![](<../../.gitbook/assets/image (551).png>)

These are the conditions on the sub-tests:

![](<../../.gitbook/assets/image (483).png>)

And this is the second sub-test

![](<../../.gitbook/assets/image (511).png>)

Now we will use this **data source**:

![](<../../.gitbook/assets/image (550).png>)

You can determine which subtest will run on each iteration. (all, none or some)

![](<../../.gitbook/assets/image (476).png>)

![](<../../.gitbook/assets/image (462).png>)

![](<../../.gitbook/assets/image (544).png>)

Now by changing the values on the CSV file I can choose which sub-tests should be executed during run-time.
