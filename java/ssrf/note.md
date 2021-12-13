# Java SSRF跨站请求伪造文档

* [java-net ssrf](#java-net ssrf)

格式：namespace;type;subtypes;names;signature;ext;input;additionalTaintStep;additionalTaintStepInput;additionalTaintStep1;additionalTaintStepInput1...

sinks:

java-net:

```
java.net;URL;false;[openConnection, openStream];;;Argument[-1];java.net.URL(String);Argument[0]

java.net;URLClassLoader;false;[loadClass, getResourceAsStream, findResource, getResource];;;Argument[-1];java.net.URLClassLoader(URL[]);Argument[0];java.net.URL(String);Argument[0]
java.net;URLClassLoader;false;[loadClass, getResourceAsStream, findResource, getResource];;;Argument[-1];java.net.URLClassLoader(URL[], ClassLoader);Argument[0];java.net.URL(String);Argument[0]
java.net;URLClassLoader;false;[loadClass, getResourceAsStream, findResource, getResource];;;Argument[-1];java.net.URLClassLoader(URL[],ClassLoader,URLStreamHandlerFactory);Argument[0];java.net.URL(String);Argument[0]
java.net;URLClassLoader;false;[loadClass, getResourceAsStream, findResource, getResource];;;Argument[-1];java.net.URLClassLoader(String,URL[],ClassLoader);Argument[1];java.net.URL(String);Argument[0]
java.net;URLClassLoader;false;[loadClass, getResourceAsStream, findResource, getResource];;;Argument[-1];java.net.URLClassLoader(String,URL[],ClassLoader,URLStreamHandlerFactory);Argument[1];java.net.URL(String);Argument[0]


java.net;URLClassLoader;false;[loadClass, getResourceAsStream, findResource, getResource];;;Argument[-1];java.net.URLClassLoader.newInstance(URL[]);Argument[0];java.net.URL(String);Argument[0]
java.net;URLClassLoader;false;[loadClass, getResourceAsStream, findResource, getResource];;;Argument[-1];java.net.URLClassLoader.newInstance(URL[],ClassLoader);Argument[0];java.net.URL(String);Argument[0]
```


## Java net ssrf

```java
import java.net.URL;

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
```
