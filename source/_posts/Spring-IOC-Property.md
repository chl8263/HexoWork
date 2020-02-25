---
title: Spring IOC-Property
date: 2020-02-24 23:10:52
tags: ["Spring"]
categories: ["Develop","Spring"]
---

What is IOC Scope?

<!-- more -->

Property
- Variable setting value in spring.
- The Environment role is property source setting and get property value.

Property Priority
- ServletConfig parameter
- ServletContext parameter
- JNDI (java:comp/env)
- JVM system property (-Dkey="value)
- JVM system environment value

Create properties file like below.

![base](/document/Spring/IOCing/IOC/property.PNG)

And write annotation '@PropertySource("classpath:/app.properties")'.
~~~java
@SpringBootApplication
@PropertySource("classpath:/app.properties")
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
~~~

Then can get anywhere for example 'environment.getProperty("app.about")'.
~~~java
@Component
public class ProRunner implements ApplicationRunner {

    @Autowired
    ApplicationContext ctx;

    @Override
    public void run(ApplicationArguments args) throws Exception {
        Environment environment = ctx.getEnvironment();

        System.out.println(environment.getProperty("app.about"));
    }
}
~~~

The expected result is like below.

~~~
spring
~~~
