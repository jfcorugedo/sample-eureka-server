# Service Discovery using Eureka #

## Quick summary ##

This application implements a Service Discovery pattern using Netflix server implementation: [Euraka] (https://github.com/Netflix/eureka).

Instead of using Eureka project on its own, this application uses Spring ecosystem to integrate it into the application.

It uses [Spring Boot](http://projects.spring.io/spring-boot/) to start Spring context and run the application and [Spring Cloud Eureka](https://cloud.spring.io/spring-cloud-netflix/) to integrate Netflix implementation into Spring.

##Version

* Spring Boot 1.4.0
* Spring Cloud 1.1.5

## How do I get set up? ##

In order to transform a common Spring Boot application into an Eureka Server, only three steps are needed:

* Add Spring Cloud dependency:

    <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-eureka-server</artifactId>
    </dependency>

* Enable Eureka initialization during Spring Boot startup using the annotation `@EnableEurekaServer` on the main class:

    @SpringBootApplication
    @EnableEurekaServer
    public class SngDemoEurekaServerApplication {
    ...
    }

* Add some configuration. Two configuration files are needed:

*bootstrap.yml*

    spring:
      application:
        name: eureka-server

*application.yml*

    server:
      port: ${PORT:8000}
    
    eureka:
      client:
        registerWithEureka: false
        fetchRegistry: false
        serviceUrl:
          defaultZone: http://eureka-server:8000/eureka/
    server:
      waitTimeInMsWhenSyncEmpty: 0
      enableSelfPreservation: false
      evictionIntervalTimerInMs: 5000
    instance:
      leaseExpirationDurationInSeconds: 15

### Deployment instructions ###

The application starts as a normal Spring Boot application:

* Run `mvn install` inside the proeject
* Go to `target` folder
* Run `java -jar sng-demo-eureka-server-1.0.0-SNAPSHOT.jar`
* _Optional_: If you're using [STS IDE](https://spring.io/tools/sts/all) you can use a view called `Boot Dashboard` to start/stop any Spring Boot project you have in your workspace