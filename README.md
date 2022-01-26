**    **Jenkins Pipeline Support for Spock*****
Utility classes to help with testing Jenkins pipeline scripts and functions written in Groovy.

User Guide (GroovyDoc)
Add this library to pom.xml in the test scope:

<dependency>
	<groupId>com.homeaway.devtools.jenkins</groupId>
	<artifactId>jenkins-spock</artifactId>
	<scope>test</scope>
</dependency>
Check the CHANGELOG.md to find details about the available versions.

Working Examples
The examples directory contains working sample projects that show off the major kinds of project this library can be used with. Check them out and try building them yourself!

Specifications
This library provides a JenkinsPipelineSpecification class that extends the Spock testing framework's Specification class. To test Jenkins pipeline Groovy code, extend JenkinsPipelineSpecification instead of Specification. Please see the GroovyDoc for JenkinsPipelineSpecification for specific usage information and the Spock Framework Documentation for general usage information.

During the tests of a JenkinsPipelineSpecification suite,

All Jenkins pipeline steps (@StepDescriptors) will be globally callable, e.g. you can just write sh( "echo hello" ) anywhere.
"Body" closure blocks passed to any mock pipeline steps will be executed.
All Jenkins pipeline variables (@Symbols and GlobalVariables) will be globally accessible, e.g. you can just write docker.inside(...) anywhere
All Pipeline Shared Library Global Variables (from the /vars directory) will be globally accessible, so you can just use them anywhere.
All interactions with any of those pipeline extension points will be captured by Spock mock objects.
You can load any Groovy script (Jenkinsfile or Shared Library variable) to unit-test it in isolation.
The Jenkins singleton instance will exist as a Spock mock object.
The CpsScript execution will exist as a Spock spy object (you should never need to interact with this, but it's there).
Dependencies
There are some dependencies of this library that are marked with Maven's provided scope. This means that Maven will pull them in for building and testing this library, but when you use this library you must pull those libraries in as dependencies yourself.

This is done because these dependencies - things like the Jenkins Pipeline API, JUnit, etc - are things that

You absolutely have to have as dependencies in your project in order for this library to be of any use
Should not have their version or final scope controlled by this library
The dependencies that should already be in your project in order for using this library to make any sense are:

<dependency>
	<groupId>org.jenkins-ci.main</groupId>
	<artifactId>jenkins-core</artifactId>
	<version>${jenkins.version}</version>
	<scope>test</scope>
</dependency>
<dependency>
	<groupId>org.jenkins-ci.plugins.workflow</groupId>
	<artifactId>workflow-step-api</artifactId>
	<version>${jenkins.workflow.step.version}</version>
	<scope>test</scope>
</dependency>
<dependency>
	<groupId>org.jenkins-ci.plugins.workflow</groupId>
	<artifactId>workflow-cps</artifactId>
	<version>${jenkins.workflow.cps.version}</version>
	<scope>test</scope>
</dependency>
<dependency>
	<groupId>org.jenkins-ci</groupId>
	<artifactId>symbol-annotation</artifactId>
	<version>${jenkins.symbol.version}</version>
	<scope>test</scope>
</dependency>

<dependency>
	<groupId>junit</groupId>
	<artifactId>junit</artifactId>
	<version>${junit.version}</version>
	<scope>test</scope>
</dependency>

<dependency>
	<groupId>javax.servlet</groupId>
	<artifactId>javax.servlet-api</artifactId>
	<version>${jenkins.servlet.version}</version>
	<scope>test</scope>
</dependency>
Depending on your parent pom, some of the ${jenkins.version} properties may already be defined. Be sure you define any that are not.

If your code actually writes code against classes in any of these dependencies, remove the <scope>test</scope> entry for the corresponding block(s).
