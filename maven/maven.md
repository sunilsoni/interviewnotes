
Maven
=====

Maven is a tool that is used for building and managing any Java based project. It is a powerful project management tool that is based on POM (Project Object Model). It simplifies the build process.

pom.xml
-------
POM stands for Project Object Model, it is an xml file which contains the configuration information related to the project. Maven uses this file to build the project. We specify all the dependencies that are needed for a project, the plugins, goals etc. By using <packaging> tag, we can specify whether we need to build the project into a JAR/WAR etc.

Maven build life-cycle
----------------------

Maven build life-cycle is made up of  phases
- **validate**: validate the project is correct and all necessary information is available
- **compile**: compile the source code of the project
- **test**: test the compiled source code using a suitable unit testing framework. These tests should not require the code to be packaged or deployed
- **package**: take the compiled code and package it in its distributable format, such as a JAR
- **verify**: run any checks on results of integration tests to ensure quality criteria’s are met
- **install**: install the package into the local repository, for using as a dependency in other projects locally
- **deploy**: done in the build environment, copies the final package to the remote repository for sharing with other developers and projects

Maven will first validate the project, then it will try to compile the sources, run the tests against the compiled code, package the binaries (e.g. jar), run integration tests against that package, verify the integration tests, install the verified package to the local repository and then deploy the installed package to a remote repository.
mvn command can be used to execute these build life-cycle phases. If you run mvn verify, then it will execute all the phases in order, validate, compile, test, package before calling the verify . We only need to call the last build phase.
mvn clean command is used to delete all the project jars that are built by Maven (/target directory of a project). Generally, this clean command is used with install/deploy phase, like mvn clean deploy to cleanly build and deploy artifacts into the shared repository.


