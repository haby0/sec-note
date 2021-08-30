# Java XML external entity (XXE) injection文档

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

