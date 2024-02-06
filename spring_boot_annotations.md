# Spring Boot Annotations

Spring Boot Annotations is a form of metadata that provides data about a program. In other words, annotations are used to provide **supplemental information about a program**.

## @SpringBootApplication

We use this annotation to mark the main class of a Spring Boot application

_@SpringBootApplication_ encapsulates @Configuration, _@EnableAutoConfiguration_, and @ComponentScan annotations with their default attributes.

## @EnableAutoConfiguration

_@EnableAutoConfiguration_, as its name says, enables auto-configuration. It means that **Spring Boot looks for auto-configuration beans** on its classpath and automatically applies them.

## @Required

It applies to the **bean** setter method. It indicates that the annotated bean must be populated at configuration time with the required property, else it throws an exception **BeanInitilizationException**.

## @Autowired

Spring provides annotation-based auto-wiring by providing @Autowired annotation. It is used to autowire spring bean on setter methods, instance variable, and constructor. When we use @Autowired annotation, the spring container auto-wires the bean by matching data-type.

## @Configuration

It is a class-level annotation. The class annotated with @Configuration used by Spring Containers as a source of bean definitions.

## @ComponentScan

It is used when we want to scan a package for beans. It is used with the annotation @Configuration. We can also specify the base packages to scan for Spring Components.

## @Bean

It is a method-level annotation. It is an alternative of XML <bean> tag. It tells the method to produce a bean to be managed by Spring Container.

## @Component

It is a class-level annotation. It is used to mark a Java class as a bean. A Java class annotated with @Component is found during the classpath. The Spring Framework pick it up and configure it in the application context as a **Spring Bean**.

## @Controller

The @Controller is a class-level annotation. It is a specialization of @Component. It marks a class as a web request handler. It is often used to serve web pages. By default, it returns a string that indicates which route to redirect. It is mostly used with @RequestMapping annotation.

## @Service

It is also used at class level. It tells the Spring that class contains the business logic.

## @Repository

It is a class-level annotation. The repository is a DAOs (Data Access Object) that access the database directly. The repository does all the operations related to the database.

## @EnableAutoConfiguration

It auto-configures the bean that is present in the classpath and configures it to run the methods. The use of this annotation is reduced in Spring Boot 1.2.0 release because developers provided an alternative of the annotation, i.e. @SpringBootApplication.

## @SpringBootApplication

It is a combination of three annotations @EnableAutoConfiguration, @ComponentScan, and @Configuration.

References:

- [baeldung.com](https://www.baeldung.com/spring-boot-annotations)
- [javatpoint.com](https://www.javatpoint.com/spring-boot-annotations)
