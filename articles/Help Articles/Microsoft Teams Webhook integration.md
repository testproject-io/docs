---
description: Microsoft Teams, webhook, teams, TestProject notifications
---

# Microsoft Teams Webhook integration

To integrate Microsoft Teams Web Hooks on TestProject you will need to follow this quick and easy to set-up article.

#### **Requirements:** <a href="#h_d9da62f024" id="h_d9da62f024"></a>

1\) TestProject account (Admin):

If the webhook is already configured user privileges will suffice.

Admin - configuring the webhook

2\) Teams account:

Admin or sufficient privileges to add connectors.

#### **Steps on Teams:** <a href="#h_9ffac7326a" id="h_9ffac7326a"></a>

1\) Add a Connectors from context menu --> Connectors:

![](<../../.gitbook/assets/image (468) (1).png>)

2\) Add "Incoming Webhook":

![](<../../.gitbook/assets/image (461) (1).png>)

3\) Add:

![](<../../.gitbook/assets/image (467) (1).png>)

4\) Click "Connectors" one more time:

![](<../../.gitbook/assets/image (476) (1).png>)

5\) Choose "Configure":

![](<../../.gitbook/assets/image (469) (1).png>)

6\) Enter the required details and **Copy URL Link:**

![](<../../.gitbook/assets/image (460) (1).png>)

**Steps on TestProject (Admin):**

_If you are a user ask your admin to create a Teams Web Hook and skip to steps 3-4._

1\) go to Integrations --> Web Hooks + Slack --> Add Web Hook:

![](<../../.gitbook/assets/image (474) (1).png>)

2\) Add all the Required information:

![](<../../.gitbook/assets/image (464) (1).png>)

3\) You are now ready to add this Webhook to the job notifications, you can do it from here:

![](<../../.gitbook/assets/image (449) (1).png>)

4\) Choose the created WebHook:

![](<../../.gitbook/assets/image (455) (1).png>)

Now everything is set and ready, a TestProject notification looks like this:

![](<../../.gitbook/assets/image (450) (1).png>)
