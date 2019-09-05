# Troubleshooting

If you get stuck on something, try some of suggestions below or feel free to contact us at any time.  You can always chat us directly from the TestProject app, or post a question on the [forum](https://forum.testproject.io/).

## Agent won't register

Some organizations have firewall rules in place that prevent the TestProject agent from communicating to the app in the way that it needs to. Check with your IT team to see if this may be the issue.  You can also check your computer's firewall settings to make sure TestProject is not getting blocked

If you are using a proxy or vpn to connect to the internet, you may need to configure it. There is a file named agent-configuration.json in `%USERPROFILE%\AppData\Roaming\TestProject\Agent` where you can provide the proxy details and set enableProxy to true.

## Can't find my agent to run tests against

Make sure you have a TestProject agent [installed and running](../getting-started/installation-and-setup.md) on your local machine. If not, you will need to start the agent before you can use it to run tests. If the agent is running, you can try restarting it.

## Blank Screen when trying to record mobile tests

Make sure you do not have any other mirroring software running. 



