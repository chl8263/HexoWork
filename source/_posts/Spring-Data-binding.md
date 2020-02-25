---
title: Spring Data binding
date: 2020-02-24 23:19:56
tags: ["Spring"]
categories: ["Develop","Spring"]
---

### What is DataBinding?

<!-- more -->


Spring DataBinding is mapping to domain from user input value.

Server read just string for user input value.

So, Need mapping to specific object or data type.

Here is some controller for mapping input value.

~~~java
@RestController
public class EventController {

    @GetMapping("/event/{event}")
    public String getEvent(@PathVariable BindData bindData){
        System.out.println(bindData);
        return bindData.getId().toString();
    }
}
~~~

And BindData object is like that.

~~~java
public class BindData {

    private Integer id;

    private String title;

    public BindData(Integer id){
        this.id = id;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    @Override
    public String toString() {
        return "BindData{" +
                "id=" + id +
                ", title='" + title + '\'' +
                '}';
    }
}
~~~

Test code for above code like below.

~~~java
@RunWith(SpringRunner.class)
@WebMvcTest
public class EventControllerTest {

    @Autowired
    MockMvc mockMvc;

    @Test
    public void getTest() throws Exception{
        mockMvc.perform(get("/event/1"))
                .andExpect(status().isOk())
                .andExpect((ResultMatcher) content().string("1"));
    }
}
~~~

The result is fail.

~~~
Missing URI template variable 'bindData' for method parameter of type BindData]
~~~

In this case, have to notify to spring how can transform data.

First of all, can use PropertyEditorSupport like below code.

~~~java
public class EventEditor extends PropertyEditorSupport {

    @Override
    public String getAsText() {

        BindData binddata = (BindData)getValue();

        return binddata.getId().toString();
    }

    @Override
    public void setAsText(String text) throws IllegalArgumentException {
        setValue(new BindData(Integer.parseInt(text)));
    }
}
~~~

When use PropertyEditorSupport for format data type, can use getAsText() and setAsText().
'getAsText()' method is binding object to string. 'setAsText' method is binding string to object.

However this way has some problem and too old. For example, not thread safe, can not register Bean, just can transform string to object or object to string.

## Converter & Formatter
Converter and Formatter appeared to replace PropertyEditor.

The Converter is converter for type S to T and Thread-safe. Formatter is converter object to String and provide function to multinationalization.

### Converter implementation

Converter can implement two parameter Source and Target. Also Converter is Thread-safe unlike PropertyEditor, so can register it as a Spring bean.

~~~java
public class EventConverter {

    public static class StringToEventConverter implements Converter<String, Event> {
        @Override
        public Event convert(String source){
            return new Event(Integer.parseInt(source));
        }
    }

    public static class EventToStringConverter implements Converter<Event, String>{
        @Override
        public String convert(Event source){
            return source.getId().toString();
        }
    }
}
~~~

Also need register at WebMvcConfigure if use above way Converter.

~~~java
@Configuration
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addFormatters(FormatterRegistry registry) {
        registry.addConverter(new EventConverter.StringToEventConverter());
    }
}
~~~

### Formatter implementation

Formatter receive just one parameter because it just transfer object to string or string to object.

~~~java
public class EventFormatter implements Formatter<Event> {

    @Override
    public Event parse(String text, Locale locale) throws ParseException {
        return new Event(Integer.parseInt(text));
    }

    @Override
    public String print(Event object, Locale locale) {
        return object.getId().toString();
    }
}
~~~

Register Formatter WebMvcConfigurer as like Converter.

~~~java
@Configuration
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addFormatters(FormatterRegistry registry) {
        registry.addFormatter(new EventFormatter());
    }
}
~~~

### Converstion Service

When use Converter and Formatter, registered ConversionService through WebMvcConfigurer.

Real convert at ConversionService and automatically inject as bean at Spring Boot.

~~~java
@Component
public class AppRunner implements ApplicationRunner {

    @Autowired
    ConversionService conversionService;

    @Override
    public void run(ApplicationArguments args) throws Exception {
    System.out.println(conversionService.getClass().toString());
    }
}
~~~

### WebConversionService

WebConversionService which provide Spring boot inject Formatter and Converter automatically.w

So, do not need to write WebMvcConfigurer like above code.

~~~java
@Component
public class EventFormatter implements Formatter<Event> {

    @Override
    public Event parse(String text, Locale locale) throws ParseException {
        return new Event(Integer.parseInt(text));
    }

    @Override
    public String print(Event object, Locale locale) {
        return object.getId().toString();
    }
}
~~~

~~~java
public class EventConverter  {

    @Component
    public static class StringToEventConverter implements Converter<String, Event> {
        @Override
        public Event convert(String source){
            return new Event(Integer.parseInt(source));
        }
    }

    @Component
    public static class EventToStringConverter implements Converter<Event, String>{
        @Override
        public String convert(Event source){
            return source.getId().toString();
        }
    }
}
~~~
