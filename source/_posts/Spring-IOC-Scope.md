---
title: Spring IOC-Scope
date: 2020-02-24 23:04:51
tags: ["Spring"]
categories: ["Develop","Spring"]
---

### What is IOC Scope?

<!-- more -->

- There are two type scope in IOC.
    1. Singleton
    2. Prototype
        - Request
        - Session
        - Websocket
        - ....

### 1. Singleton

When make Bean in spring, should write @Component or @Controller or @Service and so on and default scope type is Singleton.
~~~java
@Component
public class Single {

}
~~~

### 2. Prototype

If want scope type prototype, should write prototype in @Scope like below.
~~~java
@Component @Scope(value = "prototype")
public class Proto {

}
~~~

### Check

Let's check scope example about above code.

First, configure Single class like this.

~~~java
@Component
public class Single {

    @Autowired
    private Proto proto;

    public Proto getProto() {
        return proto;
    }
}
~~~

Second, configure Prototype class like this.

~~~java
@Component @Scope(value = "prototype")
public class Proto {

    @Autowired
    Single single;
}
~~~

As example above code, Single class type is Singleton and Proto class type is prototype.

Execute code for test like below.
~~~java
@Component
public class ScopeRunner implements ApplicationRunner {

    @Autowired
    ApplicationContext ctx;

    @Override
    public void run(ApplicationArguments args) throws Exception {
        System.out.println("proto");

        System.out.println(ctx.getBean(Proto.class));
        System.out.println(ctx.getBean(Proto.class));
        System.out.println(ctx.getBean(Proto.class));

        System.out.println("single");

        System.out.println(ctx.getBean(Single.class));
        System.out.println(ctx.getBean(Single.class));
        System.out.println(ctx.getBean(Single.class));
    }
}
~~~

As like result, every Singleton class hashcode are same and every prototype code are different.  

~~~
proto
com.example.demo.scope.Proto@71466383
com.example.demo.scope.Proto@46d63dbb
com.example.demo.scope.Proto@4088741b
single
com.example.demo.scope.Single@178270b2
com.example.demo.scope.Single@178270b2
com.example.demo.scope.Single@178270b2
~~~

How about Proto class in Single class?

Let's test.

~~~java
@Component
public class Single {

    @Autowired
    private Proto proto;

    public Proto getProto() {
        return proto;
    }
}
~~~

~~~java
@Component
public class ScopeRunner implements ApplicationRunner {

    @Autowired
    ApplicationContext ctx;
    @Override
    public void run(ApplicationArguments args) throws Exception {

        System.out.println("Proto by single");
        System.out.println(ctx.getBean(Single.class).getProto());
        System.out.println(ctx.getBean(Single.class).getProto());
        System.out.println(ctx.getBean(Single.class).getProto());
    }
}
~~~

The result is like this.
~~~
Proto by single
com.example.demo.scope.Proto@38a1a26
com.example.demo.scope.Proto@38a1a26
com.example.demo.scope.Proto@38a1a26
~~~

Why every Prototype class's hashcode are same even though configuration prototype?

That reason is that the Single class configuration is a Singleton.

When Bean Created, Single class already assigned prototype.

If want Proto class working like prototype in Singleton Bean, should write 'proxyMode' like below.

~~~java
@Component @Scope(value = "prototype", proxyMode = ScopedProxyMode.TARGET_CLASS)
public class Proto {

    @Autowired
    Single single;
}
~~~

The expected result was output.
~~~
Proto by single
com.example.demo.scope.Proto@31ff6309
com.example.demo.scope.Proto@204e90f7
com.example.demo.scope.Proto@20a05b32
~~~
