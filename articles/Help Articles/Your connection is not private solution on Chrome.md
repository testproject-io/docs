---
description: >-
  In this article i will show how you can obtain the Root CA and add to trusted
  root CA authorities
---

# "Your connection is not private" solution on Chrome

Some websites (especially ones under development) can be seen by google chrome as potentially harmful, like shown here\


![](<../../.gitbook/assets/image (448) (1).png>)

In this case, you might not be able to record or execute tests on the platform! in this article, i will show you how to authorize the websites on your machine so you can carry on with your tests. I will use [https://untrusted-root.badssl.com/](https://untrusted-root.badssl.com) as an example.\


Navigate to the website with untrusted certificate, and click on the "Not Secure" label next to the URL:

![](<../../.gitbook/assets/image (471) (1).png>)

Click on Certificate

![](<../../.gitbook/assets/image (508) (1).png>)

\
Switch to the last tab - Certification Path, and you should see a certificates chain tree, choose the **first** one (not he 2nd one selected).

![](<../../.gitbook/assets/image (540) (1) (1).png>)

\
Click on View certificate, switch to the details tab and click copy the certificate to file.

![](<../../.gitbook/assets/image (456) (1).png>)

Then click next, and select the first option:

![](<../../.gitbook/assets/image (513).png>)

Then click browse and create the file to output to, then hit next:

![](<../../.gitbook/assets/image (463) (1) (1).png>)

Now double click the new file and follow the instructions:

![](<../../.gitbook/assets/image (453) (1) (1).png>)

![](<../../.gitbook/assets/image (497).png>)

Now choose the **Trusted Root Certification Authorities** via browse button:

![](<../../.gitbook/assets/image (487) (1).png>)

Click next, then finish, windows will ask you in you are sure, agree.\


Now simply restart Chrome with chrome://restart:

![](<../../.gitbook/assets/image (546) (1).png>)

And you should be good to go!\


![](<../../.gitbook/assets/image (494) (1).png>)
