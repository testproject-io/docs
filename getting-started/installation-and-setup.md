---
description: 'Download, install, start, and register your agent, remote registration.'
---

# Installation and Setup

Once you have [created an account](creating-an-account.md) with TestProject you just need to follow a few simple steps to get setup and ready for testing.  TestProject works on almost any platform, with the install of a single agent.

The first thing you will need to do is login to the TestProject app. Once you have done that you can go to the agents tab at the top of the page and click on the link for the platform you are on to download the agent executable or go to [Agent Download](https://app.testproject.io/#/download). Once that download has finished you can use it to install the TestProject agent on your machine.

After that, there is only one step left. You need to register your agent with the TestProject app so that you can use it to create and run tests. In order to do that, the agent needs to be running on your local machine. You can start it up by finding the installed TestProjectAgent executable on your machine and running that.

## Starting TestProject Agent

### Start the agent on Windows

On Windows, the easiest way to run the agent is just to search for TestProject in the Windows search bar and clicking on the Agent to start it.

![TestProject Agent on Windows](../.gitbook/assets/image%20%2865%29.png)

The agent will then start up on your computer and you will be able to see the status of it by right-clicking on the icon in the system tray.

![TestProject Status in System Tray](../.gitbook/assets/image%20%281%29%20%281%29.png)

### Start the agent on Mac

On Mac, after you have installed the agent, you can run it by finding it in the application folder and double-clicking. This will open it in the dock and you can see the options on it by right clicking 

![TestProject Agent on Mac](../.gitbook/assets/image%20%289%29.png)

### Start the Agent on Linux

First navigate to TestProject app:

```text
cd /home/UserName/testproject/agent/bin
```

{% hint style="info" %}
Don't forget to replace UserName with the actual user
{% endhint %}

Then install the Agent:

1. Right click on that file-&gt; Properties-&gt; Permissions-&gt; check the "**Execute**" option.
2. Open the folder that contains this file on terminal and type:

```text
./TestProject_Agent_3.3.0.sh
```

{% hint style="warning" %}
Make sure to type the correct file name \(agent version may differ\)
{% endhint %}

After installing:

Start the agent in fork mode so you can use the current terminal:

```text
./testproject-agent start -f
```

It should look like this:

![Starting the agent on Linux terminal](../.gitbook/assets/image%20%28402%29.png)

## Register the Agent

### Register via UI

Once you have verified that the agent is running, you can go into the TestProject app and choose the Register an Agent option from the [Agents menu](https://app.testproject.io/#/agents).

![Registering the agent from TestProject app](../.gitbook/assets/image%20%28400%29.png)

You will be prompted to give your agent an alias. Put something meaningful in here like "Joe Smith's Windows laptop" as it is possible to share agents with other team members. Once you have done that you just need to click on the register button to automatically register your agent with the TestProject application, and you are ready to start using TestProject!

### Register via CLI - Remote registration 

{% hint style="success" %}
This method can be used for remote agent registration.
{% endhint %}

To register your agent to an account using a CLI on any machine you will need to generate an [API key](https://docs.testproject.io/api/getting-started-with-using-the-testproject-api#getting-an-api-key).

{% hint style="info" %}
Note: the API key will determine to which account this agent will register to. 
{% endhint %}

#### For Linux

Once you have your [API key](https://docs.testproject.io/api/getting-started-with-using-the-testproject-api#getting-an-api-key) head over to the terminal and make sure your agent is running.

You can verify it [here](https://docs.testproject.io/getting-started/installation-and-setup#linux).

Now to register your agent use this command:

```text
./testproject-agent register -a agentName -t Your_API_Key
```

It should look like this:

![Registering the agent on Linux terminal](../.gitbook/assets/image%20%28404%29.png)

#### For Windows 

First, make sure your agent is running you can check [here](https://docs.testproject.io/getting-started/installation-and-setup#windows).

Simply execute this command on your shell or CMD:

```text
testproject-agent register -a agentName -t Your_API_Key
```

It should look like this:

![Registering the agent on Windows CMD](../.gitbook/assets/image%20%28403%29.png)

If your windows does not recognize testproject-agent commands:

Add TestProject agent to your environment variables

Head to Control Panel -&gt; All Control Panel Items -&gt; System -&gt; Advanced system settings -&gt; Advanced -&gt; Environment Variables -&gt; Path -&gt; New

Variable value: `C:\Program Files\TestProject Agent`

You can use the image below:

![Adding test project agent to Environment Variables ](../.gitbook/assets/image%20%28406%29.png)



