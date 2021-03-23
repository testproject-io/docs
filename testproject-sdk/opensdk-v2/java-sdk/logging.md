# Logging

The TestProject Java SDK uses SLF4J API for logging. This means that it only binds to a thin logger wrapper API, and does not provide a logging implementation of it's own.

Developers must choose a concrete implementation to use in order to control the logging output. There are many SLF4J logger implementation choices, such as the following:

* [Logback](http://logback.qos.ch/)
* [Log4j](https://logging.apache.org/log4j/2.x/)
* [Java Logging](https://docs.oracle.com/javase/8/docs/api/java/util/logging/Logger.html)

Note that each logger implementation would have it's own configuration format. Once you have decided which logger to use, you can consult the specific logger documentation to see more details on how to use it.

### Using slf4j-simple

This is the simplest option that requires no configuration at all. The only thing you need to do is to add a [dependency](https://mvnrepository.com/artifact/org.slf4j/slf4j-simple) to the project:

Maven:

```text
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-simple</artifactId>
    <version>1.7.30</version>
    <scope>test</scope>
</dependency>
```

Gradle:

```text
testCompile group: 'org.slf4j', name: 'slf4j-simple', version: '1.7.30'
```

By default, logging level for this is set to _INFO_. If you want to see _TRACE_ verbose messages, add this System Property `-Dorg.slf4j.simpleLogger.defaultLogLevel=TRACE`

### Using Logback

Logback is a very popular logger implementation that is production ready and packed with many features. To use it, add a [dependency](https://mvnrepository.com/artifact/ch.qos.logback/logback-classic) to the project:

Maven:

```text
<dependency>
    <groupId>ch.qos.logbackgroupId>
    <artifactId>logback-classicartifactId>
    <version>1.2.3version>
    <scope>testscope>
dependency>
```

Gradle:

```text
testCompile group: 'ch.qos.logback', name: 'logback-classic', version: '1.2.3'
```

Then create a new file `src/main/resources/logback.xml` in your project and paste the following:

```text
<configuration>

    
    <statusListener class="ch.qos.logback.core.status.NopStatusListener" />

    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <layout class="ch.qos.logback.classic.PatternLayout">
            <Pattern>
                %d{yyyy-MM-dd HH:mm:ss.SSS} %highlight(%-5level) %-20logger{0} %message%n
            Pattern>
        layout>
    appender>

    <logger name="io.testproject" level="ALL" />

    <root level="ERROR">
        <appender-ref ref="CONSOLE"/>
    root>

configuration>
```

