# Calling REST APIs in a Test

Many web application provide RESTful APIs that you can interact with. These APIs can be a powerful way for testers to interact with the applications. TestProject has a [RESTful API Client Addon](../../testproject-addons/available-addons/restful-api-client-addon.md) that allows you to leverage the power of REST APIs directly in your tests.  You can seamlessly integrate API calls and UI calls into one test to enhance the power and flexibility of your tests.

## REST API Example

In order to better understand the power of the RESTful API addon let's take a look at an example of how to use it. For this example we will use TestProject's own REST API. This API allows you to interact with certain parts of the TestProject application. In order to use it make sure you have set up an authorization key by following the steps [here](../../api/getting-started-with-using-the-testproject-api.md) in the documentation.

### Test Setup

If you have not yet used TestProject, check out the documentation on [creating your first test](../../using-the-smart-test-recorder/web-testing/creating-a-web-test-using-the-testproject-recorder.md) and setting up a project. Once you have a test in place using the [https://app.testproject.io/](https://app.testproject.io) as the ApplicationURL, you can start recording.  In this example we are going to look at creating and deleting test parameters.

### UI Test Steps

With the TestProject Test Recorder open, click on a project on the home page. This will take you to the poject page and on that page click on the Parameters link in the left-hand navigation column.

![Parameters](<../../.gitbook/assets/image (26).png>)

You can then click on the Add a new Parameter link at the top of the page to create a new parameter.

![Add a new Parameter](<../../.gitbook/assets/image (155).png>)

On the pop-up specify the name, description and value for that parameter and click on create.

### API Test Steps

At this point you should have a test that has a number of tests steps in place that allow you to create a new parameter. Now, let's imagine that you wanted to check something on this parameter to make sure it had been created correctly and then you wanted to clean up the project by deleting it. You could of course do those things directly in the UI, but for this example, let's look at doing it with API call.

The TestProject [API documentation](https://api.testproject.io/docs/v2/) lists a [delete call for project parameters](https://api.testproject.io/docs/v2/#/ProjectParameters/ProjectParameters\_DeleteProjectParameterAsync).  This call can be used to remove a parameter, but we will need to know the `projectId` and the `parameterId`.  We can get the project ID directly from the project we clicked on in the first step with the UI recorder using the Copy ID option on the more menu.

![Copy ID](<../../.gitbook/assets/image (81).png>)

#### GET Call

Now we have the project ID but we still need the parameter ID.  Since the parameter isn't going to be created until the test is run, we can't know it ahead of time, so we will have to find it once the UI test steps have run. The API documentation has a [GET call that will return all the parameters for a project](https://api.testproject.io/docs/v2/#/ProjectParameters/ProjectParameters\_GetProjectParameters).  Let's setup a test step using this GET call.

To do this we can manually add a test step to our test.  We then need to change the Type to action

![Change Test Step Type to Action](<../../.gitbook/assets/image (136).png>)

&#x20;Once we've done that we can search for "API"  and click on the  `HTTP GET Request` action in the search results. To use this action you will need to have installed the [RESTful API Client Addon](../../testproject-addons/available-addons/restful-api-client-addon.md).

The `HTTP GET Request` action takes in a few inputs.  The first thing we need to specify is the endpoint URL.  We will also need to fill in an authorization header with our authorization key and the status that we expect to get back (200 OK) as well as the JsonPath to the part of the call that we are interested in.&#x20;

![Inputs](<../../.gitbook/assets/image (129).png>)

This setup will call the parameters API endpoint for the given project ID. You will of course need to get your own project ID and [authorization key](../../api/getting-started-with-using-the-testproject-api.md#getting-an-api-key). This call send a request to the given endpoint and returns back a response with a list of the parameters for that project which we can parse with the JsonPath expression (`$[0]['id']`). In this case we are assuming that there is only one parameter (The one you just created) and so we can get the first index  (remember indexes usually start at 0 in computer programming) of the response and the use the `id` key to get the id of that parameter.

We will need to us the parameter ID to delete the parameter so let's save it into an output parameter. In order to do this, click on the select parameter link

![Select Parameter](<../../.gitbook/assets/image (123).png>)

You can then add a new parameter using the little plus at the bottom of the page, and give it a name. Do not fill in the value field for this parameter since the test will automatically fill it in with the result of the Json Path expression. Add this parameter to use it in your test step and save that step.

#### DELETE Call

Now that we have the parameter ID we can use that to delete the parameter. Similarly to the GET call, we can add a new test step, change the step type to action and search for API. We can then click on the `HTTP DELETE Request` action to select it. This action takes in a similar set of inputs as the GET call.

![DELETE Input Parameters](<../../.gitbook/assets/image (38).png>)

In this case we are using the ParamId Parameter that we created as an output parameter in our last test step. We can easily add this to the endpoint url, by clicking on the blue plus button to the right of that field, and then selecting the parameter from the list.

Once everything is input into this test step we can save and close, and we are done!

## Conclusion

Note that this this tutorial is an example. It is setup using the TestProject API so that we can see how to using different calls like GET and DELETE. You should be able to run this test by using the Run option is the TestRecorder, but if you want to actually run this in a job you will need to add tests steps for logging into TestProject since the run time environment for jobs does not include your cookies.

![Running in the Test Recorder](<../../.gitbook/assets/image (160).png>)

API calls can enhance and extend your tests in many ways, and with the RESTful API Client Addon in TestProject it is a simple and straightforward thing to integrate API and UI test steps into one powerful test.
