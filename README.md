# Template Repository for custom distributions of Tractus-X EDC

## Quick start

To get the example up-and-running, there are two possibilities:

- using Docker:
  ```shell
  ./gradlew dockerize # on x86/64 platforms
  ./gradlew dockerize -Dplatform="linux/amd64" # on arm platforms, e.g. Apple Silicon
  ```
  Then there should be two new images in your image cache, `controlplane:latest` and `dataplane:latest`

- using a native Java process
  ```shell
  ./gradlew build
  java -jar runtimes/[controlplane|dataplane]/build/libs/[controlplane|dataplane].jar
  ```

In both cases configuration must be supplied, either using Docker environment variables, or using Java
application properties.

## Directory structure

- `config`: contains the configuration file for the Checkstyle plugin
- `extensions`: this is where your extension modules should be implemented
- `gradle`: contains the Gradle Wrapper and the Version Catalog
- `runtimes`: contains executable modules for the controlplane and data plane


## When developing only an extension

This is for develops whos focus is in developing a runtime module, which implements features and thereby extends
the EDC- and Tractus-X EDC functionality. For example, implementing support for a new database technology could be
implemented in one (or several) extensions.

If this is you, then you should focus mainly on the `extensions/` directory.

## When developing a custom runtime

This is for developers who want to package several extensions into a new _runtime_. A runtime in EDC-speak is a
runnable application. We achieve this by packaging all class files into a fat JAR using the Shadow Plugin, but naturally
other approaches exist (but are not covered here).

If this is you, then you should focus mainly on the `runtimes/` directory.

Both runtimes provided in this template are simply pulling in the official Tractus-X control plane and data plane
modules.

