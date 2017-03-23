---
layout: post
title: getOutputStream() has already been called for this response异常出现的原因和解决方法
date: 2017-03-22 
tags: java/exception   
---

    今天在做导出excel功能时遇到了getOutputStream() has already been called for this response异常。
  
    出现这个异常的原因是在response中既调用了getwriter()方法又调用了getOutputStream()方法，而这两个方法是相冲突的。
	
### getOutputStream()方法调用：

```java
OutputStream os = null;
WritableWorkbook wwb = null;
os = response.getOutputStream();
WritableWorkbook wwb = null;
...
wwb.write();
os.flush();
```

### getWriter()方法调用：

```java
//为ajax请求返回验证信息时调用
PrintWriter writer = null;
    try
    {
        writer = response.getWriter();
        writer.write(text);
    }
```

### 解决方法一：

```java
//new一个PrintWriter
ServletOutputStream out = response.getOutputStream();
PrintWriter writer = new PrintWriter(new OutputStreamWriter(out, "utf-8"));
```

### 解决方法二：

```java
//使用PrintStream替代getWriter()
PrintStream print = new PrintStream(os, true, "utf-8");
```

转载请注明：[刘凯的博客](http://fadoers.github.io) » [getOutputStream() has already been called for this response异常出现的原因和解决方法](http://fadoers.github.io/2017/03/outputstream_exception/) 


