# Slack Actions Addon

This addon provides actions to send Slack messages from you tests. These messages are sent using a webhook. Of course this means you will need a webhook url. You can create one for your slack channel, by following along with the [Slack documentation for creating webhooks](https://api.slack.com/messaging/webhooks). Once you have specified the webhook for the channel you want to send messages to, you can enter in the text that you want sent. You can also specify a number of optional properties as well.

* Text Color - Set the color of the text that gets written in slack using hexadecimal format
* Title - Set the title of the message
* Title\_link - Turn the title of the slack message into a clickable hypertext link that will take you to the specified url
* Author - Specify the author of the message
* Additional\_text - Add additional text as an attachment to the message

### Troubleshooting

#### **Failure Criteria**

This action have several criterion that may result in failure assertion:

* When `webhook` or `message` inputs are empty.
* When the given `webhook` parameter is not a valid Slack incoming webhook.
* When server fails to respond.
* Connectivity errors

#### Troubleshooting Actions

The action will report a message with the following information:

* In case the user didn't provide a webhook:

  > You must provide a webhook URL

* In case the user didn't provide a message:

  > Message can not be empty

* In case the user provided an invalid webhook URL \(not in the correct format defined by Slack: 

  > Invalid slack webhook URL

* In case the server responded with a status code other than 200 \(OK\):

  > Server returned invalid response code: {{response\_code}}

* In case of an exception that occurred while the request was being sent:

  > throw new FailureException\("Failed sending Slack text", e\)

* In case of success:

  > The message was sent successfully

### Further Information

Further information on this addon can be found in the [github repo](https://github.com/testproject-io/addons/tree/master/slack-actions) for it where you can see the code and some additional documentation

