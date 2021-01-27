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

Here's an example of how this can be done with Gradle in build.gradle:

```text
jar {
    from { configurations.testRuntimeClasspath.collect { it.isDirectory() ? it : zipTree(it) } }
    from sourceSets.test.output+sourceSets.test.allSource
}
```



