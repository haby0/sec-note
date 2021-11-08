# Java XML external entity (XXE) injection文档

* [Commons-Digester3 XXE注入](#Commons-Digester3-XXE注入)
* [Commons-Digester XXE注入](#Commons-Digester-XXE注入)
* [Tomcat-Digester XXE注入](#Tomcat-Digester-XXE注入)
* [DocumentHelper XXE注入](#DocumentHelper-XXE注入)
* [Validator XXE注入](#Validator-XXE注入)
* [XMLDecoder XXE注入](#XMLDecoder-XXE注入)
* [DocumentBuilder XXE注入](#DocumentBuilder-XXE注入)
* [jdom2-SAXBuilder XXE注入](#jdom2-SAXBuilder-XXE注入)
* [jdom-SAXBuilder XXE注入](#jdom-SAXBuilder-XXE注入)
* [SAXParser XXE注入](#SAXParser-XXE注入)
* [SAXReader XXE注入](#SAXReader-XXE注入)
* [XMLReader XXE注入](#XMLReader-XXE注入)
* [Transformer XXE注入](#Transformer-XXE注入)
* [TransformerFactory XXE注入](#TransformerFactory-XXE注入)
* [SAXTransformerFactory XXE注入](#SAXTransformerFactory-XXE注入)
* [SchemaFactory XXE注入](#SchemaFactory-XXE注入)
* [Unmarshaller XXE注入](#Unmarshaller-XXE注入)
* [XPathExpression XXE注入](#XPathExpression-XXE注入)
* [Persister XXE注入](#Persister-XXE注入)

sinks:

Commons-Digester3:

```
org.apache.commons.digester3.Digester;parse(File file);<T> T
org.apache.commons.digester3.Digester;parse(InputSource input);<T> T
org.apache.commons.digester3.Digester;parse(InputStream input);<T> T
org.apache.commons.digester3.Digester;parse(Reader reader);<T> T
org.apache.commons.digester3.Digester;parse(String uri);<T> T
org.apache.commons.digester3.Digester;parse(URL url);<T> T
org.apache.commons.digester3.Digester;asyncParse(final File file);<T> T
org.apache.commons.digester3.Digester;asyncParse(InputSource input);<T> T
org.apache.commons.digester3.Digester;asyncParse(InputStream input);<T> T
org.apache.commons.digester3.Digester;asyncParse(Reader reader);<T> T
org.apache.commons.digester3.Digester;asyncParse(String uri);<T> T
org.apache.commons.digester3.Digester;asyncParse(URL url);<T> T
```

Commons-Digester:

```
org.apache.commons.digester.Digester;parse(File file);Object
org.apache.commons.digester.Digester;parse(InputSource input);Object
org.apache.commons.digester.Digester;parse(InputStream input);Object
org.apache.commons.digester.Digester;parse(Reader reader);Object
org.apache.commons.digester.Digester;parse(String uri);Object
org.apache.commons.digester.Digester;parse(URL url);Object
```

Tomcat-Digester:

```
org.apache.tomcat.util.digester.Digester;parse(File file);Object
org.apache.tomcat.util.digester.Digester;parse(InputSource input);Object
org.apache.tomcat.util.digester.Digester;parse(InputStream input);Object
```

DocumentHelper:

```
org.dom4j.DocumentHelper;parseText(String text);Document
```

Validator:

```
javax.xml.validation.Validator;validate(Source source);void
```

XMLDecoder:

```
java.beans.XMLDecoder;readObject();Object
```

DocumentBuilder:

```
javax.xml.parsers.DocumentBuilder;parse(InputStream is);Document
javax.xml.parsers.DocumentBuilder;parse(InputStream is, String systemId);Document
javax.xml.parsers.DocumentBuilder;parse(String uri);Document
javax.xml.parsers.DocumentBuilder;parse(File f);Document
javax.xml.parsers.DocumentBuilder;parse(InputSource is);Document
```

jdom-SAXBuilder:

```
org.jdom.input.SAXBuilder;build(org.w3c.dom.Document domDocument);Document
org.jdom.input.SAXBuilder;build(org.w3c.dom.Element domElement);Document
```

jdom2-SAXBuilder:

```
org.jdom2.input.SAXBuilder;build(InputSource in);Document
org.jdom2.input.SAXBuilder;build(InputStream in);Document
org.jdom2.input.SAXBuilder;build(File file);Document
org.jdom2.input.SAXBuilder;build(URL url);Document
org.jdom2.input.SAXBuilder;build(InputStream in, String systemId);Document
org.jdom2.input.SAXBuilder;build(Reader characterStream);Document
org.jdom2.input.SAXBuilder;build(Reader characterStream, String systemId);Document
org.jdom2.input.SAXBuilder;build(String systemId);Document
```

SAXParser:

```
javax.xml.parsers.SAXParser;parse(InputStream is, HandlerBase hb);void
javax.xml.parsers.SAXParser;parse(InputStream is, HandlerBase hb, String systemId);void
javax.xml.parsers.SAXParser;parse(InputStream is, DefaultHandler dh);void
javax.xml.parsers.SAXParser;parse(InputStream is, DefaultHandler dh, String systemId);void
javax.xml.parsers.SAXParser;parse(String uri, HandlerBase hb);void
javax.xml.parsers.SAXParser;parse(String uri, DefaultHandler dh);void
javax.xml.parsers.SAXParser;parse(File f, HandlerBase hb);void
javax.xml.parsers.SAXParser;parse(File f, DefaultHandler dh);void
javax.xml.parsers.SAXParser;parse(InputSource is, HandlerBase hb);void
javax.xml.parsers.SAXParser;parse(InputSource is, DefaultHandler dh);void
```

SAXReader:

```
org.dom4j.io.SAXReader;read(File file);Document
org.dom4j.io.SAXReader;read(URL url);Document
org.dom4j.io.SAXReader;read(String systemId);Document
org.dom4j.io.SAXReader;read(InputStream in);Document
org.dom4j.io.SAXReader;read(Reader reader);Document
org.dom4j.io.SAXReader;read(InputStream in, String systemId);Document
org.dom4j.io.SAXReader;read(Reader reader, String systemId);Document
org.dom4j.io.SAXReader;read(InputSource in);Document
```

XMLReader:

```
org.xml.sax.XMLReader;parse(InputSource input);void
org.xml.sax.XMLReader;parse(String systemId);void
```

Transformer:

```
javax.xml.transform.Transformer;transform(Source xmlSource, Result outputTarget);void
```

TransformerFactory:

```
javax.xml.transform.TransformerFactory;newTransformer(Source source);Transformer
```

SAXTransformerFactory(TransformerFactory子类):

```
javax.xml.transform.sax.SAXTransformerFactory;newTransformer(Source source);Transformer
javax.xml.transform.sax.SAXTransformerFactory;newTransformerHandler(Source src);TransformerHandler
javax.xml.transform.sax.SAXTransformerFactory;newTransformerHandler(Templates templates);TransformerHandler
javax.xml.transform.sax.SAXTransformerFactory;newXMLFilter(Source src);XMLFilter
javax.xml.transform.sax.SAXTransformerFactory;newXMLFilter(Templates templates);XMLFilter
```

SchemaFactory:

```
javax.xml.validation.SchemaFactory;newSchema(Source schema);Schema
javax.xml.validation.SchemaFactory;newSchema(File schema);Schema
javax.xml.validation.SchemaFactory;newSchema(URL schema);Schema
javax.xml.validation.SchemaFactory;newSchema(Source[] schemas);Schema
```

Unmarshaller:

```
javax.xml.bind.Unmarshaller;unmarshal(java.io.File f);Object
javax.xml.bind.Unmarshaller;unmarshal(java.io.InputStream is);Object
javax.xml.bind.Unmarshaller;unmarshal(Reader reader);Object
javax.xml.bind.Unmarshaller;unmarshal(java.net.URL url);Object
javax.xml.bind.Unmarshaller;unmarshal(org.xml.sax.InputSource source);Object
javax.xml.bind.Unmarshaller;unmarshal(org.w3c.dom.Node node);Object
javax.xml.bind.Unmarshaller;unmarshal(org.w3c.dom.Node node, Class<T> declaredType);Object
javax.xml.bind.Unmarshaller;unmarshal(javax.xml.transform.Source source);Object
javax.xml.bind.Unmarshaller;unmarshal(javax.xml.transform.Source source, Class<T> declaredType);Object
javax.xml.bind.Unmarshaller;unmarshal(javax.xml.stream.XMLStreamReader reader);Object
javax.xml.bind.Unmarshaller;unmarshal(javax.xml.stream.XMLStreamReader reader, Class<T> declaredType);Object
javax.xml.bind.Unmarshaller;unmarshal(javax.xml.stream.XMLEventReader reader);Object
javax.xml.bind.Unmarshaller;unmarshal(javax.xml.stream.XMLEventReader reader, Class<T> declaredType);Object
```

XPathExpression:

```
javax.xml.xpath.XPathExpression;evaluate(InputSource source, QName returnType);Object
javax.xml.xpath.XPathExpression;evaluate(InputSource source);String
```

Persister:

```
org.simpleframework.xml.core.Persister;read(Class<? extends T> type, String source);<T> T
org.simpleframework.xml.core.Persister;read(Class<? extends T> type, File source);<T> T
org.simpleframework.xml.core.Persister;read(Class<? extends T> type, InputStream source);<T> T
org.simpleframework.xml.core.Persister;read(Class<? extends T> type, Reader source);<T> T
org.simpleframework.xml.core.Persister;read(Class<? extends T> type, InputNode source);<T> T
org.simpleframework.xml.core.Persister;read(Class<? extends T> type, String source, boolean strict);<T> T
org.simpleframework.xml.core.Persister;read(Class<? extends T> type, File source, boolean strict);<T> T
org.simpleframework.xml.core.Persister;read(Class<? extends T> type, InputStream source, boolean strict);<T> T
org.simpleframework.xml.core.Persister;read(Class<? extends T> type, Reader source, boolean strict);<T> T
org.simpleframework.xml.core.Persister;read(Class<? extends T> type, InputNode node, boolean strict);<T> T
org.simpleframework.xml.core.Persister;read(Class<? extends T> type, InputNode node, Session session);<T> T
org.simpleframework.xml.core.Persister;read(Class<? extends T> type, InputNode node, Context context);<T> T
org.simpleframework.xml.core.Persister;read(T value, String source);<T> T
org.simpleframework.xml.core.Persister;read(T value, File source);<T> T
org.simpleframework.xml.core.Persister;read(T value, InputStream source);<T> T
org.simpleframework.xml.core.Persister;read(T value, Reader source);<T> T
org.simpleframework.xml.core.Persister;read(T value, InputNode source);<T> T
org.simpleframework.xml.core.Persister;read(T value, String source, boolean strict);<T> T
org.simpleframework.xml.core.Persister;read(T value, File source, boolean strict);<T> T
org.simpleframework.xml.core.Persister;read(T value, InputStream source, boolean strict);<T> T
org.simpleframework.xml.core.Persister;read(T value, Reader source, boolean strict);<T> T
org.simpleframework.xml.core.Persister;read(T value, InputNode node, boolean strict);<T> T
org.simpleframework.xml.core.Persister;read(T value, InputNode node, Session session);<T> T
org.simpleframework.xml.core.Persister;read(T value, InputNode node, Context context);<T> T
org.simpleframework.xml.core.Persister;validate(Class type, String source);boolean
org.simpleframework.xml.core.Persister;validate(Class type, File source);boolean
org.simpleframework.xml.core.Persister;validate(Class type, InputStream source);boolean
org.simpleframework.xml.core.Persister;validate(Class type, Reader source);boolean
org.simpleframework.xml.core.Persister;validate(Class type, InputNode source);boolean
org.simpleframework.xml.core.Persister;validate(Class type, String source, boolean strict);boolean
org.simpleframework.xml.core.Persister;validate(Class type, File source, boolean strict);boolean
org.simpleframework.xml.core.Persister;validate(Class type, InputStream source, boolean strict);boolean
org.simpleframework.xml.core.Persister;validate(Class type, Reader source, boolean strict);boolean
org.simpleframework.xml.core.Persister;validate(Class type, InputNode node, boolean strict);boolean
org.simpleframework.xml.core.Persister;validate(Class type, InputNode node, Session session);boolean
org.simpleframework.xml.core.Persister;validate(Class type, InputNode node, Context context);boolean
```


## Commons-Digester3 XXE注入


`mvnrepository.com`最新版本更新到3.2,该组件所有版本目前都存在问题.

```pom
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-digester3</artifactId>
    <version>3.2</version>
</dependency>
```

```java
import org.apache.commons.digester3.Digester;

public void badDigester(HttpServletRequest request, HttpServletResponse response) throws Exception {
		ServletInputStream servletInputStream = request.getInputStream();
		Digester digester = new Digester();
		digester.parse(servletInputStream); //实际调用org.xml.sax.XMLReader解析xml数据
}


public void okDigester(HttpServletRequest request, HttpServletResponse response) throws Exception {
		ServletInputStream servletInputStream = request.getInputStream();
		Digester digester = new Digester();
        digester.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true);
		digester.setFeature("http://xml.org/sax/features/external-general-entities", false);
		digester.setFeature("http://xml.org/sax/features/external-parameter-entities", false);
		digester.parse(servletInputStream);
}
```

## Commons-Digester XXE注入

`mvnrepository.com`最新版本更新到2.1,该组件所有版本目前都存在问题.

```pom
<dependency>
    <groupId>commons-digester</groupId>
    <artifactId>commons-digester</artifactId>
    <version>2.1</version>
</dependency>
```

```java
import org.apache.commons.digester.Digester;

public void badDigester(HttpServletRequest request, HttpServletResponse response) throws Exception {
		ServletInputStream servletInputStream = request.getInputStream();
		Digester digester = new Digester();
		digester.parse(servletInputStream); //实际调用org.xml.sax.XMLReader解析xml数据
}


public void okDigester(HttpServletRequest request, HttpServletResponse response) throws Exception {
		ServletInputStream servletInputStream = request.getInputStream();
		Digester digester = new Digester();
        digester.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true);
		digester.setFeature("http://xml.org/sax/features/external-general-entities", false);
		digester.setFeature("http://xml.org/sax/features/external-parameter-entities", false);
		digester.parse(servletInputStream);
}
```

## Tomcat-Digester XXE注入

apache tomcat自己实现了Digester解析xml文件, 使用该类时存在xxe注入漏洞.

```java
import org.apache.tomcat.util.digester.Digester;

public void badDigester(HttpServletRequest request, HttpServletResponse response) throws Exception {
		ServletInputStream servletInputStream = request.getInputStream();
		Digester digester = new Digester();
		digester.parse(servletInputStream); //实际调用org.xml.sax.XMLReader解析xml数据
}


public void okDigester(HttpServletRequest request, HttpServletResponse response) throws Exception {
		ServletInputStream servletInputStream = request.getInputStream();
		Digester digester = new Digester();
        digester.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true);
		digester.setFeature("http://xml.org/sax/features/external-general-entities", false);
		digester.setFeature("http://xml.org/sax/features/external-parameter-entities", false);
		digester.parse(servletInputStream);
}
```

## DocumentHelper XXE注入

低于2.1.1版本的存在漏洞

```pom
<dependency>
	<groupId>org.dom4j</groupId>
	<artifactId>dom4j</artifactId>
	<version>2.0.1</version>
</dependency>
```

```java
import org.dom4j.Document;
import org.dom4j.DocumentHelper;

public void badDocumentHelper(HttpServletRequest request) throws Exception {
	BufferedReader br = request.getReader();
	String str = "";
	StringBuilder listString = new StringBuilder();
	while ((str = br.readLine()) != null) {
		listString.append(str).append("\n");
	}
	Document document = DocumentHelper.parseText(listString.toString());
}
```

## Validator XXE注入

JDK原生, CVE-2019-12415中的sink

```java
import javax.xml.transform.stream.StreamSource;
import javax.xml.validation.Schema;
import javax.xml.validation.SchemaFactory;
import javax.xml.validation.Validator;

public void badValidator(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	SchemaFactory factory = SchemaFactory.newInstance("http://www.w3.org/2001/XMLSchema");
	Schema schema = factory.newSchema();
	Validator validator = schema.newValidator();
	StreamSource source = new StreamSource(servletInputStream);
	validator.validate(source);
}


public void ok1Validator(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	SchemaFactory factory = SchemaFactory.newInstance("http://www.w3.org/2001/XMLSchema");
    factory.setFeature("http://javax.xml.XMLConstants/feature/secure-processing", true);
	Schema schema = factory.newSchema();
	Validator validator = schema.newValidator();
	StreamSource source = new StreamSource(servletInputStream);
	validator.validate(source);
}

public void ok2Validator(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	SchemaFactory factory = SchemaFactory.newInstance("http://www.w3.org/2001/XMLSchema");
	Schema schema = factory.newSchema();
	Validator validator = schema.newValidator();
    validator.setProperty("http://javax.xml.XMLConstants/property/accessExternalDTD", "");
	validator.setProperty("http://javax.xml.XMLConstants/property/accessExternalSchema", "");
	StreamSource source = new StreamSource(servletInputStream);
	validator.validate(source);
}
```


## XMLDecoder XXE注入

JDK原生，在JDK1.7.0_21测试存在，JDK1.8不存在，JDK1.7.X其他版本暂未测试。

```java
import java.beans.XMLDecoder;

public void badXMLDecoder(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	XMLDecoder xmlDecoder = new XMLDecoder(servletInputStream);
	xmlDecoder.readObject();
}
```

## DocumentBuilder XXE注入

```java
import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;

public void badDocumentBuilder(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
	DocumentBuilder documentBuilder = factory.newDocumentBuilder();
	documentBuilder.parse(servletInputStream);
}
```

## jdom2-SAXBuilder XXE注入

```java
import org.jdom2.input.SAXBuilder;

public void badSAXBuilder(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	SAXBuilder builder = new SAXBuilder();
	Document doc = builder.build(servletInputStream);
}

public void goodSAXBuilder(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	SAXBuilder builder = new SAXBuilder(true);
	Document doc = builder.build(servletInputStream);
}

public void goodSAXBuilder(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	SAXBuilder saxBuilder = new SAXBuilder();
	saxBuilder.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true);
	saxBuilder.build(file);
}
```

## jdom-SAXBuilder XXE注入

```java
import org.jdom.input.SAXBuilder;

public void badSAXBuilder(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	SAXBuilder builder = new SAXBuilder();
	Document doc = builder.build(servletInputStream);
}
```

## SAXParser XXE注入

```java
import javax.xml.parsers.SAXParser;
import javax.xml.parsers.SAXParserFactory;

public void badSAXParser(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	SAXParserFactory spf = SAXParserFactory.newInstance();
	SAXParser parser = spf.newSAXParser();
	parser.parse(servletInputStream, new HandlerBase());
}

public void okSAXParser(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	SAXParserFactory spf = SAXParserFactory.newInstance();
	spf.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true);
	spf.setFeature("http://xml.org/sax/features/external-general-entities", false);
	spf.setFeature("http://xml.org/sax/features/external-parameter-entities", false);
	spf.setFeature("http://apache.org/xml/features/nonvalidating/load-external-dtd", false);
	SAXParser parser = spf.newSAXParser();
	parser.parse(servletInputStream, new HandlerBase());
}
```

## SAXReader XXE注入

```java
import javax.xml.parsers.SAXParser;
import javax.xml.parsers.SAXParserFactory;

public void badSAXParser(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	SAXReader saxReader = new SAXReader();
	saxReader.read(InputSource);
}

public void okSAXParser(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	SAXParserFactory spf = SAXParserFactory.newInstance();
	spf.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true);
	spf.setFeature("http://xml.org/sax/features/external-general-entities", false);
	spf.setFeature("http://xml.org/sax/features/external-parameter-entities", false);
	spf.setFeature("http://apache.org/xml/features/nonvalidating/load-external-dtd", false);
	SAXParser parser = spf.newSAXParser();
	parser.parse(servletInputStream, new HandlerBase());
}
```

## XMLReader XXE注入

```java
import org.xml.sax.XMLReader;
import org.xml.sax.helpers.XMLReaderFactory;

public void badXMLReader(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	XMLReader reader = XMLReaderFactory.createXMLReader();
	reader.parse(new InputSource(servletInputStream));
}

public void okXMLReader(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	XMLReader reader = XMLReaderFactory.createXMLReader();
	reader.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true);
	reader.setFeature("http://apache.org/xml/features/nonvalidating/load-external-dtd", false);
	reader.setFeature("http://xml.org/sax/features/external-general-entities", false);
	reader.setFeature("http://xml.org/sax/features/external-parameter-entities", false);
	reader.parse(new InputSource(servletInputStream));
}
```

## Transformer XXE注入

```java
import javax.xml.transform.TransformerFactory;
import org.xml.sax.helpers.XMLReaderFactory;

public void badTransformer(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	TransformerFactory tf = TransformerFactory.newInstance();
	StreamSource source = new StreamSource(servletInputStream);
	tf.newTransformer().transform(source, new DOMResult());
}

public void okTransformer(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	TransformerFactory tf = TransformerFactory.newInstance();
    tf.setAttribute(XMLConstants.ACCESS_EXTERNAL_DTD, "");
	tf.setAttribute(XMLConstants.ACCESS_EXTERNAL_STYLESHEET, "");
	StreamSource source = new StreamSource(servletInputStream);
	tf.newTransformer().transform(source, new DOMResult());
}
```

## TransformerFactory XXE注入

```java
import javax.xml.transform.TransformerFactory;

public void badTransformerFactory(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	//实际创建com.sun.org.apache.xalan.internal.xsltc.trax.TransformerFactoryImpl对象
	TransformerFactory transformerFactory = TransformerFactory.newInstance();
	transformerFactory.newTransformer(new StreamSource(servletInputStream));
}

public void okTransformerFactory(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	TransformerFactory transformerFactory = TransformerFactory.newInstance();
	transformerFactory.setAttribute(XMLConstants.ACCESS_EXTERNAL_DTD, "");
	transformerFactory.setAttribute(XMLConstants.ACCESS_EXTERNAL_STYLESHEET, "");
	transformerFactory.newTransformer(new StreamSource(servletInputStream));
}
```

## SAXTransformerFactory XXE注入

```java
import javax.xml.transform.sax.SAXTransformerFactory;

public void bad1SAXTransformerFactory(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	//实际创建com.sun.org.apache.xalan.internal.xsltc.trax.TransformerFactoryImpl对象
	SAXTransformerFactory sf = (SAXTransformerFactory) SAXTransformerFactory.newInstance();
	StreamSource source = new StreamSource(servletInputStream);
	sf.newTransformerHandler(source);
}

public void bad2SAXTransformerFactory(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	//实际创建com.sun.org.apache.xalan.internal.xsltc.trax.TransformerFactoryImpl对象
	SAXTransformerFactory sf = (SAXTransformerFactory) SAXTransformerFactory.newInstance();
	StreamSource source = new StreamSource(servletInputStream);
	sf.newTransformer(source);
}

public void bad3SAXTransformerFactory(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	//实际创建com.sun.org.apache.xalan.internal.xsltc.trax.TransformerFactoryImpl对象
	SAXTransformerFactory sf = (SAXTransformerFactory) SAXTransformerFactory.newInstance();
	StreamSource source = new StreamSource(servletInputStream);
	sf.newXMLFilter(source);
}

public void okSAXTransformerFactory(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	SAXTransformerFactory sf = (SAXTransformerFactory) SAXTransformerFactory.newInstance();
	sf.setAttribute(XMLConstants.ACCESS_EXTERNAL_DTD, "");
	sf.setAttribute(XMLConstants.ACCESS_EXTERNAL_STYLESHEET, "");
	StreamSource source = new StreamSource(servletInputStream);
	sf.newTransformerHandler(source);
}
```


## SchemaFactory XXE注入

```java
import javax.xml.validation.Schema;
import javax.xml.validation.SchemaFactory;

public void badSchemaFactory(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	//实际创建com.sun.org.apache.xerces.internal.jaxp.validation.XMLSchemaFactory对象
	SchemaFactory factory = SchemaFactory.newInstance("http://www.w3.org/2001/XMLSchema");
	StreamSource source = new StreamSource(servletInputStream);
	Schema schema = factory.newSchema(source);
}

public void okSchemaFactory(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	SchemaFactory factory = SchemaFactory.newInstance("http://www.w3.org/2001/XMLSchema");
	factory.setProperty(XMLConstants.ACCESS_EXTERNAL_DTD, "");
	factory.setProperty(XMLConstants.ACCESS_EXTERNAL_SCHEMA, "");
	StreamSource source = new StreamSource(servletInputStream);
	Schema schema = factory.newSchema(source);
}
```

## Unmarshaller XXE注入

Unmarshaller在jdk 1.8后修复了xxe注入

```java
import javax.xml.bind.JAXBContext;
import javax.xml.bind.Unmarshaller;

public void badXPathExpression(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	JAXBContext jaxbContext = JAXBContext.newInstance(Test.class);
	Unmarshaller unmarshaller = jaxbContext.createUnmarshaller();
	unmarshaller.unmarshal(servletInputStream);
}


Test.java

import java.io.Serializable;
import javax.xml.bind.annotation.XmlRootElement;

@XmlRootElement(name="name")
public class Test implements Serializable {

	private Integer id;

	private String name;

	private String pass;

	public Integer getId() {
		return id;
	}

	public void setId(Integer id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getPass() {
		return pass;
	}

	public void setPass(String pass) {
		this.pass = pass;
	}

	@Override
	public String toString() {
		return "Test{" +
				"id=" + id +
				", name='" + name + '\'' +
				", pass='" + pass + '\'' +
				'}';
	}
}

```

## XPathExpression XXE注入

调用Document.parse(...)解析

```java
import javax.xml.xpath.XPath;
import javax.xml.xpath.XPathExpression;
import javax.xml.xpath.XPathFactory;

public void badXPathExpression(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	XPath xPath = XPathFactory.newInstance().newXPath();
	XPathExpression xPathExpression = xPath.compile("xxe");
	xPathExpression.evaluate(new InputSource(servletInputStream));
}
```

## Persister XXE注入

```pom
<dependency>
  <groupId>org.simpleframework</groupId>
  <artifactId>simple-xml</artifactId>
  <version>2.7.1</version>
</dependency>
```

```java
import org.simpleframework.xml.core.Persister;

public void badPersister(HttpServletRequest request) throws Exception {
	ServletInputStream servletInputStream = request.getInputStream();
	Persister persister = new Persister();
	persister.read("", servletInputStream);
}
```
