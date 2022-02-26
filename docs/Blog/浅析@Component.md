# 浅析@Component
### [Home](../index)  [Blog](./BlogIndex)
## 一、@Component注解与其他常用注解

|  注解  | 用途  |  
|  ----  | ----  |  
| @Component | 泛指组件，标注一个类为Spring容器的Bean |   
| @Service | 用于标注服务层（Service层）组件 |  
| @Controller | 用于标注表示层（Web层）组件 |  
| @Repository | 用于标注持久层（DAO层）组件 |  

### 1. @Component注解  
@Component是一个通用的构造型注解，表明该类是一个 spring 组件。  
该注解是一个元注解。元注解是可以应用于另一个注解的注解。
该注解支持自动检测类并注册Bean定义，需要将@ComponentScan添加到@Configuration类中。
### 2. 其他常用注解 
@Service, @Controller , @Repository = {@Component + 一些特定的功能}。  
@Service, @Controller , @Repository是@Component的特化（@AliasFor），用于更具体的用例(分别在持久层，服务层和表示层中)。

## 二、@Component与@Bean的区别
两者的目的是一样的，都是注册bean到Spring容器中：  
@Component注解表明一个类会作为组件类，并告知Spring要为这个类创建bean。  
@Bean注解告诉Spring这个方法将会返回一个对象，这个对象要注册为Spring应用上下文中的bean。通常方法体中包含了最终产生bean实例的逻辑。  
两者达成目的的方式不一样：  
@Component通常是通过类路径扫描来自动侦测以及自动装配到Spring容器中。  
```java
@Controller
@RequestMapping(″/web/controller1″)
public class WebController {
    .....
}
```
@Bean注解通常是我们在标有该注解的方法中定义产生这个bean的逻辑。@Bean可以用来实现自定义加载类，比如加载第三方类库中的类。
```java
public class WireThirdLibClass {   
    @Bean  
    public ThirdLibClass getThirdLibClass() {  
        return new ThirdLibClass();  
    }  
} 
```

