---
description: >-
  In this article i will show how you can obtain the Root CA and add to trusted
  root CA authorities
---

# "Your connection is not private" solution on Chrome

Some websites (especially ones under development) can be seen by google chrome as potentially harmful, like shown here\


![](https://downloads.intercomcdn.com/i/o/203177082/a16feca836bbb03747a4100d/image.png)

In this case, you might not be able to record or execute tests on the platform! in this article, i will show you how to authorize the websites on your machine so you can carry on with your tests. I will use [https://untrusted-root.badssl.com/](https://untrusted-root.badssl.com) as an example.\


Navigate to the website with untrusted certificate, and click on the "Not Secure" label next to the URL:

![](https://downloads.intercomcdn.com/i/o/203178433/61ca2c399cd521c9ef020ddd/image.png)

Click on Certificate

![](https://downloads.intercomcdn.com/i/o/203179803/3a65d4349b2a087e9ab5f3ca/image.png)

\
Switch to the last tab - Certification Path, and you should see a certificates chain tree, choose the **first** one (not he 2nd one selected).

![](https://downloads.intercomcdn.com/i/o/203180359/ec008e09b5fb783d0f551f26/image.png)

\
Click on View certificate, switch to the details tab and click copy the certificate to file.

![](https://downloads.intercomcdn.com/i/o/203181972/54577a17401e48e83f517df3/image.png)

Then click next, and select the first option:

![](https://downloads.intercomcdn.com/i/o/203184136/470e2db9def53f3ea62b3321/image.png)

Then click browse and create the file to output to, then hit next:

![](https://downloads.intercomcdn.com/i/o/203184818/300070d14a27bc98d264063a/image.png)

Now double click the new file and follow the instructions:

![](https://downloads.intercomcdn.com/i/o/203189090/5e47296afb3f12169b94eb0c/image.png)

![](https://downloads.intercomcdn.com/i/o/203189183/08bb304891d66a35cf23c23b/image.png)

Now choose the **Trusted Root Certification Authorities** via browse button:

![](https://downloads.intercomcdn.com/i/o/203192292/bf884c2c99e43152f379e374/image.png)

Click next, then finish, windows will ask you in you are sure, agree.\


Now simply restart Chrome with chrome://restart:

![](https://downloads.intercomcdn.com/i/o/203190290/107cc61be283fedd80edc31c/image.png)

And you should be good to go!\


\


![](https://downloads.intercomcdn.com/i/o/203193547/1566ecddb76c45394a2292fd/image.png)
