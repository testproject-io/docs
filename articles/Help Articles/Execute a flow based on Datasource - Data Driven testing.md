---
description: CSV, Data driven tests, Datasources.
---

# Execute a flow based on Datasource - Data Driven testing

Sometimes we want to preconfigure which flows or parts of our main tests should be executed. We can do it dynamically based on our application, but sometimes there is

**A much simpler solution**.

This solution includes True/False values on your CSV file that you upload to TestProject as a data source, you can then use this data-source to run your tests, you will have option to determine which sub-tests the main test should execute.

For example this is my **main test:**

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/370503673/96ec7f24c739f52512a2763e/d93c71b7faa229d39b98e64e20b7015ba5a9932c.png)

These are the parameters:

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/370503681/63e81c6b907ca7f7edeb5ab1/9567002dacb0ad7a8d11947b74f3e022ad3e0cf5.png)

These are the conditions on the sub-tests:

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/370503693/0f9dd5c4cab671a25f487e32/96f56d4f20c48dcc43c268e2fba24002adbc155c.png)

And this is the second sub-test

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/370503694/8fa18fd63e584c3e26efd902/72f6710ee126de0e4f6a522efe22965a72ac2ebf.png)

Now we will use this **data source**:

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/370503702/0f34dc2239024ae7c25528c9/37970ee70d95b20e662614e80c701341e71d6158.png)

You can determine which subtest will run on each iteration. (all, none or some)

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/370503711/f77ebb06daf80b39d943fd96/fc41940edd3f9f72ad290bc68ac64b01222db5f5\_2\_690x352.png)

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/370503720/75d3cdd759757623af80671b/8166e7eec6cfda5a763a327155a64dfe54fcaccb\_2\_690x331.png)

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/370503726/d5ad67ffe72a51f9314ecf69/d7c79ce920ed6e68bdb7219d09c70582d0ad9429\_2\_690x354.png)

Now by changing the values on the CSV file I can choose which sub-tests should be executed during run-time.
