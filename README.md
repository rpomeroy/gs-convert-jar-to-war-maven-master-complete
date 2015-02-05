# Spring Boot working in JBoss EAP 6.x, Wildfly, Tomcat and Standalone


This simple REST web service shows how to package a spring-boot war so that it's both executable and deployable into JBoss, Tomcat, Wildfly.  

It's derived from the Spring spring-boot guide [here](https://github.com/spring-guides/gs-convert-jar-to-war-maven) 

Everything works as expected in Tomcat, and Wildfly.  JBoss EAP 6.x _**did not**_ and needs the code found in the [WebInitializer.java](src/main/java/hello/WebInitializer.java) class (specifically in the `onStartup(...)` method.

More specifically the 

```java
servletRegistration.addMapping("/*");
```
call in that method is what does the trick.

**IMPORTANT**

When running with the embedded container the url is

[http://localhost:8080/greeting?name=bob](http://localhost:8080/greeting?name=bob)

When running deployed as a war the url is:

[http://localhost:8080/gs-convert-jar-to-war-maven-0.1.0/?name=ron](http://localhost:8080/gs-convert-jar-to-war-maven-0.1.0/?name=ron)

Once the JBoss 6.x, 7.x lineage is behind us - hopefully we can remove this cruft.

# Build Notes
If you run `mvn validate` the build will run an ant task to download containers (to the containers directory)
to unpack and test against (manually).  You'll have to supply your own JBoss EAP 6.3.0 since the download
is password protected and does redirects (which ant client doesn't handle).  The tomcat and wildfly
containers should download ok.  If not just download them manually and drop them in the containers
directory by hand.


