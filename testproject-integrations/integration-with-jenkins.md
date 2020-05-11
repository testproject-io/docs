# Jenkins Integration

## Installing TestProject Jenkins Plugin

[TestProject’s Jenkins plugin](https://plugins.jenkins.io/testproject) is available in the Jenkins plugin index. In order to install it, login to your Jenkins server. and choose **Manage Jenkins** → **Manage Plugin → Available**. in the filter field type **“TestProject”** and then select the TestProject plugin and hit **Install without Restart**.

That’s it! After a few seconds, the plugin will be installed in your Jenkins server.

![TestProject-Jenkins-1](https://blog.testproject.io/wp-content/uploads/2019/02/Installing-Jenkins-Plugin-1.gif)

## Creating a TestProject API Key

In order to integrate with TestProject, you will need an API key that your Jenkins server will use to trigger your automation jobs.  If you have not yet created a key, you can follow the steps in [getting started with using the TestProject API](../api/getting-started-with-using-the-testproject-api.md). After the new API key has been created, copy it and head back to your Jenkins server.

## Configuring the TestProject Jenkins Plugin

Next you will need to configure the TestProject Jenkins plugin and set the newly created API key. This is a one-time step \(unless you wish to change your key at some point\)

* In Jenkins, choose **Manage Jenkins** → **Configure System.**
* Locate the **TestProject** configuration section, paste your key into the **API Key** field and hit **Save**.

![Install TestProject Addon in Jenkins](https://blog.testproject.io/wp-content/uploads/2019/02/SetAPIKey-Process.gif)

## Running a TestProject Job from Jenkins

After installing the TestProject Jenkins plugin, generating an API key and configuring it to be used by Jenkins, you can start to incorporate your automated tests in the CI process. The plugin supports two of the most popular approaches: Freestyle & Pipeline.

### Get the Project and Job IDs

In order to run a TestProject job remotely, you will need the **Project ID** and the **Job ID** of the job you want to run. These IDs are unique strings and can be found in the TestProject application. To get the Project ID, just navigate to the homepage and copy the ID from the project’s context menu. 

![Project ID](../.gitbook/assets/image%20%28205%29.png)



Similarly you can select the job ID from its context menu.

![Job ID](../.gitbook/assets/image%20%28136%29.png)

### Freestyle Jenkins Projects

In order to set things up for **freestyle** projects in Jenkins, first add a new TestProject Job build step.

![Create TestProject Build in Jenkins](https://blog.testproject.io/wp-content/uploads/2019/02/AddBuildStep.png)

Next, provide the Project and Job IDs that you copied from TestProject into the build parameters. Set the wait time and then save the setting in Jenkins.

![Setup TestProject Build in Jenkins](https://blog.testproject.io/wp-content/uploads/2019/02/SetBuildStepParams.png)

#### The “Wait to finish” Parameter

The **wait** parameter is an optional setting that you can use to determine if the results of the TestProject job will affect the Jenkins job. The valid values are either **0** or else **10 or more** \(the value is in seconds\).

* Setting the value to **0** or omitting the parameter in the pipeline will run the TestProject job without waiting for it to finish. This means that the result of the TestProject job will not affect the result of the Jenkins job.
* Setting the value to **10+** will cause Jenkins to wait for TestProject job to finish within the defined time frame. If the automation doesn't finish running in the defined period or the tests fail, the Jenkins job will be marked failed as well.

### Jenkins Pipeline Projects

For **pipeline** projects use the following syntax to set things up:

`runtpjob jobId: 'YOUR_JOB_ID', projectId: 'YOUR_PROJECT_ID', waitJobFinishSeconds: 1800`

The `waitJobFinishSeconds` parameter is the same as the [wait to finish parameter ](integration-with-jenkins.md#the-wait-to-finish-parameter)above and follows the same rules.

## Reviewing Execution Results

After the execution completes, you will see console entries regarding the execution process. At the end, a direct link to the generated report will be present.

![Jenkins TestProject Output](https://blog.testproject.io/wp-content/uploads/2019/02/ConsoleOutput.png)

TestProject report of the executed job will also reflect the Jenkins CI build information.

![TestProject Jenkins Output](https://blog.testproject.io/wp-content/uploads/2019/02/Report.png)

