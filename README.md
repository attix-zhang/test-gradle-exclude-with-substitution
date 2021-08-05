# test-gradle-exclude-with-substitution

This repository is used to demostrate the bug when ues exclude and dependency substitution at same time.

In the `build.gradle` file, I exlcude the `com.google.guava:guava`. However, if other dependency is rewritten to guava, I will still get `guava`:

```
➜  test-gradle-exclude-with-substitution git:(main) ./gradlew dependencyInsight --dependency com.google.guava:guava --configuration compileClasspath

> Task :dependencyInsight
com.google.guava:guava:20.0 (selected by rule)
   variant "compile" [
      org.gradle.status              = release (not requested)
      org.gradle.usage               = java-api
      org.gradle.libraryelements     = jar (compatible with: classes)
      org.gradle.category            = library

      Requested attributes not found in the selected variant:
         org.gradle.dependency.bundling = external
         org.gradle.jvm.version         = 8
   ]

com.jcraft:jsch:0.1.42 -> com.google.guava:guava:20.0
\--- org.apache.hadoop:hadoop-common:2.6.0
     \--- compileClasspath

A web-based, searchable dependency report is available by adding the --scan option.

Deprecated Gradle features were used in this build, making it incompatible with Gradle 7.0.
Use '--warning-mode all' to show the individual deprecation warnings.
See https://docs.gradle.org/6.8.1/userguide/command_line_interface.html#sec:command_line_warnings

BUILD SUCCESSFUL in 535ms
1 actionable task: 1 executed
```
