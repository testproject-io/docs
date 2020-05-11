# Slack Integration

Slack is a powerful communication tool used by many companies. Test Project can easily integrate with Slack allowing you to get notifications and information about your test automation runs directly in a slack channel.

## Adding Slack Integration to TestProject

After logging into your TestProject account, go to the Integrations tab and click on the Web Hooks + Slack option

![Slack integrations](../.gitbook/assets/image%20%2853%29.png)

Click the ![](https://blog.testproject.io/wp-content/uploads/2019/03/add_to_slack.png) icon and you will be redirected to the Slack authorization page.

After the redirect you will need to choose the team and a channel where your TestProject notifications will be sent to \(_You will be asked to login into your Slack team account if you were not already logged in_\). Choose to “Authorize” and you will be redirected back to the “Integrations” section of your TestProject account settings. You will now see a Slack integration entry containing the name of your slack team and the channel for the integration.

## Sending TestProject Job Notifications to Slack

After setting up Slack integration and authorizing a designated channel, notifications can be sent. Simply navigate to a project that has jobs setup and click on the _envelope_ icon of your job of choice to open the notifications preferences. You can then Enable Web Hooks and select the Slack integration you want to use.

![](../.gitbook/assets/image%20%28227%29.png)

This is it! You will now receive a well formatted job execution summary in Slack after the job completes its execution. Here is an example of such a notification for a “Sanity” job that was executed on Chrome and IE browsers and contained 2 tests. The notification also contains a direct link to the generated TestProject report.

![Slack Notification](https://blog.testproject.io/wp-content/uploads/2019/03/chrome_s2dPcnsKJp.png)

