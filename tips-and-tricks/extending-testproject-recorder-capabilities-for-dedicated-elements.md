# Deploy new APK/IPA with TestProject APIs

If you are using an APK or IPA of an application to run tests against, you may have to frequently update it as you get new builds. Thankfully, the [TestProject APIs](https://api.testproject.io/docs/v2/) provide functionality for doing this. These APIs can of course be called from your scripting language of choice. In this article we will walk through how to do this in the interactive UI provided by the API documentation which you can find [here](https://api.testproject.io/docs/v2/). You can also find an article [here ](https://blog.testproject.io/2019/08/27/test-automation-ci-testproject-api/)on the TestProject blog which outlines how to do these calls in javascript.

## API Calls

The [API Documentation page](https://api.testproject.io/docs/v2/),shows the various API calls available. For this example we are looking at uploading an APK or IPA file and so the first call we will need to make is in the Applications section. Since we want to upload the file to an existing application we will want to use the file upload endpoint.

![File upload endpoint](../.gitbook/assets/image%20%28227%29.png)

However, as you can see in the description for this endpoint, we first need to call the  `v2/projects/{projectId}/applications/{appId}/file/upload-link` endpoint to get the location of the application files.  That end point has two parameters that wee need to fill in; the project id and the app id.

## Authorization

Before you can do any API calls, you will need to authorize the API. To do this you will need an API key. You can get you API key by going to the integrations tab and then navigating to the [API page](https://app.testproject.io/#/integrations/api). From there you can create an API key and specify what projects you want to enable for use with that key.

![Create an API Key](../.gitbook/assets/image%20%28213%29.png)

Once you have created the key, you can copy it and head over the [API documentation page](https://api.testproject.io/docs/v2/).

![Copy API Key](../.gitbook/assets/image%20%28214%29.png)

On the API Documentation page you need to click on the Authorize button.

![Authorize API Calls](../.gitbook/assets/image%20%2835%29.png)

You can then paste in your key, click on the authorize button and close the dialogue

## Get Project and App Ids

The appId can be found in TestProject using the options menu beside the application \(this tutorial assumes you have already uploaded the application and you are now trying to update it\).

![Get Application Id](../.gitbook/assets/image%20%2893%29.png)

You can get the projectId in a similar way to the appId by going to the project and using the Copy ID option on the more menu.

![ProjectId](../.gitbook/assets/image%20%28169%29.png)

## Sending API Calls

Once you have those values, you can click on the try it out button for the `upload-link` endpoint and fill in the parameters in their respective fields

![Fill in parameters](../.gitbook/assets/image%20%28222%29.png)

You can then click on the Execute button to send the request. You should get back an API response which contains the url for the application you are interested in. You can now use this url as the location where you will put your APK or IPA file. You will need to call the API endpoint as a `PUT` request using a tool like Postman and including the APK or IPA file as the body to the request.

Once you have uploaded the file, you will need to confirm the upload using the  `v2/projects/{projectId}/applications/{appId}/file` endpoint.  Once again fill in the application Id and the Project Id and execute the request

![Confirm the upload](../.gitbook/assets/image%20%28217%29.png)

And with that you have uploaded a new version of your APK or IPA file for testing against in TestProject. As a next step you may find it helpful to script this in you CI using [this blog post ](https://blog.testproject.io/2019/08/27/test-automation-ci-testproject-api/)as an example.



