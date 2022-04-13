---
description: Learn how to integrate TestProject with Microsoft Azure Pipelines.
---

# Setup TestProject with Azure DevOps Pipelines by using Web Hooks

To achieve CI/CD process and run TestProject automation as part of your pipeline in Azure DevOps environment follow the next steps

\
In Azure, go to your project settings, from there navigate to **Service hooks**, and proceed to **Create a subscription**.\
Here, select the **Web Hooks** service in order to provide event communication via HTTP, and hit next.

![](<../../.gitbook/assets/image (528) (1).png>)

In the **Trigger** section, you can choose when to execute the test. We will choose release created, to trigger the test to execute when the release is done.\
\
In the **Filters** section, you can choose a pipeline.\
In case you already have a pipeline set up for TestProject, you can just select it and hit **Next**.

![](<../../.gitbook/assets/image (519).png>)

In case you do not, you will need to create one.\
You can see a guide on how to set up your pipeline in this video:\
[https://www.youtube.com/watch?v=XGTvGE8oalE\&t=17s](https://www.youtube.com/watch?v=XGTvGE8oalE\&t=17s)\


In the **Action**, next, you will need to provide the **API endpoint URL**.

![](<../../.gitbook/assets/image (469) (1) (1).png>)

\
The URL should be:\
[**https://api.testproject.io/v2/projects/{PROJECT\_ID}/jobs/{JOB\_ID}/run**](https://api.testproject.io/v2/projects/%7BPROJECT\_ID%7D/jobs/%7BJOB\_ID%7D/run)\
\
You can get your project and job ID's from the TestProject website.\
This is how you get your project ID:

![](<../../.gitbook/assets/image (479) (1) (1).png>)

And this is how you get your job ID from inside that project:

![](<../../.gitbook/assets/image (520).png>)

Your URL should end up looking something like this:\
[**https://api.testproject.io/v2/projects/UKwphfwhHkaBQgYuarfUng/jobs/IRQofWcTyEStSR0AZJkeyA/run**](https://api.testproject.io/v2/projects/UKwphfwhHkaBQgYuarfUng/jobs/IRQofWcTyEStSR0AZJkeyA/run)\
\
You do not need to fill in the Basic authentication username and password, however you will need to fill in the **HTTP headers** field with your **API key**, and that key must have access to the project you intend to use.\
\
The correct format is:\
**Authorization: {API\_KEY}**

![](<../../.gitbook/assets/image (504) (1).png>)

This is how you can create or find your API key using TestProject:\
\
You will need to go to the **Integrations** section, and into the **API** tab.\
From here you will be able to see all available keys or create one.

![](<../../.gitbook/assets/image (563) (1).png>)

When creating a key, you can restrict it's access, and in this example it will be restricted to only the project we want to use with the API.

![](<../../.gitbook/assets/image (536) (1) (1).png>)

After creating the API key, all you need to do is **Copy** it:

![](<../../.gitbook/assets/image (501).png>)

And your header should be similar to this:\
**Authorization: P1KVqUyasbQRhUumGh71ARi3nauIn6UXNphml3\_Itr81**

After entering all the details correctly, service hook setup should now be complete. You can hit **Test** to see if you have done everything properly, and then hit **Finish** to complete the process.
