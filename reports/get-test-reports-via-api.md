# Get Test Reports via API

TestProject provides a number of powerful built in reports that can help you figure out test failures and summarize test run information for stakeholders. TestProject also provides an API that gives you access to much of the built in functionality. If you are running your tests in a CI build you can use the TestProject APIs to control what is going on. 

Let's take a look at how you could get a report of test results using the TestProject API.

## Getting Ready to use the API

In order to use the TestProject API, you will need to provide an authorization key. You can follow the steps in [Getting Started with Using the TestProject API](../api/getting-started-with-using-the-testproject-api.md) to generate your API key and get setup to use the API.

## Get a Job Execution Report

With everything setup and ready to go, let's take a look at making an API call to get a report. On the [TestProject API page](https://api.testproject.io/docs/v2/) you can scroll down to the reports section and click on the first endpoint to see the details for the Get Job Reports API call. The API documentation has a handy Try it out button that you can click on to try out some API calls directly in the documentation page. Click on that button now.

![Try it out Button](../.gitbook/assets/image%20%28226%29.png)

You will now need to fill in the test parameters. The `projectId` and `jobId` parameters are path parameters and so are required. You can also see some other optional query parameters that will let you filter the results that get returned. For now we will just look at making a simple call without any query parameters so let's get the `projectId` and `jobId`

In order to get the `porjectId` we can go to the home page of the TestProject app and click on the more menu of the project we are interested in. You can then use the Copy ID option to copy the project ID for the project.

![Copy Project ID](../.gitbook/assets/image%20%28113%29.png)

Go back to the API documentation page and paste that value into the `projectId` field. You will also need the `jobId` which can be found in a similar way.  On the project details page of the project you are using, you can see the jobs that you have setup for the project in the right hand panel. If you have not yet created any jobs for this project you will want to do so \(and then run the job at least once\).  To get the job ID click on the more menu on the job and select the Copy ID option

![Copy Job ID](../.gitbook/assets/image%20%28128%29.png)

Paste this value into the `jobID` field of the API call. Now that you have both the job and project IDs you can execute the test. When you do that you should see something like this

![API Response](../.gitbook/assets/image%20%28157%29.png)

## Automate Job Execution Reporting

We have seen how you can manually create a test report in the TestProject API documentation page, but the real power of API calls is in the ability to integrate into CI builds or other forms of automation. Thankfully TestProject API calls can be used outside of the documentation page. 

The response in the documentation page even gives you the curl command that you can use to call this. If you have curl installed you can just copy that command and run it at the command line to do the exact same thing as it does in the documentation tool. 

You are also given the full composed request url which you can use along with your authorization key in the header of the call to create an API call in any tool or coding language that support them. For example if you were automating you CI pipeline with python you could get the latest job execution report by doing something like this:

```text
import requests

url = 'https://api.testproject.io/v2/projects/{projectId}/jobs/{jobId}/reports/latest?details=true&format=TestProject'
headers = {'Authorization':<your auth key>}
response = requests.get(url,headers=headers)
print (response.json()) 
```

If you replace `{projectId}` and `{jobId}` with the project and job IDs that you are interested in, and put in your auth key as you find it on the [API integrations page](https://app.testproject.io/#/integrations/api) you should be able to see the response to your API call printed out. 

This example of course uses python, but the same thing would work with any other scripting language or API execution tool.

## Conclusion

TestProject has many reports available and the TestProject API makes it easy to automate the generation of these reports so that you can see what is going on in any build that you do.



