# Java SSRF跨站请求伪造文档

* [java-net ssrf](#java-net-ssrf)
* [springframework ssrf](#springframework-ssrf)

格式：namespace;type;subtypes;names;signature;ext;input;additionalTaintStep;additionalTaintStepInput;additionalTaintStep1;additionalTaintStepInput1...


namespace：包名
type：类名
names：触发漏洞方法名
input：触发漏洞方法名的形参位置
additionalTaintStep：依赖的污点


sinks:

java-net:

```java
java.net;URL;false;[openConnection, openStream];;;Argument[-1];java.net.URL(String);Argument[0]

java.net;URLClassLoader;false;[loadClass, getResourceAsStream, findResource, getResource];;;Argument[-1];java.net.URLClassLoader(URL[]);Argument[0];java.net.URL(String);Argument[0]
java.net;URLClassLoader;false;[loadClass, getResourceAsStream, findResource, getResource];;;Argument[-1];java.net.URLClassLoader(URL[], ClassLoader);Argument[0];java.net.URL(String);Argument[0]
java.net;URLClassLoader;false;[loadClass, getResourceAsStream, findResource, getResource];;;Argument[-1];java.net.URLClassLoader(URL[],ClassLoader,URLStreamHandlerFactory);Argument[0];java.net.URL(String);Argument[0]
java.net;URLClassLoader;false;[loadClass, getResourceAsStream, findResource, getResource];;;Argument[-1];java.net.URLClassLoader(String,URL[],ClassLoader);Argument[1];java.net.URL(String);Argument[0]
java.net;URLClassLoader;false;[loadClass, getResourceAsStream, findResource, getResource];;;Argument[-1];java.net.URLClassLoader(String,URL[],ClassLoader,URLStreamHandlerFactory);Argument[1];java.net.URL(String);Argument[0]


java.net;URLClassLoader;false;[loadClass, getResourceAsStream, findResource, getResource];;;Argument[-1];java.net.URLClassLoader.newInstance(URL[]);Argument[0];java.net.URL(String);Argument[0]
java.net;URLClassLoader;false;[loadClass, getResourceAsStream, findResource, getResource];;;Argument[-1];java.net.URLClassLoader.newInstance(URL[],ClassLoader);Argument[0];java.net.URL(String);Argument[0]

java.net.http;HttpRequest;false;[newBuilder];;;Argument[0];java.net.URI.create(String);Argument[0]	# jdk11
java.net.http;HttpRequest.Builder;false;[uri];;;Argument[0];java.net.URI.create(String);Argument[0]	# jdk11
```
java.net.URI.create(String);Argument[0] 应该做为一个全局污点

springframework:

org.springframework.web.client.RestTemplate 属于 spring-web模块
```java
org.springframework.web.client;RestTemplate;false;[put，delete,exchange,execute,getForEntity,getForObject,headForHeaders,optionsForAllow,patchForObject,postForEntity,postForLocation,postForObject];;;Argument[0]	
org.springframework.web.client;RestTemplate;false;[put，delete,doExecute,execute,getForEntity,getForObject,headForHeaders,optionsForAllow,patchForObject,postForEntity,postForLocation,postForObject];;;Argument[0];java.net.URI.create(String);Argument[0]
org.springframework.web.client;RestTemplate;false;[exchange];;;Argument[0];org.springframework.http.RequestEntity<T>(...,URI,...);Argument[ParameterType = URI]  # 创建RequestEntity对象，URI形参位置
```


## Java net ssrf

java.net.URL 支持的协议：file、ftp、http、https、jar、mailto、netdoc



```java
import java.net.URL;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.net.http.HttpResponse.BodyHandlers;

public void badJavaNetURLSSRF(HttpServletRequest request) throws Exception {
	String requestUrl = request.getParameter("url");
	URL xxx = new URL(requestUrl);
	xxx.openConnection();  //bad
	xxx.openStream();  //bad
}

public void badJavaNetURLClassLoaderSSRF(HttpServletRequest request) throws Exception {
	String requestUrl = request.getParameter("url");
	URL[] urls = new URL[]{xxx};
	URLClassLoader urlClassLoader = URLClassLoader.newInstance(urls);
	urlClassLoader.findResource("test");  //bad
	urlClassLoader.loadClass("aaa");  //bad
}

public void badJavaNetHttpRequestSSRF(HttpServletRequest request) throws Exception {
	String requestUrl = request.getParameter("url");
	HttpClient client = HttpClient.newHttpClient();
	HttpRequest request = HttpRequest.newBuilder().uri(URI.create(requestUrl)).build();	//bad
	client.sendAsync(request, BodyHandlers.ofString()).thenApply(HttpResponse::body).thenAccept(System.out::println).join();
}
```

## springframework ssrf


```java
import java.net.URI;
import org.springframework.web.client.RestTemplate;

public void badRestTemplateSSRF(HttpServletRequest request) throws Exception {
	String requestUrl = request.getParameter("url");
	RestTemplate restTemplate = new RestTemplate();
	restTemplate.delete(requestUrl);	//bad
}

public void badRestTemplateUriSSRF(HttpServletRequest request) throws Exception {
	String requestUrl = request.getParameter("url");
	RestTemplate restTemplate = new RestTemplate();
	restTemplate.delete(URI.create(requestUrl));	//bad
}
```
