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
* **Ephemeral Instances & Jenkins** - In this scenario the agent is started up in order to perform a specific task, and will self terminate upon completion of said task.

The operation mode of the agent is controlled by environment variables that are passed to the container upon creation.  


### Permanent Execution Engine

Let’s say you want to run multiple jobs & don’t want a fresh container for each test run. Your test capitalizes on a cache previously saved from a test run to continue further execution. Running tests from the start is a bit of an overkill even when using containers. 

This is where instances that have saved states come in. The flexibility to resume or carry on jobs with the ability to save data can become crucial for any testing environment as the testing phase matures. The Docker agent of TestProject comes with this feature built in. You can easily start images that run for indefinite times & you can save the data with the help of attached volumes in case a running container fails. To get started aforementioned we need the TP\_API\_KEY to grant access to the project & an TP\_AGENT\_ALIAS to set a custom name for the agent. When starting an instance with these variables the agent is automatically registered to the account.This name can be referred to if you want to view the agent in your account. 

![](https://lh4.googleusercontent.com/nS0AIQm-_PXV_qvrr3OScoTFAwEQj6v8prQOYnPdfLTPy7Ipy6_a76D7XTQG-cnlVZNgFM_RT9M3ARSw2ZSju2VXkQ04Q0zzgKF0zgoKASv3G4WtV6W81gCK3LLgn30ukl3og11c)

  
**You can also set up manual registration of the agent from the Web UI by mapping the containers port 8585 to 8585 TCP port on the host. A volume can also be set up to store the images data. Here’s how a sample command looks like to run the permanent instance with an attached volume :**   


![](https://lh3.googleusercontent.com/zgESmU87hnOfci-OqsAcDVdfCdnarJ61QDCCwDlVCBIuIcJG_nLmNBXzyb8asCPTDMOxuGl8w_YKu4a1kZHMyRiI9fZYjaIEen1n-Pp5NgUNdMzGCH_wxMzG-Y0FCiI6GJ-VWLH3)

