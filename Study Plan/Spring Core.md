# Spring Core

---

# 🚀 **Spring Core - Complete FAANG Level Roadmap**

---

## ✅ 1. **Spring Core Introduction**

- What is Spring Framework?
- Evolution of Spring
- Spring Modules (Core, Data, MVC, AOP, Security, Boot, Batch, etc.)
- Monolithic vs Microservices

> Why Important?
> 
> 
> This is the foundation. Expect interviewers to ask why Spring exists and how it compares to EJB/Struts.
> 

---

## ✅ 2. **IOC (Inversion of Control) & Dependency Injection**

- What is IoC?
- ApplicationContext vs BeanFactory (Differences & Use Cases)
- DI Types:
    - Constructor Injection
    - Setter Injection
    - Field Injection (Why it’s discouraged)
- Bean Lifecycle (Creation, Initialization, Destruction)
- XML Config vs Java Config vs Annotation Config
- Spring Context Refresh Cycle (Internals)

> FAANG Focus:
> 
> 
> You must know the full bean lifecycle including:
> 
- Instantiation (Reflection)
- Dependency Injection Process
- Post Processors (BeanPostProcessor, InstantiationAwareBeanPostProcessor)
- Sequence to remember:

```jsx
1. postProcessBeforeInstantiation() [InstantiationAwareBeanPostProcessor]
2. Instantiation (Reflection → Constructor called)
3. postProcessAfterInstantiation() [InstantiationAwareBeanPostProcessor]
4. Dependency Injection (setters/fields/constructors already resolved)
5. postProcessProperties() [InstantiationAwareBeanPostProcessor]
6. postProcessBeforeInitialization() [BeanPostProcessor]
7. @PostConstruct / afterPropertiesSet() / custom init()
8. postProcessAfterInitialization() [BeanPostProcessor]
```

---

## ✅ 3. **Bean Scopes (Deep Dive)**

- Singleton, Prototype, Request, Session, Global Session
- When to Use Each Scope
- Circular Dependency Handling (Singleton vs Prototype)
- Scope in Multi-threaded Applications (Why prototype in multi-threaded cases)

> FAANG Focus:
> 
> 
> Understand the performance and memory trade-offs of each scope.
> 

---

## ✅ 4. **Bean Lifecycle (Real Internals)**

- `@PostConstruct`, `@PreDestroy`
- Init-method and Destroy-method (XML Config)
- Bean FactoryPostProcessor vs BeanPostProcessor
- `ApplicationContextAware`, `BeanNameAware`, `InitializingBean`, `DisposableBean`

> FAANG Focus:
> 
> 
> Draw a **full lifecycle flowchart** for interviews — this is heavily asked.
> 

---

## ✅ 5. **Spring Core Annotations (Deep Understanding)**

- `@Component`, `@Service`, `@Repository`, `@Controller`
- `@Configuration`, `@Bean`, `@ComponentScan`
- `@Primary`, `@Qualifier`
- `@Lazy`, `@Scope`, `@Value`
- `@Profile`
- `@PropertySource`

> FAANG Focus:
> 
> 
> Explain annotation processing flow (how Spring detects and processes annotations internally).
> 

---

## ✅ 6. **Bean Wiring & Autowiring (Deep Dive)**

- `@Autowired` (byType)
- `@Qualifier` (byName)
- Constructor vs Setter Autowiring vs Field
- Circular Dependency Handling

---

## ✅ 7. **Spring Property Management**

- `application.properties` vs `application.yml`
- External Configuration (Environment Variables, System Properties)
- `@Value` Injection
- PropertySources & Environment Abstraction
- Configuration Binding (`@ConfigurationProperties`)

> FAANG Focus:
> 
> 
> Real-world scenario: Multiple environments (DEV, QA, PROD) and their property management.
> 

---

## ✅ 8. **Event Handling in Spring**

- `ApplicationEvent` and `ApplicationListener`
- Custom Events
- Asynchronous Event Listeners
- Event Multicasting

---

## ✅ 9. **Spring Aware Interfaces (Deep Dive)**

- `BeanNameAware`, `BeanFactoryAware`, `ApplicationContextAware`, `ResourceLoaderAware`
- Real Use Cases in Large Systems

---

## ✅ 10. **FactoryBeans (Core Concept)**

- What is a `FactoryBean`?
- Difference Between BeanFactory and FactoryBean
- When to Use FactoryBean (Examples like SqlSessionFactoryBean)

---

## ✅ 11. **Circular Dependency Problem (Real Analysis)**

