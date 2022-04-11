---
description: >-
  In this Article we will use the HTTP REQUEST Jenkins plugin to make custom
  calls for the TestProject API.
---

# How to set an API call from Jenkins

## First, install the HTTP Request Plugin for Jenkins. If you already have it, you can skip this step. <a href="#first-we-install-the-http-request-plugin-for-jenkins-if-you-already-have-it-you-can-skip-this-step" id="first-we-install-the-http-request-plugin-for-jenkins-if-you-already-have-it-you-can-skip-this-step"></a>

1. In your Jenkins dashboard, go to **Manage Jenkins**

![](https://downloads.intercomcdn.com/i/o/194800896/390d5535b4450fcb283b5ee8/image.png)

2\. Go to **Manage Plugins**.\


![](https://downloads.intercomcdn.com/i/o/194801182/551b8a64caaead3607be06d5/image.png)

3\. Go to **Available** and search for **HTTP Request**\


![](https://downloads.intercomcdn.com/i/o/194801679/9fde5322280b627ff6aaa0ab/image.png)

4\. Select the plugin and **Install Without Restart**.\


![](https://downloads.intercomcdn.com/i/o/194801890/6d188ee050c644c6c4029319/image.png)

## Now we shall create the FreeStyle project for the API call. <a href="#now-we-shall-create-the-freestyle-project-for-the-api-call" id="now-we-shall-create-the-freestyle-project-for-the-api-call"></a>

1. Back in your Jenkins dashboard, select **New Item**.

![](https://downloads.intercomcdn.com/i/o/194802787/74b1e211513cab057ccbcdf2/image.png)

2\. Select **Freestyle project** and give it a name.

3\. In this window, you can configure the project to your liking. In this article, we will focus on the API call. Go to build, press Add Build Step, **and select HTTP Request**.

![](https://downloads.intercomcdn.com/i/o/194804092/00fa01d053cf88e80fc573b0/image.png)

## Now we will create the URL for the request. <a href="#now-we-will-create-the-url-for-the-request" id="now-we-will-create-the-url-for-the-request"></a>

1. Go to your TestProject account and click on **Integrations -> API**

![](https://downloads.intercomcdn.com/i/o/194804667/bc2b8d6a2e1ea45bc8ed4cdb/image.png)

2\. If you do not have an API key, click on **Create API Key**; now, we can copy it for further use in our Jenkins Project.

3\. After we have the API Key, we press on **API Documentation. This will open the documentation window.**

4\. In this window, we will click on **Authorize** and enter our API key.

5\. Here, we will select which API call we wish to invoke. For this article we will create a **Project Parameter** with an API Call.

6\. Scroll down to **ProjectParameters** and select the **Create New Project Parameter**,

![](https://downloads.intercomcdn.com/i/o/194806700/82ba920d268d49dc2af9adc1/image.png)

We can see the request method. In this case it will be POST.

Press on **Try It out** to see the body and parameters of the request.

7\. Now, we can see the request body and parameters needed to create a new project parameter.\
\
First, we will get the project id, go to your TestProject account, find your project, and select the three dots near it -> **Copy Id**.

![](https://downloads.intercomcdn.com/i/o/194807464/82aece2d701fb5d1e1811f21/image.png)

Now that you have the ID, you can do the following:

![](https://downloads.intercomcdn.com/i/o/194809459/4f922cb9be85213186f1c911/image.png)

8\. You can press on Execute to see the Request URL **OR** take the URL from here and fill in the {projectid} with your project id.

![](https://downloads.intercomcdn.com/i/o/194810143/8f2d8f7cc53240a6f0183dd1/image.png)

## Now we will go back to the Jenkins dashboard and fill in the HTTP Request build Step. <a href="#now-we-will-go-back-to-the-jenkins-dashboard-and-fill-in-the-http-request-build-step" id="now-we-will-go-back-to-the-jenkins-dashboard-and-fill-in-the-http-request-build-step"></a>

![](https://downloads.intercomcdn.com/i/o/194811463/4bc0e414fe307b4d0ae2b72b/image.png)

![](https://downloads.intercomcdn.com/i/o/194812461/cf70ff60373df1475f1c1c54/image.png)

After we save the Request, we can now build it whenever we want, and you can build it in your CI pipeline.

After we run the Build we will get the following:

![](https://downloads.intercomcdn.com/i/o/194813223/f084c1a34e24e6880ef03afd/image.png)

It was a success, and now we can see the new Project Parameter!

![](https://downloads.intercomcdn.com/i/o/194813453/df6cfca180be4d8566b3d393/image.png)

Happy Testing!
