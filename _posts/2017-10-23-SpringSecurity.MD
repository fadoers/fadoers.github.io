---
layout: post
title: SpringSecurity
date: 2017-10-23 
tags: java   
---

# **Spring Security**
## **1 Core components**
### **1.1 SecurityContextHolder, SecurityContext,Authentication Objects**
>*Spring Security* 中最核心的对象就是`SecurityContextHolder`, 这是一个保存当前用户所有安全信息的类。在默认情况下， `SecurityContextHolder`用`ThreadLocal`去保存这些信息， 这也就意味着security context在当前线程下任何地方都可以通过静态方法取到。</br>
当然，对于某些应用来说，将安全信息保存于`ThreadLocal`中并不适用。比如， 一个`Swing`客户端需要该程序中的所有线程共享`SecurityContextHolder`，这时可以通过选择`SecurityContextHolder.MODE_INHERITABLETHREADLOCAL`替换默认的`SecurityContextHolder.MODE_THREADLOCAL`实现这一功能。

#### **Obtaining information about the current user**
> 在`SecurityContextHolder`中我们保存了当前用户信息，*Spring Security*使用`Authentication` 对象代表这些信息，你可以用以下的代码在应用中的任何地方获取当前登陆用户的用户名。

```java
Object principal = SecurityContextHolder.getContext().getAuthentication().getPrincipal();

if (principal instanceof UserDetails) {
	String username = ((UserDetails)principal).getUsername();
} else {
	String username = principal.toString();
}
```

### **1.2 The UserDetailsService**
> 当前用户*principal*只是一个`Object`, 在大多数情况下它可以被转为`UserDetails`对象， `UserDetails`是*Spring Security*中的核心接口。可以把它想象成处于储存的真实用户信息和*Spring Seruitry* 的`SecurityContextHolder`需要包含的当前用户之间的适配器。
我们一般会把它转为自己提供的一个实现`UserDetails`接口的对象。</br>
那么`UserDetails`该怎么获取呢，很简单，只需要实现*Spring Security*提供的接口`userDetailsService`并且实现该接口中唯一的方法


```java
UserDetails loadUserByUsername(String username) throws UsernameNotFoundException;
```
> `loadUserByUsername()`方法根据传入的字符串从DB中取得用户数据，然后与输入的密码做比对。需要注意的是，`UserDetailsService`并不拥有用户认证功能，这一部分工作是由`AuthenticationManager`完成的。在大部分情况下，我们通过实现`AuthenticationProvider`接口来提供用户验证

### **1.3 GrantedAuthority**
> 除了*principal*， 另一个重要的方法是`getAuthorities()`，这个方法提供了一个`GrantedAuthority`集合。`GrantedAuthority`代表了一个被包装成与*principal*关联的权限，比如`PRIVILEGE_ADMIN`

## **2. Authentication**

转载请注明：[刘凯的博客](http://fadoers.github.io) » [SpringSecurity](http://fadoers.github.io/2017/03/SpringSecurity/) 