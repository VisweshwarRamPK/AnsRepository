**21) SPRING BEANS:**

**I) DEFINITION:**



* A Spring bean is an object that is managed by the Spring IoC (Inversion of Control) container. Beans represent objects that Spring creates, configures, and manages during the application's runtime.
* The IoC container is responsible for creating, initializing, configuring, and managing the lifecycle of these beans.

**II) SPRING IOC CONTAINER:**

**Definition: **The IoC container in Spring is responsible for creating, managing, and destroying Spring beans (objects). It also handles dependency injection, which means it automatically provides the objects (beans) that parts of your application needed at that time.

**Key Point: **The IoC container decouples (separates) your code, so your classes don’t have to create the objects they need. Instead, Spring creates and provides those objects, making your code easier to manage and more flexible.

 **There are two types of containers:**



* **BeanFactory**: A basic container.
* **ApplicationContext**: A more advanced container that provides more enterprise-specific functionality like event propagation and declarative mechanisms.

**III) BEANS DEFINITION:**

**XML configuration: Historically, beans were defined in an XML file, where the class and properties of the beans were specified.**

**&lt;bean id="myBean" class="com.example.MyClass"/>**

**Annotations (@Component, @Service, @Repository): In modern Spring applications, beans are usually defined using annotations.**

**@Component**

**public class MyBean {**

**    // Bean implementation**

**}**

**Java-based configuration (@Bean): Beans can also be defined in a <code>@Configuration</code> class using the <code>@Bean</code> annotation.</strong>

**@Configuration**

**public class AppConfig {**

**    @Bean**

**    public MyBean myBean() {**

**        return new MyBean();**

**    }**

**}**

**Use Case: **In modern applications, annotation-based configuration is widely used because it simplifies bean management and reduces boilerplate code.

**IV) DEPENDENCY INJECTION:**

Spring Beans rely on Dependency Injection (DI) for managing dependencies. There are three common types of DI in Spring:



* **Constructor Injection:** Dependencies are passed through the constructor.
* **Setter Injection: **Dependencies are passed through setter methods.
* **Field Injection:** Dependencies are injected directly into fields (using `@Autowired`).

**V) BEAN SCOPE:**

**Definition:** The scope of a bean defines how long the bean lives.

**Common Scopes:**



* **Singleton:** A single instance of the bean is created for the entire Spring application (default scope).
* **Prototype: **A new instance of the bean is created every time the bean is requested.
* **Request**: A single instance is created for each HTTP request (used in web applications).
* **Session**: A single instance is created for each HTTP session.

**Use Case**: Use the singleton scope for stateless services and the prototype scope for stateful components where new instances are required.

**VI) BEAN LIFECYCLE:**

**Instantiation:** The IoC container creates the bean.

**Dependency Injection: **If any dependencies are needed, they are injected into the bean.

**Initialization: **After the bean is created and its dependencies are set, you can add some custom setup if needed (using `@PostConstruct` or an init  method).

**Destruction: **When the bean is no longer needed, Spring can clean it up before it’s destroyed, and you can add custom cleanup logic (using `@PreDestroy` or a special method) to safely release resources.

**VII) AUTOWIRING OF BEANS:**

**@Autowired: **Autowiring is a feature where Spring automatically injects beans into other bean’s field,constructor,setter

**@Qualifier:** If there are multiple beans of the same type, @Qualifier helps you choose the correct bean to inject by specifying its name.

**VIII) USE:**

**Centralized Management**: Spring handles object creation and management, reducing manual setup in your code.

**Dependency Injection**: Automatically injects required dependencies into classes, promoting modular and maintainable code.

**Inversion of Control (IoC)**: The Spring container manages the lifecycle and wiring of beans, reducing tight coupling between components.

**Flexible Configurations**: Beans can be configured using XML, annotations, or Java-based setups, offering flexibility in how beans are defined and managed.

**Scope Management**: Different bean scopes (Singleton, Prototype, Request, Session) control how beans are created and shared, allowing fine-tuned lifecycle management.

**IX) FEATURES: **

**Lifecycle Management:** Spring handles the entire lifecycle of beans, from creation to cleanup, ensuring proper initialization and destruction.

**Dependency Injection: **Automatically injects dependencies into beans, simplifying wiring and reducing manual setup.

**Bean Scopes: **Defines how long beans live and how they are shared, with options like Singleton, Prototype, Request, and Session.

**Bean Configuration:** Beans can be configured using XML, Java-based, or annotation-based methods, offering flexibility in setup.

**Autowiring:** Automatically provides dependencies using annotations like `@Autowired`, and resolves conflicts with `@Qualifier`.

**BeanFactory vs. Application Context:** Two interfaces for bean management, with `ApplicationContext` offering additional features over `BeanFactory`.

**Bean Post-Processors**: Beans that implement `BeanPostProcessor` allow custom logic to be applied to beans before and after initialization.

**X) PROBLEMS SOLVED BY SPRING BEANS:**

**Manual Object Creation:** Automates object creation and management, reducing boilerplate code.

**Dependency Management:** Uses dependency injection to reduce tight coupling and simplify testing.

Implementation of Spring Beans:
Filter Configuration
```java
package com.example.employee.config;

import com.example.employee.filter.CustomFilter;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.boot.web.servlet.FilterRegistrationBean;

@Configuration
public class FilterConfig {
    @Bean
    public FilterRegistrationBean<CustomFilter> loggingFilter() {
        FilterRegistrationBean<CustomFilter> registrationBean = new FilterRegistrationBean<>();
        registrationBean.setFilter(new CustomFilter());
        registrationBean.addUrlPatterns("/employees/*");
        return registrationBean;
    }
}
```
Security Configuration
```java
package com.example.employee.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
public class SpringSecurity {
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .csrf().disable() // Disable CSRF for simplicity
            .authorizeHttpRequests()
            .requestMatchers("/api/employees/**").authenticated()
            .anyRequest().permitAll()
            .and()
            .httpBasic();
        return http.build();
    }

    @Bean
    public UserDetailsService userDetailsService() {
        UserDetails user = User.withDefaultPasswordEncoder()
            .username("admin")
            .password("admin123")
            .roles("ADMIN")
            .build();
        return new InMemoryUserDetailsManager(user);
    }
}
```

