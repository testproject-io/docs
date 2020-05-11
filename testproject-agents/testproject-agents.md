---
description: Leverage TestProject Agents to run in Docker containers and setup virtual labs
---

# Setup TestProject Agents in Docker

## What is Docker?

[Docker](https://www.docker.com/) is the de-facto standard to build, run and share containerized apps from your desktop to the cloud. A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.

## Why do I need TestProject Agents inside Docker containers?

Containers are a perfect companion to the agile movement. Organizations today need fast paced & efficient software teams & with that comes the hefty practice of continuous pushing of source code from development to testing & production multiple times. With Docker’s ability to isolate environments with specific dependencies & the flexibility to ship them from or to different environments makes the work more efficient & reliable. 

Docker containers can accelerate your test automation platform using "dockerized" TestProject Agents. What makes the docker agent useful is that it saves a bunch of resources & provides the ability to run tests with just a simple command. For most cases you’ll need to set up the TP\_API\_KEY from the web console which is a way of authorizing the docker agent to an account. Optionally, you’ll need a Job id TP\_JOB\_ID if you want the containers to execute directly instead of waiting for instructions from the web UI.

You can set up the agent in two ways:

* Giving signals to execute jobs right from the web UI. 
* Or providing dedicated tokens beforehand for seamless execution of jobs without the need for manual intervention. 

## Setting up TestProject Agents in Docker

### Requirements

* All you need is a [TestProject](https://testproject.io/) account, that's it! If you don't already have one, you can [sign up](https://app.testproject.io/signup/) and open your free account [here](https://app.testproject.io/signup/).

The TestProject Agent docker container can be used in two distinct ways, as also described in our [DockerHub](https://hub.docker.com/r/testproject/agent) page:

* **Permanent Execution Engine** - The agent is registered once, and then can be used to execute tests and jobs from the TestProject web application
* **Ephemeral Instances** - In this scenario the agent is started up in order to perform a specific task, and will self terminate upon completion of said task.

The operation mode of the agent is controlled by environment variables that are passed to the container upon creation.

### Permanent Execution Engine

Let’s say you want to run multiple jobs & don’t want a fresh container for each test run. Your test capitalizes on a cache previously saved from a test run to continue further execution. Running tests from the start is a bit of an overkill even when using containers. 

This is where instances that have saved states come in to the picture. 

The flexibility to resume or carry on jobs with the ability to save data can become crucial for any testing environment as the testing phase matures. 

The Docker agent of TestProject comes with this feature built in. You can easily start images that run for indefinite time & you can save the data with the help of attached volumes in case a running container fails. To get started aforementioned we need the TP\_API\_KEY to grant access to the project & an TP\_AGENT\_ALIAS to set a custom name for the agent. 

When starting an instance with these variables, the agent is automatically registered to the account. This name can be referred to if you want to view the agent in your account. 

![TestProject Agents](https://lh4.googleusercontent.com/nS0AIQm-_PXV_qvrr3OScoTFAwEQj6v8prQOYnPdfLTPy7Ipy6_a76D7XTQG-cnlVZNgFM_RT9M3ARSw2ZSju2VXkQ04Q0zzgKF0zgoKASv3G4WtV6W81gCK3LLgn30ukl3og11c)

You can also set up manual registration of the agent from the Web UI by mapping the containers port 8585 to 8585 TCP port on the host. A volume can also be set up to store the images data. Here’s how a sample command looks like to run the permanent instance with an attached volume: 

```text
docker run --name testproject-agent \
    -e TP_API_KEY="REPLACE_WITH_YOUR_KEY" \
    -e TP_AGENT_ALIAS="My First Agent" \
    -v </path/to/host/folder>:/var/testproject/agent \
    testproject/agent:latest
```

Attaching a volume also enables seamless updates for the TestProject Agents.

In its current state, the agent is idle & is waiting for a job to run. Let’s bring the container into action by sending it the job signal using [TestProject’s Jenkins plugin](https://plugins.jenkins.io/testproject/). The plugin is available for installation from: Manage Jenkins &gt; Manage Plugins:

![](https://lh5.googleusercontent.com/zBNLHqylqfULHUgabxV4_tTZxKUbyxgYrTxQhkhKLf5HRUWndjdYcArb4OC40yFuSRaKt_BeG54rZICxr8C5rbq2jhE4P4rmOCAnBdLLraXL_Yn_OGoCdmLtF2xsfpluZ4HV0Ew1)

Using the API\_KEY, you can link the plugin to your TestProject account seamlessly. All you need to do is to navigate to Manage Jenkins &gt; Configure System & scroll down to **TestProject Global Configuration**, enter the APi\_KEY & you’re good to go!

![](https://lh5.googleusercontent.com/6kK_uCaMT5ith0jvnz-0hcno44N1uQssrzFuGNJ1_UWiuIRHbb_CETEgBDMDVIjo4UaYBrttbLJ61-daEtPd64A9CGZn0AN0A_3XWxzMIGSjxSneN8V0bE2w2SfmLEHKA7tjCwGN)

Create a Freestyle project under the build section and add a build step with **Run TestProject Job** selected. The Id’s can be found from the TestProject’s web console.  

![](https://lh4.googleusercontent.com/SQPqF9PLGmJJ26PIf-JpYjvc3vwdsRJ4lERpgFWGHIMqmkwiA810G8GBhqc4qBmRqpNfzpUSJvEEs5yc2e1Z70pqe7rPHFtO8D18ODFPixjWsb1MO8g-1TFYZvvqjf_WR5K2mwql)

### **Ephemeral Instances**

In order to have test environments that resemble production environments we can either configure it at the source code level, or have tests run on actual servers with the dependencies like db etc. installed.

The story at the source code level brings unwanted configurations to the code**,** making it hard to maintain with newer updates & bug fixes. However, running it on an actual hardware is also a burnout as stuff can get overwhelmed pretty quick & comes with a lot of setup and maintenance overheads. In addition, since resources are shared among tests we can only run them one at a time to ensure they don’t interfere with each other’s executions.

```text
version: "3.1"
Services:
  Testproject-agent:
    image: testproject/agent:latest
    container_name: testproject-agent3
    Depends_on:
      - chrome
      - firefox
    Environment:
      TP_API_KEY: <your_api_key>
      TP_AGENT_ALIAS: "Docker Agent"
      TP_JOB_ID: <job_id>
      TP_JOB_PARAMS: '"jobParameters" : { "browsers": [ "chrome", "firefox" ] }'
      CHROME: "chrome:4444"
      FIREFOX: "firefox:4444"
  Chrome:
    image: selenium/standalone-chrome
    Volumes:
      - /dev/shm:/dev/shm
  Firefox:
    image: selenium/standalone-firefox
    Volumes:
      - /dev/shm:/dev/shm
```

Let’s have a look at Docker Compose which enables us to get the best of both worlds. It makes it easier to replicate the parts we have in environments & create them in the form of containerized solutions. We get the freedom to test in a real physical environment. 

The TestProject Agent is responsible for handling the test cases with the given api\_key & job\_id. The Docker compose file also sets up multiple browsers to run the tests on. After running the test it exits so that any cache left is cleared.

Let’s set up a Docker compose file to run from a Jenkins pipeline. With the Docker TestProject Jenkins plugin we can run tests directly from the pipeline enabling a seamless CI set up. Here’s a sample jenkinsfile that pulls & runs a nodejs application initiates the test on the containers via the TestProject plugin & cleans up in the end:

```text
pipeline {
   agent any

   stages {
      stage('Build') {
         steps {
            // Get some code from a GitHub repository
            git 'https://github.com/collabnix/testapp.git'
           
         }

      }
      stage('Run') {
	 steps {

	    sh "node index.js &"

	 }
      }
      stage('Test') {
	 steps {
	    tpJobRun agentId: 'ph3CXXXXXXXX', jobId: 'o7wS4nXXXXXXX', projectId: 'DzkGyzxkMXXXXXXXX', waitJobFinishSeconds: 180
	    
	    sh "killall -9 node"

	 }
      }
   }
}
```

## Troubleshooting

In case of a permanent execution engine scenario, one should ensure that their active account is linked & registered. You can verify registered agents & their status from the top Navigation Bar under the Agents tab.

![](https://lh3.googleusercontent.com/1JrQNZsAz9ygXOvTVyoMAYhT3ZF0nrxJcEuOSf--j91qcYqRAb5SyAuj14u5PFy8n4fNCyTd2opstDv8WW8kINm833-XM1toPpwQnfmWu4B-_t0NVLHtQnMVlxQenkC8SBqnBmq8)

## **Conclusion**

The containerized version of the TestProject Agent takes testing to the next level by eliminating the need to set up entire servers for testing & provides the flexibility to create temporary & permanent instances for automated testing.

![](../.gitbook/assets/image%20%2827%29.png)

