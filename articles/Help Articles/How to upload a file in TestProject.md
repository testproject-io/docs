# How to upload a file in TestProject?

Uploading a file from your local machine to your website is a pretty common scenario. It's an important scenario that needs to be tested and it usually completes the test flow.&#x20;

The problem you might face in your attempt to upload a file is when you click on the upload button. It immediately opens the native OS file explorer dialog, where you are required to select the file that you want to upload. Selenium cannot automate the native OS file dialog, so you won't be able to record your actions on that dialog.

Let's have a look at this input element of type file:

![](https://downloads.intercomcdn.com/i/o/174436615/39940eea0106e1d72af3a335/o8ZjEu5GMt.png)

As mentioned above, clicking on the **"Choose File"** button would trigger the native OS file explorer dialog:

![](https://downloads.intercomcdn.com/i/o/174436801/2cfaf4f750f934fb0b8be7dd/VGcv5mcsjE.png)

This element can also be wrapped by another element with different styles, but as long as it's an input element of type file, this following addon will know how to handle it.\


### The File Uploader Addon <a href="#the-file-uploader-addon" id="the-file-uploader-addon"></a>

To overcome this limitation and to simplify the file upload process, we've created the [**File Uploader**](https://addons.testproject.io/file-uploader) addon. This addon contains two actions for uploading a file in your web test:

_**Upload File using XPath**_ - This is an action that requires the XPath of the input element: **//input\[@type = 'file'].** The second parameter is of course, the local path to the file you want to upload.

![](https://downloads.intercomcdn.com/i/o/396692453/c872094228d1e20da997e89a/NOcoHOnsIP.gif)

\
_**Upload file to input element**_ - This is an element action and you need to use it on the input element. It works on two types of elements that are located by these XPaths: **//button\[text()='Upload']** AND **//input\[@type = 'file']**. This element action takes only one input parameter which is the local path to the file that you want to upload.

![](https://downloads.intercomcdn.com/i/o/396690225/ab130d8bb5413a8ab1220a62/murRYmggH0.gif)

_**Important Note:**_

_Some websites require an action to happen before the file type element becomes visible in the explorer, If your element is missing try to continue the sequence of uploading the file (manually) until you can detect the element try to do it step by step._

**Still need help?**

Common issues and troubleshoot / missing elements:

[https://forum.testproject.io/t/file-uploading-addon-fails-during-runtime-to-upload-file/2479](https://forum.testproject.io/t/file-uploading-addon-fails-during-runtime-to-upload-file/2479)

[https://forum.testproject.io/t/issue-with-file-upload-button/4599/19](https://forum.testproject.io/t/issue-with-file-upload-button/4599/19)

\
