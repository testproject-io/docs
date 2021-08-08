# Hybrid Cloud and Offline Mode

TestProject provides you with maximum flexibility for running your test in the way that fits your needs and use case. For many users, our **Hybrid Cloud** offering will make for an easy and simple setup with seamless collaboration by default along with automatic deployment.  Other users might need ways to create and run tests that do not reside in an external cloud provider. In that case, TestProject provides an **offline mode** that will enable local on-premise test executions that leave no footprint in the cloud. 

Whatever your needs, TestProject has a way to meet them, and best of all it is free to get started with either approach. 

## What is the Hybrid Cloud?

With the hybrid cloud approach, test artifacts and reports on them will be stored in TestProject's safe and secure cloud environment. However, the recording and execution of the tests themselves happen locally with the [TestProject Agent](../../testproject-agents/what-is-a-testproject-agent.md). 

You can use the TestProject recorder to create your tests and it will use the local agent to record the tests in a cached browser on your own local machine. You can then run your tests from within the TestProject platform which will once again utilize the local agent. Those locally executed results are seamlessly integrated with the cloud repository giving you instant insights into test runs. 

As you can imagine, this hybrid approach gives you the best of both worlds and allows you to have effortless test setup without needing to worry about keeping different driver versions up to date or orchestrating your test runs. It also gives you access to a lot of great features. For example, you can create tests with the[ AI-powered online test recorder](../create-a-test-step/#smart-recorder). You can also easily collaborate with team members across your company with the powerful [sharing](../collaboration-and-sharing.md) features.  You also have access to [test reports](../../testproject-sdk/opensdk-v2/java-sdk/reports.md) and dashboards along with the ability to do remote test execution on platforms like [Sauce Labs](../../testproject-integrations/sauce-labs-integration/) and [BrowserStack ](../../testproject-integrations/browserstack-integration/)and many other available tool integrations. 

The hybrid cloud approach is highly secured. Data is saved in encrypted parameters and can be stored as “Secret Parameters” that are saved with AES 256 standard for an even further layer of data encryption.

### Getting started with using the Hybrid Cloud

Hybrid cloud is the default way to use TestProject, so you once you have [created your free account](../creating-an-account.md), you can [install and setup the agent ](../installation-and-setup.md)and then [start creating tests](../../using-the-smart-test-recorder/web-testing/creating-a-web-test-using-the-testproject-recorder.md). It really is that easy to get started with using the hybrid cloud. The agent will run locally and seamlessly communicate with the TestProject cloud. 

## What is Offline Mode?

Sometimes though, you might need even more control of your tests using your own private environment. Perhaps your company has strict compliance and security regulations and so you need to test in an environment that is completely disconnected from the internet. In that case you will need to use the offline mode. In this mode, your data will never leave your premise. 

However, that doesn't mean you are left to do all the heavy lifting on your own. In fact, you can still retain much of the power and functionality that you would get in the hybrid cloud mode. You can still create, edit and debug test with TestProject's in-browser recorder. However, instead of saving your test artifacts in the cloud they will be saved locally. You can also debug and summarize test results using local HTML test reports that are automatically created for you.

In addition, you can use the [TestProject Agent Command Line Interface \(CLI\)](../../testproject-agents/testproject-agent-cli.md) to easily execute your tests. The agent CLI will even give you access to the [AI self-healing capabilities](../using-ai-to-improve-testing.md#self-healing) that TestProject has and will also include any addons that your test uses. 

### Getting started with Offline Mode

Creating and running tests in offline mode requires having a local test agent installed. You will need to [download the agent](https://app.testproject.io/#/agents) and copy it onto the computer that will be running the tests. Once you do that you can follow the steps in the section on [installation and setup](../installation-and-setup.md). Of course, don't register the agent if you want to remain offline. 

In order to run the agent offline, you will need to use the agent CLI. This should be available by calling the agent executable, but you will need to make sure that the executable is in your path. You can do this by locating the installed executable location on your computer and ensuring that this location is added to your PATH environment variable. For example, on a windows machine, the agent would be installed to `C:\Program Files\TestProject Agent` by default. The `Program Files` folder should already be in your PATH variable, but if it was not, you would need to add it. Once you are sure that the executable is in your path you can call it by opening a command prompt and typing in the following command:

```bash
testproject-agent.exe help
```

If you are on a Mac or Linux device you can just type:

```bash
testproject-agent help
```

This will print out information about the various commands that are available. You can read more about using the testproject-agent CLI [here](../../testproject-agents/testproject-agent-cli.md).

### Download tests 

If you need to run particular tests in an isolated environment, without access to the TestProject cloud, you can download the tests as either a YAML file or as a complete test package and then copy those files to the isolated environment in order to run the tests there. In order to do that you can use the **Save as File** option on the more menu of a test.

![Save as File](../../.gitbook/assets/image%20%28219%29%20%281%29.png)

You can then directly save it, which will save `.yaml` file with the test information. For basic tests this is fine, but if you have a more complex test \(for example, one using addons\) you can choose to download it as a "Test Package" which will include all dependencies required for running in an offline environment. 

![Save as File Options](../../.gitbook/assets/image%20%28227%29.png)

Once you have downloaded the files, you can easily run them by navigating to the folder where the saved files are and then executing the following command:

```bash
testproject-agent.exe run <name of downloaded file>
```

This will run the file using your local agent without any connection to the cloud. 

### Viewing Test Results

Once the test execution has completed, you can view a local HTML report of the test results. You should see something like this in the command prompt showing you where to find the report files. 

![Report Path](../../.gitbook/assets/image%20%28244%29.png)

If you go to the file location indicated in the report path and open the `.html` file from there, you will see a report summarizing the results of the test run.

![Local Test Report](../../.gitbook/assets/image%20%28105%29.png)

And there you have it. Without any connection to the cloud, you are able to run and report on test results on a local machine. If you want to dig a little deeper into how you can work with TestProject in offline mode, you can read about how to use the TestProject CLI [here ](../../testproject-agents/testproject-agent-cli.md)or you can read more about how local test files work [here](understanding-test-files.md).

