## Spring Bean

### Spring Bean 이란?
 * Spring IoC 컨테이너가 관리하는 자바 객체를 Bean 이라고 부른다.
 * Spring 에서는 POJO(Plain Old Object)를 beans 라고 부른다.

### Bean 을 IoC 컨테이너에 등록하는 방법

(1) Annotation 을 사용하는 방법
* Bean을 등록하기 위해서는 @Component Annotation 을 사용한다. 
* 이 경우 Spring 이 Annotation 을 확인하고 자체적으로 Bean 으로 등록한다.
* 직접 @Component 를 작성하는 것 이외에도, 스테레오 타입인 @Controller, @Service, @Repository 와 같은 Annotation 들도 자동으로 스캔하여 빈에 등록된다.
   * @RestController 또한 @Controller + @ResponseBody 를 합친 것이므로 동일하게 Bean 등록이 된다.  

```java
@Controller
public class ExController {
    @GetMapping("ex")
    public String ex (Model model) {
        model.addAttribute("data","This is data");
        return "ex";
    }
}
```
위의 예시와 같이 등록 가능하다.
* @Controller 어노테이션을 살펴보면 아래와 같이 @Component 어노테이션을 포함하고 있는 모습을 확인할 수 있다.
```java
  @Target({ElementType.TYPE})
  @Retention(RetentionPolicy.RUNTIME)
  @Documented
  @Component 
  public @interface Controller {

	/**
	 * The value may indicate a suggestion for a logical component name,
	 * to be turned into a Spring bean in case of an autodetected component.
	 * @return the suggested component name, if any (or empty String otherwise)
	 */
	@AliasFor(annotation = Component.class)
	String value() default "";

}
```

(2) Bean Configuration File 에 직접 Bean 등록하는 방법
* @Configuration 어노테이션과 @Bean 어노테이션을 이용하여 Bean 을 등록할 수 있다.
* @Configuration 이 붙은 파일 내에서 @Bean 어노테이션을 사용해서 빈을 직접 등록 가능하다.
* @Bean 을 사용하여 수동으로 등록할 때에는 해당 메서드 이름이 빈 이름으로 결정된다.

```java
@Configuration
public class ExConfig {
    
    @Bean
    public FilterRegistrationBean logFilter(){
        
    }
}
```
위의 예시와 같이 등록할 수 있다.

* Spring 에서는 @Component 스캔을 통해 자동으로 Bean 등록을 하는 방식을 권장한다.
* Spring 에서는 Main App 클래스에서 @ComponentScan 어노테이션을 사용해서 등록해야 하며, Spring Boot 환경에서는 디폴트로 존재하는 @SpringBootApplication에 @ComponentScan 어노테이션이 포함되어 있다.
---
@SpringBootApplication
```java
@Target(value = {ElementType.TYPE})
@Retention(value = RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = {
        @ComponentScan.Filter(type = FilterType.CUSTOM, classes = {TypeExcludeFilter.class}),
        @ComponentScan.Filter(type = FilterType.CUSTOM, classes = {AutoConfigurationExcludeFilter.class})})
public @interface SpringBootApplication {

  @AliasFor(annotation = EnableAutoConfiguration.class)
  public Class<?>[] exclude() default {};

  @AliasFor(annotation = EnableAutoConfiguration.class)
  public String[] excludeName() default {};

  @AliasFor(annotation = ComponentScan.class, attribute = "basePackages")
  public String[] scanBasePackages() default {};

  @AliasFor(annotation = ComponentScan.class, attribute = "basePackageClasses")
  public Class<?>[] scanBasePackageClasses() default {};

  @AliasFor(annotation = ComponentScan.class, attribute = "nameGenerator")
  public Class<? extends BeanNameGenerator> nameGenerator() default BeanNameGenerator.class;

  @AliasFor(annotation = Configuration.class)
  public boolean proxyBeanMethods() default true;
}
```
---
### 참조
 * [스프링 빈(Bean)이란?](https://mozzi-devlog.tistory.com/19)
 * [스프링 빈(Spring Bean)이란? 개념 정리](https://melonicedlatte.com/2021/07/11/232800.html)