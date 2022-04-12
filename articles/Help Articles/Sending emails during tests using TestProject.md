---
description: Sending emails using the Picksmart Send Email addon.
---

# Sending emails during tests using TestProject

If you'd like to send emails during the execution of your test, you can do so by using the Simple Mail Transfer Protocol (SMTP) and Picksmart Send Email addon.

To use this addon, you'll need to install the addon from the addons section:

![](<../../.gitbook/assets/image (509) (1).png>)

Then create the '**Picksmart Send Email**' action in one of your tests.

Once the action is created, you'll need to fill in each one of its fields:

_**RecipientAddress**_ - The address to the email will be sent to.

_**AttachmentPath**_ - Optional parameter for email attachment.

_**Host**_ - The SMTP host name that will send the email.

_**FromEmail**_ - The email account associated with the SMTP host entered previously, that will send the email to the recipient.

_**SSLPort**_ - The SSL port number that will be used to send the email.

**Subject** - Will be the Subject of the sent email message.

_**BodyText**_ - This Will be the content of the sent email.

_**SmtpUsername**_** - The username needed to log into the SMTP server.**

_**SmtpPassword**_ - The password needed to log into the SMTP server.

Once you're done configuring the step, if all the input parameters are filled in correctly, your email will be sent with the subject, content, and attachment as defined above once you run it.

In the following example, we'll send an email using the Google SMTP server.

Before proceeding, you'll need to allow access from less secure apps for your account. These settings need to be turned on:\
[https://myaccount.google.com/lesssecureapps](https://myaccount.google.com/lesssecureapps)

![](<../../.gitbook/assets/image (505) (1).png>)

Then, as mentioned before, create the step and fill in the input fields:

For **GMAIL**:

The host is: **smtp.gmail.com**

The SSLPort should be: 465

The SMTP username is your Google account email address, without the domain, i.e. [my\_email@gmail.com](mailto:my\_email@gmail.com), the username should be **my\_email**, and the password is the same as for that account itself.

![](<../../.gitbook/assets/image (562) (1).png>)

![](<../../.gitbook/assets/image (481).png>)

After running the step, the email will be sent to the account specified:

![](https://downloads.intercomcdn.com/i/o/223752464/38fd700e84efc56ff189fd01/3.png)

When using on different SMTP hosts, please make sure to set up their server requirements and fill in the parameters correctly. For example, Yahoo will require you to go through a different process than allowing less secure apps, as we did for the example from Google.
