# TeamCity Integration

[TestProject](https://testproject.io) plugin for [TeamCity](https://www.jetbrains.com/teamcity) provides an easy way to execute TestProject jobs, update applications, data sources, project parameter, test packages and generate configuration for the TestProject Agent.

## Prerequisites

In order to use this plugin you need to have: 1. An active TestProject account which can be created for free at [https://testproject.io](https://testproject.io). 2. At least one registered and running TestProject Agent.

## How to use

* Install the plugin in your TeamCity server.
* Go to _'Administration'_ > _'Integrations'_ > _'TestProject'_ > set your TestProject API key (which can be obtained [here](https://app.testproject.io/#/developers/api)).&#x20;
* Create a new build step and select _'TestProject'_ in the _'Runner type'_ dropdown.
* Now, simply select the action that you want to perform in TestProject.
* Here's how you can get the ID of your project, job, agent, etc:

Project id:

![Copy ID](https://storage-static.testproject.io/teamcity/project-id.png)

Job id:

![Copy ID](https://storage-static.testproject.io/teamcity/job-id.png)

Test package id:

![Copy ID](https://storage-static.testproject.io/teamcity/test-package-id.png)

Project parameter id:

![Copy ID](https://storage-static.testproject.io/teamcity/project-parameter-id.png)

Agent id:

![Copy ID](https://storage-static.testproject.io/teamcity/agent-id.png)

Data source id:

![Copy ID](https://storage-static.testproject.io/teamcity/data-source-id.png)

Application id:

![Copy ID](https://storage-static.testproject.io/teamcity/app-id.png)

## Build Steps

### Running a TestProject Job

Using this step, you can trigger TestProject jobs as part of your TeamCity test build. To trigger a job, you need to provide the following parameters:

* `Project Id` - The ID of the project containing the job.
* `Job Id` - The ID of the job to execute.
* `Agent Id` _(optional)_ - The ID of the TestProject agent that will execute the job. Leave this field empty to use the default agent defined for this job.
* `Wait to finish` - How many seconds should the step wait for the automation job to finish. If **0** is provided, the setup will not wait for the job to finish execution.
* `Path to the JUnit XML report` _(optional)_ - Path (including the file name) to a file where the JUnit XML report will be stored. The file path can be absolute or relative to your workspace.
*   `Execution Parameters` _(optional)_ - A JSON object that allows you to override the job's default settings and parameters for a single execution. Here's an example:

    ```javascript
    {
    "browsers": [
      "Chrome"
    ],
    "devices": [
      "AAA111BBB"
    ],
    "queue": true,
    "restartDriver": true,
    "projectParameters": {
      "ProjectParameter1": "Value1",
      "ProjectParameter2": "Value2",
      "ProjectParameter3": "Value3"
    },
    "testParameters": [
      {
        "testId": "string",
        "testPosition": 0,
        "dataSourceId": "string",
        "reinstallApp": true,
        "data": [
          {
           "TestParameter1": "Value1",
            "TestParameter2": "Value2",
            "TestParameter3": "Value3"
          }
        ]
      }
    ]
    }
    ```

**Please visit **[**our API documentation**](https://api.testproject.io/docs/v2/#/Jobs/Jobs\_RunJobAsync)** to read more about using execution parameters when running a job.**

#### Example

![Copy ID](https://storage-static.testproject.io/teamcity/run-job.png)

### Updating a Mobile Application (apk/ipa) File

Using this step, you can update an existing Android or iOS application file as part of your build.\
&#x20;The step accepts the following parameters:

* `Project Id` - The ID of the project containing the application.
* `Application Id` - The ID of the application to update.
* `Path to the .apk/.ipa File` - The path to `apk/ipa` file. The file path can be absolute or relative to your workspace.

#### Example

![Copy ID](https://storage-static.testproject.io/teamcity/update-mobile-app.png)

### Updating a Web Application URL

Using this step, you can update the URL of a web application.\
&#x20;The step accepts the following parameters:

* `Project Id` - The ID of the project containing the application.
* `Application Id` - The ID of the application to update.
* `Application URL` - The new URL address.

#### Example

![Copy ID](https://storage-static.testproject.io/teamcity/update-web-app.png)

### Updating a Data Source

Using this step, you can update an existing data source file (`.csv`).\
&#x20;This step accepts the following parameters:

* `Project Id` - The ID of the project containing the data source.
* `Data Source Id` - The ID of the data source to update.
* `Path to the .csv File` - The path to the data source (`.csv`) file. The file path can be absolute or relative to your workspace.

#### Example

![Copy ID](https://storage-static.testproject.io/teamcity/update-datasource.png)

### Updating a Project Parameter

Using this step, you can update the value of any project parameter in your project.\
&#x20;The step accepts the following parameters:

* `Project Id` - The ID of the project containing the parameter.
* `Parameter Id` - The ID of the parameter to update.
* `Value` - The new value that should be assigned to the parameter.

#### Example

![Copy ID](https://storage-static.testproject.io/teamcity/update-project-parameter.png)

### Updating a Test Package

Using this step, you can update an existing test package (coded test) in your project.\
&#x20;The step accepts the following parameters:

* `Project Id` - The ID of the project containing the test package.
* `Test Package Id` - The ID of the test package to update.
* `Path to the .jar/.dll/.zip File` - The path to the new test package file (`.jar`/`.dll`/`.zip`). The file path can be absolute or relative to your workspace.
*   `Resolve Conflicts` \[true/false] - Should TestProject try to automatically resolve conflicts?\


    A conflict may arise if the updated test package is used by other tests or the new packages contains breaking changes such as removed test cases, etc.

#### Example

![Copy ID](https://storage-static.testproject.io/teamcity/update-test-package.png)

### Generating TestProject Agent Configuration

Using this step, you can generate configuration for a TestProject Agent.\
&#x20;This can be used to allow a TestProject Agent running in a docker container to automatically register, execute a job and terminate on completion.\


This step accepts the following parameters:

* `Job Id` _(optional)_ - The ID of the job to execute.
*   `Agent Alias` _(optional)_ - An alias (name) for the agent.\


    > This parameter is optional. If no value is provided, TestProject will generate an alias for you.
* `Temp Agent` _(optional)_ - A temp agent will be deleted from the account once it shuts down.
*   `Execution Parameters` _(optional)_ - A JSON object containing job execution parameters.

    > This parameter is optional. If no value is provided, the job will be executed with its default configuration.\
    >
    >
    > ```javascript
    > {
    >    "browsers": [
    >        "ChromeHeadless",
    >        "FirefoxHeadless"
    >    ]
    > }
    > ```

The agent configuration will be stored automatically in your workspace. You can find the full path in the build logs. \
&#x20;You can also save the agent configuration token in an environment variable and use it later whenever you need. To store it in an environment variable, create new parameter (it should be of type _'Environment Variable'_) in your build and name it `env.AGENT_CONFIG`.

**Please visit **[**our docker hub page**](https://hub.docker.com/r/testproject/agent)** to read more about TestProject Agents containers**

#### Example

![Copy ID](https://storage-static.testproject.io/teamcity/agent-configuration.png)

## Additional info

WebSite: [https://testproject.io](https://testproject.io)

Blog: [https://blog.testproject.io](https://blog.testproject.io)

Forum: [https://forum.testproject.io](https://forum.testproject.io)

Addons: [https://addons.testproject.io](https://addons.testproject.io)

Docker Hub: [https://hub.docker.com/r/testproject/agent](https://hub.docker.com/r/testproject/agent)

YouTube: [https://www.youtube.com/channel/UCEAPPxNvHT74Xj6Ixt28mNw](https://www.youtube.com/channel/UCEAPPxNvHT74Xj6Ixt28mNw)
