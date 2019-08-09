---
layout: post
title:  "@Controller, @Service, @Repository, @Component"
categories: springBoot
tags: springBoot
author: 段雨寒
---

* content
{:toc}

 1. @Controller: 表明一个注解的类是一个"Controller"，也就是控制器，可以把它理解为MVC 模式的Controller 这个角色。这个注解是一个特殊的@Component，允许实现类通过类路径的扫描扫描到。它通常与@RequestMapping 注解一起使用。
 2. @Service: 表明这个带注解的类是一个"Service"，也就是服务层，可以把它理解为MVC 模式中的Service层这个角色，这个注解也是一个特殊的@Component，允许实现类通过类路径的扫描扫描到
 3. @Repository: 表明这个注解的类是一个"Repository",团队实现了JavaEE 模式中像是作为"Data Access Object" 可能作为DAO来使用，当与 PersistenceExceptionTranslationPostProcessor 结合使用时，这样注释的类有资格获得Spring转换的目的。这个注解也是@Component 的一个特殊实现，允许实现类能够被自动扫描到
 4. @Component: 表明这个注释的类是一个组件，当使用基于注释的配置和类路径扫描时，这些类被视为自动检测的候选者。
 5. 也就是说，上面四个注解标记的类都能够通过@ComponentScan 扫描到，上面四个注解最大的区别就是使用的场景和语义不一样，比如你定义一个Service类想要被Spring进行管理，你应该把它定义为@Service 而不是@Controller因为我们从语义上讲，@Service更像是一个服务的类，而不是一个控制器的类，@Component通常被称作组件，它可以标注任何你没有严格予以说明的类，比如说是一个配置类，它不属于MVC模式的任何一层，这个时候你更习惯于把它定义为 @Component。@Controller，@Service，@Repository 的注解上都有@Component，所以这三个注解都可以用@Component进行替换。
	@Configuration 使用@Component 进行原注解，因此@Configuration 类也可以被组件扫描到（特别是使用XML元素）。
