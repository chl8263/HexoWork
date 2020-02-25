---
title: Spring IOC-ApplicationEventPublisher
date: 2020-02-24 23:15:25
tags: ["Spring"]
categories: ["Develop","Spring"]
---

### What is ApplicationEventPublisher?

<!-- more -->

- As implementation of Observer pattern, provide interface for event programming.

### 1. Make Event

Event Publisher consist of occur part and receive part and Object to be used for delivery.

First, occur part.

To occur EventPublisher, should use ApplicationEventPublisher object, ApplicationContext has ApplicationEventPublisher object already.

And use publichEvent method with Object to be used for delivery inside.

~~~java
@Component
public class EventRunner implements ApplicationRunner {

    @Autowired
    ApplicationEventPublisher eventPublisher;

    @Override
    public void run(ApplicationArguments args) throws Exception {
        eventPublisher.publishEvent(new MyEvent(this, 100));
    }
}
~~~

Second, The Object to be used for delivery like below code.

In constructor, meaning of source is for can tracking what object occurred.

~~~java
public class MyEvent {

    private int data;

    public MyEvent(Object source, int data){
        this.data = data;
    }

    public int getData(){
        return data;
    }
}
~~~

Third, receive part like below code.

Need to write __@Component__ for register bean and a __@EventListener__ on the method want to receive.
~~~java
@Component
public class MyEventHandler {

    @EventListener
    public void onApplicationEvent(MyEvent myEvent) {
        System.out.println("Event occurred -> " + myEvent.getData());
    }
}
~~~

Then the result like below.

~~~
Event occurred -> 100
~~~



### 2. Handle event

If there are over 2 receive handler, what is order?

Create another handler for test.
~~~java
@Component
public class AnotherHandler {

    @EventListener
    public void handle(MyEvent myEvent){
        System.out.println("Another -> "+myEvent.getData());
    }
}
~~~

Then result is like below.

~~~
Event occurred -> 100
Another -> 100
~~~

If want to give order at each receiver, can write '@Order(Ordered.HIGHEST_PRECEDENCE)'.

~~~java
@Component
public class AnotherHandler {

    @EventListener
    @Order(Ordered.HIGHEST_PRECEDENCE)
    public void handle(MyEvent myEvent){
        System.out.println("Another -> "+myEvent.getData());
    }
}
~~~

Then the result like below.

~~~
Another -> 100
Event occurred -> 100
~~~

When use to thread, need write __@Async__.

~~~java
@Component
public class AnotherHandler {

    @EventListener
    @Async
    public void handle(MyEvent myEvent){
        System.out.println("Current Thread -> " + Thread.currentThread().toString());
        System.out.println("Another -> "+myEvent.getData());
    }
}
~~~

And need write __@EnableAsync__ in Application.java

~~~java
@SpringBootApplication
@EnableAsync // Enable async
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
~~~

Events provided by spring.

- ContextRefreshedEvent : Occurs when create or refresh ApplicationContext.

- ContextStartedEvent : Occurs when receive signal to start() ApplicationContext.

- ContextStoppedEvent : Occurs when receive signal to stop() ApplicationContext.

- ContextClosedEvent : Occurs when remove singleton bean to close() ApplicationContext.

- RequestHandledEvent : Occurs when request HTTP.

Code structure like below.

~~~java
@Component
public class EventRunner implements ApplicationRunner {

    @Autowired
    ApplicationEventPublisher eventPublisher;

    @Override
    public void run(ApplicationArguments args) throws Exception {
        eventPublisher.publishEvent(new MyEvent(this, 100));

        ((ConfigurableApplicationContext)eventPublisher).start();
        ((ConfigurableApplicationContext)eventPublisher).stop();
        ((ConfigurableApplicationContext)eventPublisher).close();
    }
}
~~~

~~~java
@Component
public class AnotherHandler {

    @EventListener
    @Async
    public void handle(MyEvent myEvent){
        System.out.println("Current Thread -> " + Thread.currentThread().toString());
        System.out.println("Another -> "+myEvent.getData());
    }

    @EventListener
    public void handle(ContextRefreshedEvent event){
        System.out.println("Refresh");
    }

    @EventListener
    public void handle(ContextStartedEvent event){
        System.out.println("Start");
    }

    @EventListener
    public void handle(ContextStoppedEvent event){
        System.out.println("Stop");
    }

    @EventListener
    public void handle(ContextClosedEvent event){
        System.out.println("Close");
    }
}
~~~


The result like this.
~~~
Refresh
2020-02-05 00:07:51.660  INFO 2848 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2020-02-05 00:07:51.663  INFO 2848 --- [           main] com.example.demo.Application             : Started Application in 2.354 seconds (JVM running for 3.252)
class com.example.demo.eventPublisher.EventRunner
Current Thread -> Thread[main,5,main]
Event occurred -> 100
Current Thread -> Thread[task-2,5,main]
Another -> 100
Start
Stop
Close
~~~
