---
layout: post
title: PrintWriter 和 OutputStream
date: 2017-03-22
tag: blog
---

PrintWriter 和 OutputStream 是两个常用的输出流，PrintWriter以字符为单位，传输过程中将字符转换为某种字符集编码的字节数组，字节转换的字符集编码是通过设置setContentTpye或setCharacterEncoding或setLocale等方法实现的。而OutputStream是以字节为单位的，传输的是2进制流。
这样就解释了上一篇getWriter()和getOutputstream()的冲突问题。调用response中的getOutputStream()方法得到的是一个ServletOutputSteam对象，ServletOutputSteam继承的是OutputSteam类。getWriter()方法得到的是一个PrintWriter对象。实际上通过getOutputStream()方法得到的ServletOutputSteam和
通过getWriter()方法得到的PrintWriter是对同一底层进行的封装。

### getWriter()的调用过程：
```java
public PrintWriter getWriter() throws IOException {
	if (this.writer == null) {
		String characterEncoding = getCharacterEncoding();
		this.writer = new ResponsePrintWriter("ISO-8859-1");
	}
	return this.writer;
}
```
```java
private class ResponsePrintWriter extends PrintWriter {
	public ResponsePrintWriter(String paramString)
			throws UnsupportedEncodingException {
		super(new OutputStreamWriter(
				ContentCachingResponseWrapper.this.content, paramString));
	}

	/*...*/
	
}
	
```
```java
public OutputStreamWriter(OutputStream out, String charsetName) throws UnsupportedEncodingException{
	super(out);
	if (charsetName == null)
		throw new NullPointerException("charsetName");
	se = StreamEncoder.forOutputStreamWriter(out, this, charsetName);
}
```	
从源码中可以看出PrintWriter把OutputSteam中的二进制流按照给定的字符编码方式转换成了字符流，所以response传输数据的时候，对于同一个输出流不能同时调用这两种方法。
<br>
转载请注明：[刘凯的博客](http://fadoers.github.io) » [PrintWriter 和 OutputStream](http://fadoers.github.io/2017/03/PrintWriter_OutputStream/)  