- What is Circular Dependency?
- How Spring Handles It
- When Circular Dependency Fails (Constructor Injection)
- Workarounds (`@Lazy`, `ObjectFactory`, `Proxy`, ApplicationContext injection)

---

## ✅ 12. **Post Processors (Master These!)**

- `BeanPostProcessor`
- `BeanFactoryPostProcessor`
- `InstantiationAwareBeanPostProcessor`
- `SmartLifecycle`

> FAANG Focus:
> 
> 
> You should know exactly **when and why** these are invoked in the lifecycle. Real examples like Property Placeholder Resolution.
> 

---

## ✅ 13. **Annotation Processing (Deep Dive)**

- How `@ComponentScan` Works Internally
- Role of `ClassPathBeanDefinitionScanner`
- How Proxying Works (JDK Dynamic Proxy vs CGLIB)
- What is `@Enable` and ImportSelector?
- Embeddable Annotation

> FAANG Focus:
> 
> 
> You should know how annotation processing works from **classpath scanning** to **bean registration**.
> 

---

## ✅ 14. **Spring Profiles (Real-World Use)**

- What is Profile?
- `@Profile` vs Active Profiles in `application.properties`
- Multi-profile Handling

---

## ✅ 15. **Resource Management**

- `ResourceLoader` and `Resource`
- Loading Files from Classpath, FileSystem, URL
- `@PropertySource`

---

## ✅ 16. **Task Scheduling**

- `@Scheduled` and `TaskScheduler`
- Thread Pools for Scheduling
- Cron Expressions in Spring

---

## ✅ 17. **Transaction Management (Core Concepts)**

- `@Transactional` (How it works internally)
- PlatformTransactionManager
- Propagation Levels (FAANG must-know)
- Isolation Levels
- Transaction Rollback Rules
- Declarative vs Programmatic Transactions

---

## ✅ 18. **ApplicationContext Hierarchy**

- Parent-Child Contexts
- Real Scenarios (e.g., WebApplicationContext and Root ApplicationContext)
- Bean Override in Hierarchical Contexts

---

## ✅ 19. **Spring Expression Language (SpEL)**

- SpEL Basics
- Property Access, Method Invocation, Collection Handling
- Real Examples (Injecting Environment Variables)

---

## ✅ 20. **Spring Internationalization (i18n)**

- MessageSource
- Loading Message Bundles
- Locale Resolution

---

## ✅ 21. **Factory Method vs Constructor Injection (Real Analysis)**

---

## ✅ 22. **Proxying (Key FAANG Topic)**

- JDK Dynamic Proxy vs CGLIB
- Why JDK Proxy for Interfaces and CGLIB for Classes
- ProxyFactoryBean

---

## ✅ 23. **Context Refresh Events**

- What happens on Context Refresh?
- Listeners for Context Start, Stop, Close
- Post-refresh Beans Initialization

---

## ✅ 24. **Spring Boot Integration (Just Basics - Focus on Core)**

---

## ✅ 25. **Commonly Asked Spring Core Interview Questions (FAANG level)**

### Conceptual:

- Explain IoC vs DI.
- Explain full Spring Bean Lifecycle.
- What is `BeanPostProcessor`? Use Case?
- Difference between ApplicationContext and BeanFactory.
- How does @Transactional work internally?
- How does `@Autowired` actually work?
- Difference between `@Component`, `@Service`, `@Repository`.
- Explain Circular Dependency and its solutions.
- What happens when Spring Context starts?
- What is ProxyBeanMethods in @Configuration?
- Why Singleton is default scope?
- Difference between FactoryBean and BeanFactory.
- How does `@ComponentScan` work internally?
- How does Spring handle `@Value` injection?

### Scenario-based:

- Multiple beans of same type — how to handle?
- How to load configuration dynamically based on Environment?
- How to refresh properties at runtime?
- How to handle large property files across microservices?
- How to create a custom BeanPostProcessor?

---

# 🔥 **Bonus (For Extra Depth)**

- Spring vs Guice (Why Spring Won)
- Spring Internals (Dependency Injection Graph Build Process)
- Spring 6.x Features (Ahead of Time Processing - AOT)

---

# 🌟 **Study Resources**

| Resource | Link |
| --- | --- |
| Spring Documentation | [https://docs.spring.io](https://docs.spring.io/) |
| Baeldung Spring Core | [https://www.baeldung.com/spring-core](https://www.baeldung.com/spring-core) |
| "Pro Spring" Book (5th Edition) | Highly Recommended |
| Source Code | Read the actual Spring codebase on GitHub |

---