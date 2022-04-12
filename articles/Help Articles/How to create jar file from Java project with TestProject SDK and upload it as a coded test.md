# How to create jar file from Java project with TestProject SDK and upload it as a coded test

Download Java SDK from [Integrations](https://app.testproject.io/#/integrations/develop-addon) under Develop an Addon.

![](<../../.gitbook/assets/image (463) (1).png>)

Add the downloaded Jar to the project.

In Intellij, go to file > project structure (ctrl + alt + shift + s with keyboard shortcut) > Modules > Dependencies > click on the plus button > Jars and > select the Jar and click Ok > click Apply and Ok to close settings.

![](<../../.gitbook/assets/image (448).png>)

In Eclipse, Right click on your project > select Build Path > click on Configure

Build Path > click on Libraries and select Add External JARs > select the jar file > click Apply and Ok.

Add dependency in `pom.xml` file for Maven

```xml
<dependency>
    <groupId>io.testproject</groupId>
    <artifactId>java-sdk</artifactId>
    <version>0.63.1</version>    
    <systemPath>/path/to/sdk/io.testproject.sdk.java.jar</systemPath>
    <scope>system</scope>
</dependency>
```

Or in `build.gradle` file for Gradle

```xml
dependencies {
    compile files('>/path/to/sdk/io.testproject.sdk.java.jar')
}
```

Write your tests. Keep in mind [Implicit Project and Job Names](https://intercom.help/testprojectio/en/articles/1.https:/docs.testproject.io/testproject-sdk/opensdk-v2/java-sdk#implicit-project-and-job-names).

Add file named `testproject-sdk.properties` under resources folder with the content `version=0.63.1` (or other version if you prefer).

![](<../../.gitbook/assets/image (556) (1).png>)

Run Maven commands Clean > Compile > Package. You will see a Jar file under target in the project tree.

![](<../../.gitbook/assets/image (468).png>)

Or Gradle commands Clean > Build > Jar. You will see the Jar file under build > libs

![](<../../.gitbook/assets/image (458).png>)

In TestProject go to your project and click on Add a new Test > select Code test type > drag the Jar file to the upload area and click on Upload > click Next > provide (meaningful!) package name, you can add Description and Application as well > finish the wizard.
