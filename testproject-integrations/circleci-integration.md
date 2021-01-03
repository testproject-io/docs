---
description: >-
  In this guide you will know how to Integrate your recorded/coded tests using
  CircleCI Pipelines
---

# CircleCI Integration

## **Background:**

This tutorial explains how to integrate TestProject with CircleCI CI/CD pipeline with the following scenarios

1. Running TestProject recorded tests with CircleCI CI/CD Pipelines
2. Running TestProject coded python tests with CircleCI CI/CD Pipelines
3. Running TestProject coded Java tests with CircleCI CI/CD Pipelines

## **Running TestProject recorded tests with CircleCI CI/CD Pipelines**

Today’s development cycles include fast releases and require agile testing methods, developers and testers need to collaborate to release tested features faster. Integration of test automation within the software CI/CD plays a significant with agile development cycle and better software to be released to production faster.

TestProject cloud offers seamless integration with any CI/CD flow by using its Restful API which allows performing numerous operations, as well as execute Tests on-premise and on remote agents, both ad hoc and permanent agents,.

Below is a diagram that explains high-level TestProject architecture and the prerequisites needed for CI/CD :

![](../.gitbook/assets/0.jpeg)

**Getting Started With TestProject API:**

1. You need to create an API Key from here: [https://app.testproject.io/\#/integrations/api](https://app.testproject.io/#/integrations/api)
2. Generate your API key: [here](https://app.testproject.io/#/integrations/api), and copy it.
3. Go to the API documentation: [here](https://api.testproject.io/docs/v2/#/)
4. Click on the Authorize button and paste your API key and click on Authorize.

![](../.gitbook/assets/1%20%286%29.png)

By using TestProject Restful API, we will create a curl command that will execute the desired recorded tests using a CURL command in the Pipeline.

**Generating the Curl Command**

In the API Swagger, we will scroll down to the Endpoint we wish, in this example we will use the **Run Job Endpoint** which can be found [here](https://api.testproject.io/docs/v2/#/Tests/Tests_RunTestAsync).

With this Endpoint, we can execute a Test on any registered agent in the account associated with our API key.

All values that are passed in the body of this request will override the **DEFAULT** job values

In this example, we will run a Recorded Web test on Chrome using the Run Job endpoint.

**Setting up the Endpoint:**

**In the “Run” Job endpoint, click on ‘Try It Out’**

![](../.gitbook/assets/2%20%286%29.png)

We will insert the Project ID:

![](../.gitbook/assets/3%20%286%29.png)

And the Job ID:

![](../.gitbook/assets/4%20%286%29.png)

Next, we can edit the body of the request, here we can insert values that will override the default job values on runtime.

To just run the Job as is, with the default values, you can just keep the body empty like so:

![](../.gitbook/assets/5%20%286%29.png)

In our example we will edit the values of the body to override default values from the Job.

We will override the default params **username** and **password** in the test with custom values.

The job will have two tests, both have two parameters in them called **username** and **password**.

We will override those parameters on runtime using the **testParameters** JSON which we pass in the **body** of the request.

This is how the parameters are defined in the tests:

![](../.gitbook/assets/6%20%285%29.png)

**This is how we override them using the request body**:

![](../.gitbook/assets/7%20%285%29.png)

We will now generate the CURL command by pressing Execute:

![](../.gitbook/assets/8%20%284%29.png)

And we will see the CURL command generated:

![](../.gitbook/assets/9%20%284%29.png)

This is the curl command we will be used in our pipeline.

Now we can set up our pipeline using the above command to execute the Job every time we push a new change to the defined branch.

**Setting up the Pipeline in CircleCI on a Permanent Agent**

1. In your Dashboard, add a Project, this will be the project which will have the pipeline, once we push a new change to this project, we will execute the pipeline.

![](../.gitbook/assets/10%20%282%29.png)

1. Select the project

![](../.gitbook/assets/11%20%282%29.png)

1. In the following window, we will have the options to choose pre-configured YAML files for our pipeline, in this example, I will select the Python file since the project is in python.
2. Paste the curl command in the proper step.

 ![](../.gitbook/assets/12%20%282%29.png)

   3. Click on **Commit and Run** to configure the pipeline in the selected branch

Now every time we push a change to the selected branch, the Pipeline will trigger the Curl command which in the following will trigger the tests.

**Complete example of a pipeline config.yml**

```text
version: 2.1
orbs:
  python: circleci/python@0.2.1
jobs:
  build-env:
    executor: python/default
    steps:
      - checkout
  run-recorded-tests:
    executor: python/default
    steps:
     - run:
          command: curl -X POST "Request URL"  -H "accept:application/json"  -H "Authorization:YOUR API KEY" -H "Content-Type:application/json" -d "{'testParameters': [{'data': [{'username': 'TestProject','passowrd': '12345'}]}]}"
          name: Run Test On Build
workflows:
  main:
    jobs:
      - build-env
      - run-recorded-tests
```

You can view the pipeline execution in the Dashboard:

![](../.gitbook/assets/13%20%282%29.png)

**Running TestProject recorded tests with CircleCI CI/CD Pipelines using Docker Ephemeral Agent**

In the previous example, we saw how to execute tests on a permanent agent by supplying a Job ID and API key. This example will explain how to execute Web tests on Docker agents, which will allow you to spin up agents on demand. We will utilize docker compose to create agents on the fly for a specific job to run and terminate them afterward.

It will also allow you to execute multiple tests in Parallel within your pipeline.

Below is a diagram on the flow of the process:

![](../.gitbook/assets/14.jpeg)

First, we will need to config the correct environment variables.

**Configuring Environment Variables in CircleCI:**

The following config below uses these Environment variables:

![](../.gitbook/assets/15%20%281%29.png)

You can set them in CircleCI Dashboard:

1. Go to project settings:

![](../.gitbook/assets/16%20%281%29.png)

1. Click on Environment Variables:

![](../.gitbook/assets/17.png)

1. Add Environment Variable:

![](../.gitbook/assets/18.png)

**Configuring Docker Compose YML file**

You will need an docker-compose.yml file which will spin up the Docker agent.

In this example we are overriding the **username**/**password** parameters that are used in the tests by using this YAML file:

```text
version: "3.1"
services:
  testproject-agent:
    image: testproject/agent:latest
    container_name: testproject-agent
    depends_on:
      - chrome
      - firefox
    environment:
      TP_API_KEY: $TP_API_KEY
      TP_JOB_ID: $TP_JOB_ID
      TP_JOB_PARAMS: '"jobParameters" : {"browsers": [ "chrome", "firefox" ],  "testParameters": [{"data": [{"username":"TestProject", "password":"12345"}]}]}'
      CHROME: "chrome:4444"
      FIREFOX: "firefox:4444"
    ports:
    - "8888:8589"
  chrome:
    image: selenium/standalone-chrome
    volumes:
      - /dev/shm:/dev/shm
  firefox:
    image: selenium/standalone-firefox
    volumes:
      - /dev/shm:/dev/shm
```

Using the above compose file, we will spin a docker agent which will execute the Job stated in $**TP\_JOB\_ID**.

The variable **TP\_JOB\_PARAMS** holds the JSON which holds the username and password parameters that will be overridden in runtime.

Using [this](https://github.com/Rantzur1992/recorded_example/blob/main/.circleci/config.yml) config in the pipeline to execute the Job on the Docker agent.

You can read more on TestProject Docker agent [here](https://hub.docker.com/r/testproject/agent).

## **Running TestProject coded Python tests with CircleCI CI/CD Pipelines**

Using TestProject Python SDK, you can seamlessly integrate existing/new Python code to your Pipeline.

With a simple process, you will be able to run your tests with every new change that is pushed and enjoy Cloud and Local reports directly to your TestProject account.

Below is a diagram on the flow of the process:

![](../.gitbook/assets/19.jpeg)

Before integrating your coded tests with CircleCI, we need to make sure you are using our Python SDK.

1. Navigate to [https://app.testproject.io/\#/integrations/sdk](https://app.testproject.io/#/integrations/sdk)
2. Download the Python SDK using **pip3 install testproject-python-sdk**
3. Copy the Developer Token, which we can later use in our Python code.
4. You can read more in the Python SDK repository: [https://github.com/testproject-io/python-sdk](https://github.com/testproject-io/python-sdk)

Once we have set up our code, we can integrate our coded python test using CircleCI.

In CircleCI, open a new project like shown previously, and select the Project for your coded test.

Like previously, we will select a pre-configured Python yml file, and configure it to run our Tests.

Here is a complete example of a config.yml which does the following:

1. Creates a clean ubuntu 20.04 environment.
2. Spins up docker container using docker-compose from a public example’s repo from TestProject.
3. Runs the Example python tests on the Docker Agent.

**Note: When using Docker Agent on CircleCI, you must use Machine config and Not Docker Executor.**

**Config.yml:**

```text
version: 2.1
orbs:
  python: circleci/python@0.2.1
jobs:
  build-compose-run-test:
    machine:
      image: ubuntu-2004:202010-01
    working_directory: testproject
    steps:
      - run:
          name: Update And Install Dependancies
          command: |
            sudo apt-get -y update
            sudo apt-get install -y curl wget git
            git clone https://github.com/Rantzur1992/python_example.git
            python3 --version
      - run:
          name: Start Docker Agent
          command: |
            cd python_example
            set -x
            docker-compose up -d
            pip3 install testproject-python-sdk
      - run:
          name: Run Tests
          command: |
            sleep 20
            cd python_example
            python3 python_example.py
workflows:
  main:
    jobs:
      - build-compose-run-test
```

The following config above uses this Environment variables:

![](../.gitbook/assets/20.png)

You can set them in CircleCI Dashboard:

1. Go to project settings:

![](../.gitbook/assets/21.png)

1. Click on Environment Variables:

![](../.gitbook/assets/22.png)

1. Add Environment Variable:

![](../.gitbook/assets/23.png)

Now you are good to go running your Python Coded tests using TestProject SDK in your pipeline.

![](../.gitbook/assets/24.png)

## **Running TestProject coded Java tests with CircleCI CI/CD Pipelines**

Integrating your Coded Java tests is very similar to Integrating Python tests like shown above.

You need the save Environment variables, just need to change the config.yml to work with your Java environment.

We will use Gradle in this example.

First, we set up our **build.gradle** to point to the classes which hold our tests.

In this simple example, we will use one class called JavaExample which holds the main method.

In the **build.gradle**:

```text
application {
 mainClassName = "JavaExample" //This points to your entry point class
}

plugins {
 id 'java'
 id 'application'
}

dependencies {
 testCompile group: 'junit', name: 'junit', version: '4.12'
 implementation 'io.testproject:java-sdk:0.65.0-RELEASE' //Use the latest version of the SDK
}
```

In our config we will use Gradle to run that main method.

Example of **build.gradle**\(Also visible in the Git Repository\):

```text
plugins {
 id 'java'
 id 'application'
}

group 'org.example'
version '1.0-SNAPSHOT'

repositories {
 mavenCentral()
}

application {
 mainClassName = "JavaExample"
}

dependencies {
 testCompile group: 'junit', name: 'junit', version: '4.12'
 implementation 'io.testproject:java-sdk:0.65.0-RELEASE'
}
```

**The config.yml**:

```text
version: 2
jobs:
 build:
 machine:
  image: ubuntu-2004:202010-01
 working_directory: ~/testproject
 steps:
  - run:
    name: Update Dependancies And Install Java 11
    command: |
      sudo apt-get -y update
      sudo apt install -y openjdk-11-jdk wget git
      java -version
 - run:
    name: Download And Install Gradle
    command: |
      VERSION=6.5.1
      wget https://services.gradle.org/distributions/gradle-${VERSION}-bin.zip -P /tmp
      sudo unzip -d /opt/gradle /tmp/gradle-${VERSION}-bin.zip
      export GRADLE_HOME=/opt/gradle/latest
      export PATH=${GRADLE_HOME}/bin:${PATH}
      gradle -v
 - run:
   name: Clone Code Repo
   command: |
     git clone https://github.com/Rantzur1992/java_example.git
 - run:
   name: Start Docker Agent
   command: |
     cd java_example
     set -x
     docker-compose up -d
     sleep 10
 # run tests
 - run:
   name: Run Test
   command: |
     cd java_example
     gradle run
```

This pipeline will install **JDK 11** which is required by the TestProject SDK, install Gradle, Start the docker agent, and execute the test.

![](../.gitbook/assets/25.png)

**Summary Diagram**

For summary, the following diagram shows the flow from development to automation execution from TestProject:

![](../.gitbook/assets/26.jpeg)

## **View Execution Reports**

After execution we can view the Reports in the Reports page.

In your TestProject account click on **Reports**

![](../.gitbook/assets/27.png)

Here we can see all of our Execution reports, find the Job

![](../.gitbook/assets/28.png)

Expanding it will show all previous execution under that Job.

![](../.gitbook/assets/29.png)

We can also download the PDF reports to see the full detailed report with screenshots.

**All examples can be found on our** [**GitHub**](https://github.com/testproject-io)**.**

