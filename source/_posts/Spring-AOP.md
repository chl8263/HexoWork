---
title: Spring AOP
date: 2020-02-24 23:22:05
tags: ["Spring"]
categories: ["Develop","Spring"]
---

What is AOP(Aspect-oriented programming)?

<!-- more -->


AOP is programming method that applies common function when necessary outside the developer's code.

#### AOP key technique

* Aspect & Target
* Advice
* Join point & PointCut

#### AOP implement
* Java
    * Aspect J
    * Spring AOP

#### How to implement AOP
* Compile   (Aspect J)
* Load time
* Runtime   (Spring AOP)

#### Spring AOP Features
* Proxy based AOP implement
* Only can adapt Spring bean

AOP using Spring Proxy can make like below code and purpose is time check each method.

First, create interface.

~~~java
public interface EventService {

    void createEvent() throws InterruptedException;

    void publishEvent() throws InterruptedException;

    void deleteEvent();
}
~~~

Second, create class that implement EventService.

~~~java
@Service
public class SimpleEventService implements EventService{
    @Override
    public void createEvent() throws InterruptedException {

        Thread.sleep(1000);
        System.out.println("Create an event");
    }

    @Override
    public void publishEvent() throws InterruptedException {

        Thread.sleep(1000);
        System.out.println("Published an event");
    }

    @Override
    public void deleteEvent() {
        System.out.println("Delete an Event");
    }
}
~~~

And create another class implement EventService and write SimpleEventService at each method and write @Primary for give priority to dependency injection.

~~~java
@Primary
@Component
public class ProxySimpleEventService implements EventService{

    @Autowired
    SimpleEventService simpleEventService;

    @Override
    public void createEvent() throws InterruptedException {

        long begin = System.currentTimeMillis();
        simpleEventService.createEvent();
        System.out.println(System.currentTimeMillis() - begin);
    }

    @Override
    public void publishEvent() throws InterruptedException {

        long begin = System.currentTimeMillis();
        simpleEventService.publishEvent();
        System.out.println(System.currentTimeMillis() - begin);
    }

    @Override
    public void deleteEvent() {

        simpleEventService.deleteEvent();
    }
}
~~~

But this way a little bit cumbersome.

That why Spring AOP appeared.

First add dependency Spring AOP

~~~
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
</dependency>
~~~

Write @Aspect above class.

Want code that wants AOP function at linePerf and write @Around as whether based on annotation or execution.

Also can use @Before that execute before method.

~~~java
@Component
@Aspect
public class PerfAspect {

    //@Around("execution(* com.example..*.EventService.*(..))")
    @Around("@annotation(PerfLogging)")
    public Object linePerf(ProceedingJoinPoint joinPoint) throws Throwable{

        long begin = System.currentTimeMillis();
        Object retVal = joinPoint.proceed();
        System.out.println(System.currentTimeMillis() - begin);

        return retVal;
    }

    @Before("bean(simpleEventService)")
    public void hello(){
        System.out.println("before");
    }
}
~~~
