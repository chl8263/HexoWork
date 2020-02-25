---
title: Spring IOC-Profile
date: 2020-02-24 23:06:14
tags: ["Spring"]
categories: ["Develop","Spring"]
---

### What is IOC Profile?

<!-- more -->


Spring profile is manage bean group.

Can see current active profile using getEnvironment method in ApplicationContext.

- How define profile.
    - Define in class
        - @Configuration @Profile("test")
        - @Component     @Profile("test")
    - Define in method
        - @Bean @Profile("test")


First of all, make interface.        
~~~java
public interface ProRepository {

    public String printState();
}
~~~

Also make TestProRepository.
~~~java
@Repository
public class TestProRepository implements ProRepository {

    @Override
    public String printState() {
        return "Test!!!";
    }
}
~~~

And can use with Configuration class like below.

~~~java
@Configuration
@Profile("test")
public class TestConfiguration {
    @Bean
    public ProRepository proRepository(){
        return new TestProRepository();
    }
}
~~~

Next, should write configuration in VM setting.

![base](/document/Spring/IOCing/IOC/vmSetting.PNG)


Let's Execute code.

Once get Environment from ApplicationContext, use getActiveProfiles which has current active profile and getDefaultProfiles which just default.

~~~java
@Component
public class ProRunner implements ApplicationRunner {

    @Autowired
    ProRepository proRepository;

    @Autowired
    ApplicationContext ctx;

    @Override
    public void run(ApplicationArguments args) throws Exception {
        Environment environment = ctx.getEnvironment();
        System.out.println(Arrays.toString(environment.getActiveProfiles()));
        System.out.println(Arrays.toString(environment.getDefaultProfiles()));

        System.out.println(proRepository.printState());
    }
}
~~~

Result like below.
~~~
[test]
[default]
Test!!!
~~~

But don't have to create configuration class, there is more convenient way.

Just write '@Profile("test")' in class.
~~~java
@Repository
@Profile("test")
public class TestProRepository implements ProRepository {

    @Override
    public String printState() {
        return "Test!!!";
    }
}
~~~

And create another class for how to use profile.

~~~java
@Repository
@Profile("!test")
public class TTProRepositrory implements ProRepository {

    @Override
    public String printState() {
        return "Not test!";
    }
}
~~~

As like above code, can write '@Profile("!test")', it means that can write some operator in Profile annotation.

- Profile Operator
    - ! (not)
    - & (and)
    - | (or)

Current configuration is like '-Dspring.profiles.active="test" ', so the expected result like below.

~~~
[test]
[default]
Test!!!
~~~

If change VM configure ''-Dspring.profiles.active="test222" ' ',so the expected result like below.

~~~
[test22]
[default]
Not test!
~~~
