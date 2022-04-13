# How can I generate code from my recorded test and open the generated code in my IDE?

TestProject allows you to export your recorded test into Java or C# coded tests in a click of a button. That cool feature, allows you to continue working on your test in your IDE and later, to upload it back to TestProject.

#### How to download the code <a href="#how-to-download-the-code" id="how-to-download-the-code"></a>

In your project, go to the test that you want to generate the code for and click on the three-dots icon. Then, select the Generate Code option:

![](<../../.gitbook/assets/image (453).png>)

Select the preferred language that you want to export the test to, the browser and the package name:

![](<../../.gitbook/assets/image (536).png>)

#### How to open the Java project <a href="#how-to-open-the-java-project" id="how-to-open-the-java-project"></a>

Once the project has been downloaded, extract the zip file.\
Open your IDE (IntelliJ, Eclipse, etc.)  -> File -> Open -> select the extracted folder of your test.

In your IDE, open the build.gradle file and update the TP\_SDK variable value to the path where you stored the Java SDK on your machine (you can download it from [here](https://app.testproject.io/#/integrations/develop-addon)). Now, the project will be updated and you should be able to run your test!\
To run the test, simply run the "Runner" class.

#### How to open the C# project <a href="#how-to-open-the-c-project" id="how-to-open-the-c-project"></a>

Once the project has been downloaded, extract the zip file. Double click on the .csproj file to open it in your IDE (Visual Studio, etc.). The TestProject C# SDK will be included automatically by the NuGet Package Manager.\
To run your test, simply click on the run button (F5).
