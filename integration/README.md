# Asakusa Distribution Integration Tests

This module provides integration tests for this repository. It checks a combination of the runtime, compiler and Gradle plug-ins.

## Requirements

### Platform

This integration test requires both development and runtime environment of Asakusa Framework.

### Envrionemnt variables

* `PATH`
  * must include `cmake` and `make`, additionally `cmake` can detect `gcc` and `g++`
  * no `hadoop` command on the path
* `JAVA_HOME`
  * refer to Java SDK `>= 1.8`

## How to run tests

```sh
./gradlew integrationTest
```

### Available options

* `-PmavenLocal`
  * use artifacts of *test tools* on local repository, this also refers artifacts of `asakusa-core-integration`
  * default: never use artifacts on local repository
* `-Dmaven.local=false`
  * use artifacts of *testee* only on remote repositories
  * default: `true` (preferentially use artifacts on local repositories)
* `-Dhadoop.cmd=/path/to/bin/hadoop`
  * use `hadoop` command
  * default: N/A (skip `hadoop` required tests)
* `-Dspark.cmd=/path/to/bin/spark-submit`
  * use `spark-submit` command
  * default: N/A (skip `spark-submit` required tests)
* `-Dsdk.incubating=true`
  * test with Asakusa SDK incubating features
  * default: `false` (disable incubating features, and **skip** incubating features related tests)
* `-Dasakusafw-distribution.version=x.y.z`
  * change Asakusa Distribution version
  * default: (current version)
* `-Dgradle.version=x.y`
  * change Gradle version (`>= 3.5`)
  * default: (tooling API version)
* `-Dorg.slf4j.simpleLogger.defaultLogLevel=level`
  * change log level
  * default: `debug`

### Tips: running tests on Eclipse

1. Run `./gradlew prepareIntegrationTest`
  * This prepares test data onto `build/integration-test`, it may be lost by `./gradlew clean`
  * with `-PmavenLocal`
    * use Maven local repository to resolve dependencies
2. Run `./gradlew eclipse`.
  * with `-PmavenLocal`
    * use Maven local repository to resolve dependencies
  * with `-PreferProject`
    * use related projects on Eclipse workspace
3. Import this project into the Eclipse workspace.
4. Configure *Run Configuration* of JUnit tests:
  * Add `-Dasakusafw-distribution.version=x.y.z` to `Arguments > VM arguments`
  * Add other options to `Arguments > VM arguments`
5. Run JUnit test
