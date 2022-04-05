---
description: Brief explanation of TestProject's docker container.
---

# TestProject Agent on Docker

A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application, starting from  code and system tools to even system libraries and settings.\
\
Containerized software will always run the same, regardless of the infrastructure. Containers isolate software from its environment and ensure that it works uniformly.\
\
The TestProject Agent docker container can be used in **two** distinct ways:\
\
The first one being as a **Permanent Execution Engine** - In this scenario the agent is registered once, and then can be used to execute tests and jobs from the TestProject web application.\
\
The second one being as a **Ephemeral Instance** - In this scenario the agent is started up in order to perform a specific task, and will self terminate upon completion of said task.\
\
The operation mode of the agent is controlled by **environment variables** that are passed to the container upon creation.\
\
For more details and examples please head over to our DockerHub page at:\
[https://hub.docker.com/r/testproject/agent](https://hub.docker.com/r/testproject/agent)
