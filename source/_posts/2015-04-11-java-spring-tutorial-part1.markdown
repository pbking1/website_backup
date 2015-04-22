---
layout: post
title: "java spring tutorial part1"
date: 2015-04-11 15:41:46 -0400
comments: true
categories: java System_analyze_and_design
---

###maven
- make sure 'mvn -v' return the current version in you computer
- otherwise, install the maven first

###Hello world
- project hierarchy
	- helloworld (folder)
		- (root directory)
		- src
			- main
				- java
					- hello
						- Greeter.java
						- HelloWorld.java
		- target(auto generate after mvn install)
			- helloworld-0.1.0.jar
		- pom.xml
<!--more-->
####class
- `mkdir -p src/main/java/hello`
	- make a directory to put the java class
- create two class `HelloWorld.java` and `Greeter.java`
	- HelloWorld.java
		- ```
			package hello;

			import org.joda.time.LocalTime;

			public class HelloWorld{
				public static void main(String[] args){
					LocalTime currentTime = new LocalTime();
					System.out.println("The currentTime local time is " + currentTime);
					Greeter greeter = new Greeter();
					System.out.println(greeter.sayHello());
				}
			}

		```

	- Greeter.java
		- ```
			package hello;

			public class Greeter {
			    public String sayHello() {
			        return "Hello world!";
			    }
			}
		```

####configuration
- pom.xml
	- put the file in the root of the project
	- ```
		<?xml version="1.0" encoding="UTF-8"?>
		<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
		    <modelVersion>4.0.0</modelVersion>
		    <groupId>org.springframework</groupId>
		    <artifactId>helloworld</artifactId>
		    <packaging>jar</packaging>
		    <version>0.1.0</version>
			
			<!--- 插件 -->
			<dependencies>
				<dependency>
					<groupId>joda-time</groupId>
					<artifactId>joda-time</artifactId>
					<version>2.2</version>
				</dependency>
			</dependencies>

		    <build>
		        <plugins>
		            <plugin>
		                <groupId>org.apache.maven.plugins</groupId>
		                <artifactId>maven-shade-plugin</artifactId>
		                <version>2.1</version>
		                <executions>
		                    <execution>
		                        <phase>package</phase>
		                        <goals>
		                            <goal>shade</goal>
		                        </goals>
		                        <configuration>
		                            <transformers>
		                                <transformer
		                                    implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
		                                    <mainClass>hello.HelloWorld</mainClass>
		                                </transformer>
		                            </transformers>
		                        </configuration>
		                    </execution>
		                </executions>
		            </plugin>
		        </plugins>
		    </build>
		</project>
	```

####run the maven project
- compile
	- mvn compile
- install
	- mvn install
- two ways to run
	- java -jar helloworld-0.1.0.jar 
	- mvn exec:java -Dexec.mainClass="hello.HelloWorld"