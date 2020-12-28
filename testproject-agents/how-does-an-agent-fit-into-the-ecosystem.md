# How Does an Agent fit into the Ecosystem?

The TestProject agent and the TestProject app work seamless together to give the flexibility of using and controlling your own devices while providing a cloud based way to share an collaborate on effective test case management. The TestProject ecosystem can be summarized with the below diagram.

![TestProject Ecosystem](../.gitbook/assets/image%20%28112%29.png)

As the diagram illustrates, local agents enable the recording of new tests and the running of existing tests. When creating a new test with the test recorder, you will specify a local agent to use and that agent will manage all the drivers and other details that are needed to enable seamless test recording. In the same manner, when running tests you will choose the local agent\(s\) to run them on and those agents take care of all the details of running those tests including using any connected mobile devices.

## Local Agent

In order to use TestProject you need a local agent. You can install that agent directly onto your computer or you can install it with [Docker](testproject-agent-in-docker.md), or in you [CI builds](../testproject-integrations/integration-with-teamcity.md). The local agent takes care of a lot of background work for you. It pulls together several different testing libraries into one seemless experience. Without TestProject, the tester that want to have thorough test coverage would need to install multiple systems \(Selenium and Appium\) and then drivers for each browser as well. The diagram below helps to summarize some of ability of the TestProject agent.

![TestProject Local Agent](../.gitbook/assets/image%20%28194%29.png)

Actions like recording or running tests are sent from the TestProject Application to the local agent. The agent will then call appium if you running a test on a connected mobile device, or selenium if you are running on a web browser. These systems use webdrive to control the underlying actions and so TestProject will check that you have the correct version of webdrive available for whichever platform you are testing with. If the version is out of date, TestProject will automatically find and install the correct version. 

As the local agent performs the actions it send data back to the TestProject application, letting it know what has happened. Local agents can be installed on Window, Linux and MacOS including through Docker images. With TestProject, gone are the days of needing to keep Webdriver, Selenium, and Appium versions all in sync with each other for multiple browsers and devices. One simple install takes care of it all. 

The local agent also has it's own API that you can use to do things like check on the status, download the logs and a number of other things. You can see the local agent API documentation by going to [http://localhost:8585/swagger/](http://localhost:8585/swagger/) if the agent is running. 



