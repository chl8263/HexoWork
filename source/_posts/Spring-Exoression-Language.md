---
title: Spring Exoression Language
date: 2020-02-24 23:20:59
tags: ["Spring"]
categories: ["Develop","Spring"]
---

### What is Spring Expression Language?

<!-- more -->


Spring Expression Language is just expression language in Spring. Supported since spring 3.0.

Several way to Expression Spel, first write in '#{}' literal.

1. Plus Integer.
2. Plus String.
3. Expression Boolean.
4. Get property (using '${ }' literal).
5. Get Bean.
~~~java
@Component
public class SpelRunner implements ApplicationRunner {

    @Value("#{1 + 1}") //Plus Integer.
    int value;

    @Value("#{'hello ' + 'world'}") //Plus String.
    String greeting;

    @Value("#{1 eq 1}") //Expression Boolean.
    boolean trueOrFalse;

    @Value("${my.value}")   //Get property.
    int myValue;

    @Value("#{${my.value} eq 100}") //Expression Boolean of get property.
    boolean isMyValue;

    @Value("#{'spring'}")   //Expression just string
    String spring;

    @Value("#{sample.data}")    //Get Bean.
    int sampleData;

    @Override
    public void run(ApplicationArguments args) throws Exception {
        System.out.println("=============");
        System.out.println(value);
        System.out.println(greeting);
        System.out.println(trueOrFalse);
        System.out.println(myValue);
        System.out.println(isMyValue);
        System.out.println(spring);
        System.out.println(sampleData);
    }
}
~~~

### Actually used

* Value annotation
* @ConditionalOnExpression annotation
* Spring Security
* Spring Data (@Query annotation)
* Thymeleaf
