# Getting Started With Using the TestProject API

TestProject has a RESTful API that can be used to help automation some of the actions in TestProject. This API can be especially helpful when you are trying to us TestProject in your CI environments.

Getting started with the TestProject API is a straightforward and simple process.

## Getting an API Key

The first thing you will need to do is to generate an API key which allows access to API for your account. In order to do that, open the TestProject application and go to the Integration tab and select the API option

![TestProject API](../.gitbook/assets/image%20%28163%29.png)

From there you can create a new API key and set the access you want it to have. API keys can have unrestricted access which means that they can be used in any project or they can be scoped to only have access to specific projects.

![API Key Scopes](../.gitbook/assets/image%20%28215%29.png)

## Using the API Key

Once you've setup that key you can copy it and use it in API call that you make. If you are just trying something out in the API you can play around with it directly in the [API documentation page](https://api.testproject.io/docs/v2/#/). At the top of the page, click on the Authorize button and paste in your API key.

![Authorize the API](../.gitbook/assets/image%20%2853%29.png)

If you are calling the API from another tool or in your CI etc. you will need to specify the key in the `headers` as an `Authorization` header

```text
Authorization:<key name>
```





