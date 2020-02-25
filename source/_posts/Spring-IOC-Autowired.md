---
title: Spring IOC-Autowired
date: 2020-02-24 22:59:45
tags: ["Spring"]
categories: ["Develop","Spring"]
---

### What is IOC Autowired?

<!-- more -->


IOC : Inversion of control, Rather than creating and using dependent objects directly, inject an object.

- How to inject using Autowired annotation?
    1. @Primary
    2. List
    3. @Qualifier
    4. Write class name

### 1. @Primary

As BookService like below code. There are repository which extends BookRepository.

~~~java
public interface BookRepository {
}

@Repository
public class EwanBookRepository implements BookRepository {
}

@Repository
public class MyBookRepository implements BookRepository {
}
~~~


Then which BookRepository being inject?.

We can see BookRepository class name from setUp method with @PostConstruct.

~~~java
@Service
public class BookService {

    @Autowired
    private BookRepository bookRepository;

    @PostConstruct
    public void setUp(){
        System.out.println(bookRepository.getClass());
    }    
}
~~~

Result is fail because spring don't know which class inject.

~~~
Exception in thread "task-2" org.springframework.beans.factory.BeanCreationNotAllowedException: Error creating bean with name 'springApplicationAdminRegistrar': Singleton bean creation not allowed while singletons of this factory are in destruction (Do not request a bean from a BeanFactory in a destroy method implementation!)
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:208)
	at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:321)
	at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:207)
	at org.springframework.context.event.AbstractApplicationEventMulticaster.retrieveApplicationListeners(AbstractApplicationEventMulticaster.java:245)
	at org.springframework.context.event.AbstractApplicationEventMulticaster.getApplicationListeners(AbstractApplicationEventMulticaster.java:197)
	at org.springframework.context.event.SimpleApplicationEventMulticaster.multicastEvent(SimpleApplicationEventMulticaster.java:134)
	at org.springframework.context.support.AbstractApplicationContext.publishEvent(AbstractApplicationContext.java:403)
	at org.springframework.context.support.AbstractApplicationContext.publishEvent(AbstractApplicationContext.java:360)
	at org.springframework.boot.autoconfigure.orm.jpa.DataSourceInitializedPublisher.publishEventIfRequired(DataSourceInitializedPublisher.java:99)
	at org.springframework.boot.autoconfigure.orm.jpa.DataSourceInitializedPublisher.access$100(DataSourceInitializedPublisher.java:50)
	at org.springframework.boot.autoconfigure.orm.jpa.DataSourceInitializedPublisher$DataSourceSchemaCreatedPublisher.lambda$postProcessEntityManagerFactory$0(DataSourceInitializedPublisher.java:200)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at java.lang.Thread.run(Thread.java:748)
~~~

So if want enroll which class priority first, write @Primary like below code.

~~~java
@Repository @Primary
public class EwanBookRepository implements BookRepository {
}
~~~

The result is success and can see class name that injected in BookService.

~~~
class com.example.demo.book.EwanBookRepository$$EnhancerBySpringCGLIB$$ab287e3a
~~~

### 2. List

If want get all class that type BookRepository, can inject as List.
~~~java
    @Autowired
    List<BookRepository> bookRepositoryList;

    @PostConstruct
    public void setUp(){
        bookRepositoryList.forEach(x ->
                System.out.println(x.getClass())
        );
    }
~~~

The result like below.

~~~
class com.example.demo.book.EwanBookRepository$$EnhancerBySpringCGLIB$$289e3a54
class com.example.demo.book.MyBookRepository$$EnhancerBySpringCGLIB$$a27f925b
~~~

### 3. Qualifier

Also can use class name in @Qualifier, but be careful first spelling should small letter even though class name is upper case.

~~~java
@Autowired @Qualifier("ewanBookRepository")
    private BookRepository bookRepository;

    @PostConstruct
    public void setUp(){
        System.out.println(bookRepository.getClass());
    }
~~~

The result like below.

~~~
class com.example.demo.book.EwanBookRepository$$EnhancerBySpringCGLIB$$289e3a54
~~~

### 4. Write class name

Can write class name directly, spring can inject that class.

~~~java
@Autowired
    private BookRepository ewanBookRepository;

    @PostConstruct
    public void setUp(){
        System.out.println(ewanBookRepository.getClass());
    }
~~~

The result like below.

~~~
class com.example.demo.book.EwanBookRepository$$EnhancerBySpringCGLIB$$fc17c0d9
~~~

## The Recommended way is @Primary.
