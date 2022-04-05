---
description: Learn how to integrate TestProject with Microsoft Azure Pipelines.
---

# Setup TestProject with Azure DevOps Pipelines by using Web Hooks

To achieve CI/CD process and run TestProject automation as part of your pipeline in Azure DevOps environment follow the next steps

\
In Azure, go to your project settings, from there navigate to **Service hooks**, and proceed to **Create a subscription**.\
Here, select the **Web Hooks** service in order to provide event communication via HTTP, and hit next.

![](https://downloads.intercomcdn.com/i/o/199573910/cd07d7bd59b22d18635f418e/Untitled.png)

In the **Trigger** section, you can choose when to execute the test. We will choose release created, to trigger the test to execute when the release is done.\
\
In the **Filters** section, you can choose a pipeline.\
In case you already have a pipeline set up for TestProject, you can just select it and hit **Next**.

![](https://downloads.intercomcdn.com/i/o/199575038/967cc026c459b1a977428e95/Untitled.png)

In case you do not, you will need to create one.\
You can see a guide on how to set up your pipeline in this video:\
[https://www.youtube.com/watch?v=XGTvGE8oalE\&t=17s](https://www.youtube.com/watch?v=XGTvGE8oalE\&t=17s)\


In the **Action**, next, you will need to provide the **API endpoint URL**.

![](https://downloads.intercomcdn.com/i/o/199650631/faf105c2a0294fd5c5801d4f/Untitled.png)

\
The URL should be:\
[**https://api.testproject.io/v2/projects/{PROJECT\_ID}/jobs/{JOB\_ID}/run**](https://api.testproject.io/v2/projects/%7BPROJECT\_ID%7D/jobs/%7BJOB\_ID%7D/run)\
\
You can get your project and job ID's from the TestProject website.\
This is how you get your project ID:

![](https://downloads.intercomcdn.com/i/o/199666839/ca1abf19f78f5f59ece359cd/Untitled.png)

And this is how you get your job ID from inside that project:

![](https://downloads.intercomcdn.com/i/o/199667325/0dbf708f2fd1c7a41efa39e8/Untitled1.png)

Your URL should end up looking something like this:\
[**https://api.testproject.io/v2/projects/UKwphfwhHkaBQgYuarfUng/jobs/IRQofWcTyEStSR0AZJkeyA/run**](https://api.testproject.io/v2/projects/UKwphfwhHkaBQgYuarfUng/jobs/IRQofWcTyEStSR0AZJkeyA/run)\
\
You do not need to fill in the Basic authentication username and password, however you will need to fill in the **HTTP headers** field with your **API key**, and that key must have access to the project you intend to use.\
\
The correct format is:\
**Authorization: {API\_KEY}**

![](https://downloads.intercomcdn.com/i/o/199968503/0b9eb803b29baa1abc873809/image.png)

This is how you can create or find your API key using TestProject:\
\
You will need to go to the **Integrations** section, and into the **API** tab.\
From here you will be able to see all available keys or create one.

![](https://downloads.intercomcdn.com/i/o/199668143/59d9567eb36ba398db2ad214/Untitled1.png)

When creating a key, you can restrict it's access, and in this example it will be restricted to only the project we want to use with the API.\


![](https://downloads.intercomcdn.com/i/o/199668593/aa5c6801dd7c8a56ec35965f/image.png)

After creating the API key, all you need to do is **Copy** it:\


![](https://downloads.intercomcdn.com/i/o/199668729/ddf03788563250e0c81d3752/image.png)

And your header should be similar to this:\
**Authorization: P1KVqUyasbQRhUumGh71ARi3nauIn6UXNphml3\_Itr81**

After entering all the details correctly, service hook setup should now be complete. You can hit **Test** to see if you have done everything properly, and then hit **Finish** to complete the process.
