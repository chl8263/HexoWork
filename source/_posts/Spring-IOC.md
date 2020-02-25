---
title: Spring IOC
date: 2020-01-20 22:37:02
tags: ["Spring"]
categories: ["Develop","Spring"]
---

### What is Spring IOC?

<!-- more -->


IOC : Inversion of control, Rather than creating and using dependent objects directly, inject an object.

- Spring IOC container
    - BeanFactory
    - Center storage of application component
    - Read bean definitions from bean configuration source, configure and serve beans

Make configuration file like the picture below.

{% asset_img container.PNG %}

- Bean
    - The object which manage from Spring IOC container
    - Benefit
        - Manage dependency
        - Scope
            - Singleton
            - Prototype
        - Life cycle interface

Configure using XML file and annotation.

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookService"  --> Enroll class to use bean
          class="com.example.demo.book.BookService"  --> Write class path
          scope="singleton">  --> Write scope singleton or prototype and so on
        <property name="bookRepository" ref="bookRepository"/>
    </bean>

    <bean id="bookRepository"
          class="com.example.demo.book.BookRepository"
    />
</beans>
~~~

In application.xml, property that under the beans tag are taken from 'setBookRepository' in BookService
~~~xml
<property name="bookRepository" ref="bookRepository"/>
~~~
~~~JAVA
@Service
public class BookService {

    private BookRepository bookRepository;

    public void setBookRepository(BookRepository bookRepository){
        this.bookRepository = bookRepository;
    }
}
~~~

~~~java
public class Application {

    public static void main(String[] args) {

        ApplicationContext context = new ClassPathXmlApplicationContext("application.xml"); //Get bean configure xml file
        String [] beanNames = context.getBeanDefinitionNames(); //Get bean names
        System.out.println(beanNames);  

        BookService bookService = (BookService) context.getBean("bookService"); //Get BookService bean in IOC container

        System.out.println(bookService.bookRepository != null); //Check BookRepository in BookService and working IOC
    }
}
~~~

The result is like below code.

~~~
[Ljava.lang.String;@2db7a79b
true

Process finished with exit code 0
~~~

But this way how to manage bean is inconvenient.

So Component-scan has appeared to solve the above method inconvenient.

~~~
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <context:component-scan base-package="com.example.demo"/>
</beans>
~~~

component-scan can scan path within created base-package.

~~~
<context:component-scan base-package="com.example.demo"/>
~~~

Write annotation in class for component-scan.

For example, @component, @Controller, @Service, @Repository

~~~java
@Component // or @Service
public class BookService {

    public BookRepository bookRepository;

    public void setBookRepository(BookRepository bookRepository){
        this.bookRepository = bookRepository;
    }
}

@ Component // or @Repository
public class BookRepository {
}
~~~

But they can't still dependency injection yet.

Write @Autowired or @inject for dependency injection.
~~~java
@Service
public class BookService {
    @Autowired
    public BookRepository bookRepository;

    public void setBookRepository(BookRepository bookRepository){
        this.bookRepository = bookRepository;
    }
}
~~~

So result is like below code and same above one.
~~~
[Ljava.lang.String;@56193c7d
true
~~~

Many developer want write configure using java code, so can write this way instead XML file like below.

~~~java
@Configuration
public class ApplicationConfig {

    @Bean
    public BookService bookService(){
        BookService bookService = new BookService();
        bookService.setBookRepository(bookRepository());
        return bookService;
    }

    @Bean
    public BookRepository bookRepository(){
        return new BookRepository();
    }
}
~~~

Also Can inject in method paremeter
~~~java
    @Bean
    public BookService bookService(BookRepository bookRepository){ //Can inject in method paremeter
        BookService bookService = new BookService();
        bookService.setBookRepository(bookRepository);
        return bookService;
    }
~~~

Of course can use injection using @Autowired, then code like below.

~~~java
@Bean
    public BookService bookService(){
        return new BookService();
    }

    @Bean
    public BookRepository bookRepository(){
        return new BookRepository();
    }
~~~

Also can use to way component-scan like this.

~~~java
@Configuration
@ComponentScan(basePackageClasses = Application.class)
public class ApplicationConfig {

}
~~~

Now see the main method.

~~~java
public class Application {

    public static void main(String[] args) {

        ApplicationContext context = new AnnotationConfigApplicationContext(ApplicationConfig.class);
        String [] beanNames = context.getBeanDefinitionNames();
        System.out.println(beanNames);

        BookService bookService = (BookService) context.getBean("bookService");

        System.out.println(bookService.getBookRepository() != null);
    }
}
~~~

Spring boot can create context if using @SpringBootApplication.

~~~java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
    }
}
~~~
