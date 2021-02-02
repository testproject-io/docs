---
description: How to package tests into JAR before uploading to TestProject
---

# Packaging

## SDK \(v1\)

When using SDK v1, there is no need to package the SDK into the final JAR, refer to the following examples on how to **exclude** SDK v1 rom the final JAR:

* [Maven & pom.xml](https://github.com/testproject-io/addons/blob/master/Examples/Web/pom.xml#L57)
* [Gradle and build.gradle](https://github.com/testproject-io/addons/blob/master/Examples/Web/build.gradle#L33)

## Open SDK \(v2\)

When using the OpenSDK v2, you have to include the SDK with the final JAR you create, the easiest way to do it is by building a "fat" JAR. Also, in order to include your unit tests in the final JAR, you have to explicitly configure it during the build.

### Gradle <a id="gradle"></a>

Here's an example of additions to `build.gradle` that will create a JAR with dependencies and test classes:

#### build.gradle

```groovy
jar {
    // Include compiled test classes and their sources
    from sourceSets.test.output+sourceSets.test.allSource

    // Collect and zip all classes from both test and runtime configurations
    from { configurations.testRuntimeClasspath.collect { it.isDirectory() ? it : zipTree(it) } }
}
```

### Maven <a id="maven"></a>

Here's an example of additions to `pom.xml` and a descriptor that will create a JAR with dependencies and test classes:

#### pom.xml

```markup
<build>
    <plugins>
        <!-- Use maven-jar-plugin to include tests -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-jar-plugin</artifactId>
            <executions>
                <execution>
                    <goals>
                        <goal>test-jar</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
        <!-- Use maven-assembly-plugin plugin with a custom descriptor -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <configuration>
                <descriptors>
                    <!-- Path to the descriptor file -->
                    <descriptor>src/main/java/assembly/test-jar-with-dependencies.xml</descriptor>
                </descriptors>
            </configuration>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

#### Assembly Descriptor

Save this file under `src/main/java/assembly` as `test-jar-with-dependencies.xml`:

```markup
<assembly xmlns="http://maven.apache.org/plugins/maven-assembly-plugin/assembly/1.1.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/plugins/maven-assembly-plugin/assembly/1.1.0 http://maven.apache.org/xsd/assembly-1.1.0.xsd">
    <id>test-jar-with-dependencies</id>
    <formats>
        <format>jar</format>
    </formats>
    <includeBaseDirectory>false</includeBaseDirectory>
    <dependencySets>
        <dependencySet>
            <outputDirectory>/</outputDirectory>
            <useProjectArtifact>true</useProjectArtifact>
            <useProjectAttachments>true</useProjectAttachments>
            <unpack>true</unpack>
            <scope>test</scope>
        </dependencySet>
    </dependencySets>
</assembly>
```

