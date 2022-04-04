# How to create jar file from Java project with TestProject SDK and upload it as a coded test

Download Java SDK from [Integrations](https://app.testproject.io/#/integrations/develop-addon) under Develop an Addon.

![](https://downloads.intercomcdn.com/i/o/259546633/4f83c74d5aded2ab3176c2d9/image.png)

Add the downloaded Jar to the project.

In Intellij, go to file > project structure (ctrl + alt + shift + s with keyboard shortcut) > Modules > Dependencies > click on the plus button > Jars and > select the Jar and click Ok > click Apply and Ok to close settings.

![](https://downloads.intercomcdn.com/i/o/259546851/3e16fd6c61e43e7793192a97/image.png)

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

![](https://downloads.intercomcdn.com/i/o/259550245/1b196b63a3e7f545ee3b86b2/image.png)

Run Maven commands Clean > Compile > Package. You will see a Jar file under target in the project tree.

![](https://downloads.intercomcdn.com/i/o/259550449/c704c15ca8e9bc70846b3064/image.png)

Or Gradle commands Clean > Build > Jar. You will see the Jar file under build > libs

![](https://downloads.intercomcdn.com/i/o/259550537/a26d6523357174508b3a916d/image.png)

In TestProject go to your project and click on Add a new Test > select Code test type > drag the Jar file to the upload area and click on Upload > click Next > provide (meaningful!) package name, you can add Description and Application as well > finish the wizard.
