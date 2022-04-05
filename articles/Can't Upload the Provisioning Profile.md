# Can't Upload the Provisioning Profile

If you encountered this error that says the provisioning profile uploading failed, then it means that some step in the iOS configuration process went wrong.\
Try the below solutions to fix this issue:

1. Make sure you followed this tutorial step by step. Do exactly as it says: [https://blog.testproject.io/2019/01/29/setup-ios-test-automation-windows-without-mac/](https://blog.testproject.io/2019/01/29/setup-ios-test-automation-windows-without-mac/)
2. You need to make sure you include the correct certificate in your provisioning profile. The whole iOS configuration process is about exchanging certificates between Apple and TestProject. First, you generate a CSR (Certificate Signing Request) file from TestProject. Then, you create the Apple certificate based on that CSR file. It is very important to do it exactly that way.\
   Once the Apple certificate is generated, you must include it in the provisioning profile that you are creating. If you are not sure what certificate to select, you can select all of them.
3. If non of the above helped, start the configuration process again and make sure you are following the instruction step-by-step
