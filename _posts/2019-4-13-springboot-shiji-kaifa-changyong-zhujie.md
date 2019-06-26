---
layout: post
title:  "springboot实际开发中常用的注解"
categories: springBoot
tags: springBoot
author: 赵醒醒
---

* content
{:toc}

## @Autowired 与@Resource

@Autowired与@Resource都可以用来装配bean. 都可以写在字段上,或写在setter方法上。
@Autowired默认按类型装配（这个注解是属于spring的），默认情况下必须要求依赖对象必须存在，如果要允许null值，可以设置它的required属性为false，如：@Autowired(required=false) ，如果我们想使用名称装配可以结合@Qualifier注解进行使用，如下：

```
@Autowired()
@Qualifier("demoService")
privateDemoService demoService;
```
@Resource（这个注解是属于J2EE的），默认按照名称进行装配，名称可以通过name属性进行指定，如果没有指定name属性，当注解写在字段上时，默认取字段名进行安装名称查找，如果注解写在setter方法上默认取属性名进行装配。当找不到与名称匹配的bean时才按照类型进行装配。但是需要注意的是，如果name属性一旦指定，就只会按照名称进行装配。

```
@Resource()
privateDemoService demoService;
```

```
@Autowired//默认按type注入
@Qualifier("demoService")//一般作为@Autowired()的修饰用
------------------------------------------------------------------------------
@Resource(name="demoService")//默认按name注入，可以通过name和type属性进行选择性注入
```
------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## @Controller、@RestController、@ResponseBody

@RestController注解相当于@ResponseBody ＋ @Controller合在一起的作用。

1.@responseBody注解的作用是将controller的方法返回的对象通过适当的转换器转换为指定的格式之后，写入到response对象的body区，通常用来返回JSON数据或者是XML数据，需要注意的呢，在使用此注解之后不会再走试图处理器，而是直接将数据写入到输入流中，他的效果等同于通过response对象输出指定格式的数据。
2. 如果需要返回到指定页面，则需要用 @Controller配合视图解析器InternalResourceViewResolver才行。
    如果需要返回JSON，XML或自定义mediaType内容到页面，则需要在对应的方法上加上@ResponseBody注解。
3. @RestController注解，相当于@Controller+@ResponseBody两个注解的结合，返回json数据不需要在方法前面加@ResponseBody注解了，但使用@RestController这个注解，就不能返回jsp,html页面，视图解析器无法解析jsp,html页面

简单理解就是
@Controller 返回页面  
@RestController返回json  
@ResponseBody＋@Controller返回json

------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## @Requestmapping

可以使用@RequestMapping 来映射URL 到控制器类，或者是到Controller 控制器的处理方法上。当@RequestMapping 标记在Controller 类上的时候，里面使用@RequestMapping 标记的方法的请求地址都是相对于类上的@RequestMapping 而言的；当Controller 类上没有标记@RequestMapping 注解时，方法上的@RequestMapping 都是绝对路径。这种绝对路径和相对路径所组合成的最终路径都是相对于根路径“/ ”而言的。
@Requestmapping还有很多用法
[@Requestmapping的其他用法讲的非常详细](https://www.cnblogs.com/jpfss/p/8047628.html)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## @RequestBody
1、@requestBody注解常用来处理content-type不是默认的application/x-www-form-urlcoded编码的内容，比如说：application/json或者是application/xml等。一般情况下来说常用其来处理application/json类型。

2、
通过@requestBody可以将请求体中的JSON字符串绑定到相应的bean上，当然，也可以将其分别绑定到对应的字符串上。
例如说以下情况：
```
$.ajax({
　　　url:"/login",
　　　type:"POST",
　　　data:'{"userName":"admin","pwd","admin123"}',
　　　content-type:"application/json charset=utf-8",
　　　success:function(data){
　　　　　　alert("request success ! ");
　　　}
});

@requestMapping("/login")
public void login(@requestBody String userName,@requestBody String pwd){
System.out.println(userName+" ："+pwd);
}
```

这种情况是将JSON字符串中的两个变量的值分别赋予了两个字符串，但是呢假如我有一个User类，拥有如下字段：
String userName;
String pwd;
那么上述参数可以改为以下形式：@requestBody User user 这种形式会将JSON字符串中的值赋予user中对应的属性上
需要注意的是，JSON字符串中的key必须对应user中的属性名，否则是请求不过去的。

------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## @RequestParam
@RequestParam注解将请求参数绑定到你控制器的方法参数上
@RequestParam 有三个属性：
value：请求参数名（必须配置）
required：是否必需，默认为 true，即 请求中必须包含该参数，如果没有包含，将会抛出异常（可选配置）
defaultValue：默认值，如果设置了该值，required 将自动设为 false，无论你是否配置了required，配置了什么值，都是 false（可选配置）
配置一个属性

```
@RequestParam("") 或 @RequestParam(value="")
```
配置多个属性

```
@RequestParam(value="", required=true, defaultValue="")
```
**网友踩过的坑**
1.可以对传入参数指定参数名 

```
@RequestParam String inputStr  
// 下面的对传入参数指定为aa，如果前端不传aa参数名，会报错  
@RequestParam(value="aa") String inputStr 
```
错误信息： 
HTTP Status 400 - Required String parameter 'aa' is not present 

2.如果用@RequestMapping注解的参数是int基本类型，但是required=false，这时如果不传参数值会报错，因为不传值，会赋值为null给int，这个不可以 

解决方法：  “Consider declaring it as object wrapper for the corresponding primitive type.”建议使用包装类型代替基本类型，如使用“Integer”代替“int”

------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## @PathVariable
@PathVariable 映射 URL 绑定的占位符
通过 @PathVariable 可以将 URL 中占位符参数绑定到控制器处理方法的入参中：URL 中的 {xxx} 占位符可以通过@PathVariable(“xxx“) 绑定到操作方法的入参中。
**SpringMVCTest.java**

```
//@PathVariable可以用来映射URL中的占位符到目标方法的参数中
@RequestMapping("/testPathVariable/{id}")
    public String testPathVariable(@PathVariable("id") Integer id)
    {
        System.out.println("testPathVariable:"+id);
        return SUCCESS;
    }
```

**index.jsp**

```
<a href="springmvc/testPathVariable/1">testPathVariable</a>
```
