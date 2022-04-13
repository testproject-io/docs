---
description: >-
  In this Article we will use the HTTP REQUEST Jenkins plugin to make custom
  calls for the TestProject API.
---

# How to set an API call from Jenkins

## First, install the HTTP Request Plugin for Jenkins. If you already have it, you can skip this step. <a href="#first-we-install-the-http-request-plugin-for-jenkins-if-you-already-have-it-you-can-skip-this-step" id="first-we-install-the-http-request-plugin-for-jenkins-if-you-already-have-it-you-can-skip-this-step"></a>

1. In your Jenkins dashboard, go to **Manage Jenkins**

![](<../../.gitbook/assets/image (483) (1).png>)

2\. Go to **Manage Plugins**.

\


![](<../../.gitbook/assets/image (515) (1).png>)

3\. Go to **Available** and search for **HTTP Request**

\


![](<../../.gitbook/assets/image (458) (1).png>)

4\. Select the plugin and **Install Without Restart**.

\


![](<../../.gitbook/assets/image (480) (1).png>)

## Now we shall create the FreeStyle project for the API call. <a href="#now-we-shall-create-the-freestyle-project-for-the-api-call" id="now-we-shall-create-the-freestyle-project-for-the-api-call"></a>

1. Back in your Jenkins dashboard, select **New Item**.

![](<../../.gitbook/assets/image (514) (1).png>)

2\. Select **Freestyle project** and give it a name.

3\. In this window, you can configure the project to your liking. In this article, we will focus on the API call. Go to build, press Add Build Step, **and select HTTP Request**.

![](<../../.gitbook/assets/image (506) (1) (1).png>)

## Now we will create the URL for the request. <a href="#now-we-will-create-the-url-for-the-request" id="now-we-will-create-the-url-for-the-request"></a>

1. Go to your TestProject account and click on **Integrations -> API**

![](<../../.gitbook/assets/image (470) (1) (1).png>)

2\. If you do not have an API key, click on **Create API Key**; now, we can copy it for further use in our Jenkins Project.

3\. After we have the API Key, we press on **API Documentation. This will open the documentation window.**

4\. In this window, we will click on **Authorize** and enter our API key.

5\. Here, we will select which API call we wish to invoke. For this article we will create a **Project Parameter** with an API Call.

6\. Scroll down to **ProjectParameters** and select the **Create New Project Parameter**,

![](<../../.gitbook/assets/image (454) (1) (1).png>)

We can see the request method. In this case it will be POST.

Press on **Try It out** to see the body and parameters of the request.

7\. Now, we can see the request body and parameters needed to create a new project parameter.\
\
First, we will get the project id, go to your TestProject account, find your project, and select the three dots near it -> **Copy Id**.

![](<../../.gitbook/assets/image (558) (1) (1).png>)

Now that you have the ID, you can do the following:

![](<../../.gitbook/assets/image (559) (1).png>)

8\. You can press on Execute to see the Request URL **OR** take the URL from here and fill in the {projectid} with your project id.

![](<../../.gitbook/assets/image (532) (1) (1).png>)

## Now we will go back to the Jenkins dashboard and fill in the HTTP Request build Step. <a href="#now-we-will-go-back-to-the-jenkins-dashboard-and-fill-in-the-http-request-build-step" id="now-we-will-go-back-to-the-jenkins-dashboard-and-fill-in-the-http-request-build-step"></a>

![](<../../.gitbook/assets/image (550) (1).png>)

![](<../../.gitbook/assets/image (564) (1).png>)

After we save the Request, we can now build it whenever we want, and you can build it in your CI pipeline.

After we run the Build we will get the following:

![](<../../.gitbook/assets/image (567).png>)

It was a success, and now we can see the new Project Parameter!

![](<../../.gitbook/assets/image (450).png>)

