# How can I upload a coded test to TestProject

If you want to create your tests as coded tests by using our Java or C# Selenium and Appium Powered SDK, then once you finish developing your test in your favorite IDE, you need to upload it to TestProject.

A single Java/C# project can contain multiple test cases (represented by a class that implements the required interface). Once you upload your project to TestProject, it will be shown as a package that contains all the test cases inside it.

#### Uploading a Java project <a href="#uploading-a-java-project" id="uploading-a-java-project"></a>

To upload a Java project, you need to compile your project to .jar file. You can use Gradle, Maven or any build tool that you like.

**For Gradle**: Open the **Gradle tab** and go to **Tasks/build/jar.** Once the jar task is finished, you will find your jar file here: **build/libs/YOUR\_JAR**

![](https://downloads.intercomcdn.com/i/o/173692962/186d27ac84d11a716c8f31e4/KbsQNCoT7I.png)

![](https://downloads.intercomcdn.com/i/o/173692970/db0c29af5f6c3877d7e2d314/Edsa4wTc8b.png)

**For Maven**: Open the Maven tab, go to **Lifecycle** and execute: **clean, compile, package.** Once the package command is finished, you will find your jar file in the **target** folder (the jar without dependencies).

![](https://downloads.intercomcdn.com/i/o/173693586/eb54baccbc4c9cc9ab2caadf/bcHsUgxlX8.png)

![](https://downloads.intercomcdn.com/i/o/173693664/7aea4391ee514e004c9f958b/4fXkdMTNaX.png)

#### Uploading a C# project <a href="#uploading-a-c-project" id="uploading-a-c-project"></a>

To upload a C# project, you will need to get the .dll file of the project.\
Right-click on your project in the Solution Explorer and click on build. Once the build is done, right-click again on the project and open it in file explorer. To get the .dll file: bin/Debug/netcoreappX.X upload the .dll file in that folder. If you have more than one .dll file, it means that you used addons proxy in your test and you need to include them too. Zip all the .dll files together and upload to TestProject:

![](https://downloads.intercomcdn.com/i/o/173695167/ae6d7309fd415b96cfd1e74c/T6Uf7TEij6.gif)

#### Upload your Java/C# project to TestProject <a href="#upload-your-javac-project-to-testproject" id="upload-your-javac-project-to-testproject"></a>

**Go to your project in TestProject and click on "Add a new Test":**

![](https://downloads.intercomcdn.com/i/o/173695320/f2b1839e281c71b5d58a6dcb/FuJHpeC8Qh.png)

**Select the "Code" option and click "Next":**

![](https://downloads.intercomcdn.com/i/o/173695403/115c010f4277aea3b608acae/aVteF80yau.png)

**Drag and drop the jar/dll/zip file here:**

![](https://downloads.intercomcdn.com/i/o/173695536/f1d22ee0e3cf4467ced02413/chrome\_0MXvMQcYGs.png)

**Click "Next":**

![](https://downloads.intercomcdn.com/i/o/173695661/b77315b1d31c7d4bd9650496/chrome\_tI7dkfjCxX.png)

**Select the platform, name, description and application:**

![](https://downloads.intercomcdn.com/i/o/173696015/542797fcdb4bab31509b1d6d/chrome\_8PRyZUIFwu.png)

That's it! You successfully uploaded your coded test to TestProject :)
