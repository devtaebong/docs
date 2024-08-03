# 컨트롤러 테스트

## `@WebMvcTest`

### @WebMvcTest 어노테이션 기능

`@WebMvcTest` 어노테이션은 웹계층을 테스트할 때 사용된다.
해당 어노테이션은 웹계층 (예: 컨트롤러, 필터, 인터셉터 등)을 자동으로 설정해준다.

#### `@AutoConfigureCache`

- `@AutoConfigureCache`는 테스트 환경에서 캐시 관련 설정을 구성해준다. 이를 통해 캐시를 사용하는 코드가 테스트에서 올바르게 동작하는지 확인할 수 있다.
- 주로 캐시매니저(Cache Manager)를 설정하고, 캐시를 사용하는 컴포넌트들을 테스트할 수 있다.

#### `@AutoConfigureWebMvc`

- `@AutoConfigureWebMvc`는 Spring MVC 설정을 자동으로 구성해준다.
- 이를 통해 DispatcherServlet, 컨트롤러, 뷰리졸버 등과 같은 웹 관련 빈들을 설정할 수 있다.

#### `@AutoConfigureMockMvc`

- `@AutoConfigureMockMvc` 어노테이션은 MockMvc 객체를 자동으로 구성한다.
- MockMvc는 Spring MVC 컨트롤러 테스트 유틸리티로, HTTP 요청과 응답을 모킹하여 실제 서블릿 컨테이너 없이도 컨트롤러를 테스트할 수 있게 해준다.
- 이를 통해 다양한 HTTP 메서드와 요청/응답 데이터를 테스트할 수 있다.



```java
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@BootstrapWith(WebMvcTestContextBootstrapper.class)
@ExtendWith({SpringExtension.class})
@OverrideAutoConfiguration(
    enabled = false
)
@TypeExcludeFilters({WebMvcTypeExcludeFilter.class})
@AutoConfigureCache
@AutoConfigureWebMvc
@AutoConfigureMockMvc
@ImportAutoConfiguration
public @interface WebMvcTest {
    String[] properties() default {};

    @AliasFor("controllers")
    Class<?>[] value() default {};

    @AliasFor("value")
    Class<?>[] controllers() default {};

    boolean useDefaultFilters() default true;

    ComponentScan.Filter[] includeFilters() default {};

    ComponentScan.Filter[] excludeFilters() default {};

    @AliasFor(
        annotation = ImportAutoConfiguration.class,
        attribute = "exclude"
    )
    Class<?>[] excludeAutoConfiguration() default {};
}
```