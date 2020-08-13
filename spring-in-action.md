spring-in-action



控制器类，使用`@Controller` 进行注释，由Spring组件扫描自动发现，并在Spring应用程序上下文中作为bean进行实例化

如何声明视图控制器（一个只将请求转发给视图的控制器）

```java
// 声明视图控制器
@Configuration
public class WebConfig implements WebMvcConfigurer {
  @Override
  public void addViewControllers(ViewControllerRegistry registry) {
    registry.addViewController("/").setViewName("home");
  }
}
```





` addViewControllers() ` 提供了 `ViewControllerRegistry ` 参数，用来注册一个或多个视图控制器

`addViewController("/")` 这是视图控制器的处理GET请求的路径，该方法返回一个 `ViewControllerRegistration` 对象，在该对象上调用 `setViewName()` 指定home作为应该转发'/'请求的视图





处理数据

> 首先使用 Spring 对 JDBC（Java Database Connectivity）的支持来消除样板代码。然后，将重新使用 JPA（Java Persistence API）处理数据存储库，从而消除更多代码。



















































