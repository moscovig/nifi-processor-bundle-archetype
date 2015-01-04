nifi-processor-bundle-archetype
=================

This project contains a Maven archetype for creating new projects to develop
custom processors for the Apache NiFi project.

## Usage

These instructions assume you have JDK7, Maven >= 3.0.5, and have already built [Apache NiFi from
source](https://nifi.incubator.apache.org/development/quickstart.html).

1. Clone this repository to your computer

2. cd nifi-processor-bundle-archetype

3. mvn clean install

4. cd to another directory where you want to create a new project for processor development

5. Generate your new project with the following command:

    mvn archetype:generate -DarchetypeGroupId=org.apache.nifi -DarchetypeArtifactId=nifi-processor-bundle-archetype -DarchetypeVersion=0.0.1-SNAPSHOT -DgroupId={YOUR_GROUP_ID} -DartifactId={YOUR_ARTIFACT_ID} -Dversion={YOUR_VERSION}

    Replace the {YOUR_*} values with appropriate values.
    
    The artifactId you specify will automatically get "-bundle" added to the end of it. For example, 
    an artifactId of "myprocessors" will produce an artifactId of "myprocessors-bundle".
    
    You will be prompted for the NiFi version you want to use. At the time of writing this the only
    version available is 0.0.1-SNAPSHOT so you can hit enter to accept the default, but this is where
    you could specify a different version in the future.

6. You should now be able to cd into the new directory for your artifactId and run mvn clean install

    NOTE: The directory created in step 5 will be your artifactId without "-bundle" even though the poms 
    will have the "-bundle", so you may want to rename this top level directory to add "-bundle" for 
    consistency with the poms.

## Project Structure

Assuming you used "example" as your artifactId in step 5, this archetype will generate a project with 
the following structure:

> example
> ├── example-nar
> │   ├── pom.xml
> │   
> ├── example-processors
> │   ├── pom.xml
> │   ├── src
> │      ├── main
> │      │   ├── java
> │      │   │   └── org
> │      │   │       └── apache
> │      │   │           └── nifi
> │      │   │               └── processors
> │      │   │                   └── MyProcessor.java
> │      │   └── resources
> │      │       └── META-INF
> │      │           └── services
> │      │               └── org.apache.nifi.processor.Processor
> │      └── test
> │          └── java
> │              └── org
> │                  └── apache
> │                      └── nifi
> │                          └── processors
> │                              └── MyProcessorTest.java
> ├── pom.xml

* example-processors 
    
    This is where you will implement your processors, MyProcessor is an example to help get started. Any 
    processors you develop need to be listed in META-INF/services/org.apache.nifi.processor.Processor

* example-nar 

    This project is responsible for creating the nar that will be deployed to nifi. After running a build 
    you can copy example-nar/target/example-nar-1.0.nar to $NIFI_HOME/lib and restart NiFi. Any processors 
    you developed should then be available when adding a new processor to the flow.
    
## Sources

http://maven.apache.org/archetype/archetype-common/archetype-descriptor.html
http://gsmsengupta.blogspot.com/2014/01/creating-archetype-for-multi-project.html
http://www.javacodegeeks.com/2012/02/maven-archetype-creation-tips.html