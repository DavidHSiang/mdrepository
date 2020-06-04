---
title: spring-oxm入门示例
date: 2020-05-18 22:41:36
tags: 
	- Spring
categories: 
	- [开发框架,Spring]
---

转载自[Spring oxm入门实例](https://blog.csdn.net/xiang__liu/article/details/81191850): https://blog.csdn.net/xiang__liu/article/details/81191850

## O/X Mapper 是什么？

Spring 3.0 的一个新特性是 O/X Mapper。O/X 映射器这个概念并不新鲜，O 代表 Object，X 代表 XML。它的目的是在 Java 对象（几乎总是一个 plain old Java object，或简写为 POJO）和 XML 文档之间来回转换。

例 如，您可能有一个带有几个属性的简单 bean，且您的业务需要将那个 Java 对象转换为一个 XML 文档。Spring 的 O/X  Mapper 能够为您解决那个问题。如果反过来，您需要将一个 XML 文档转换为一个简单 Java bean，Spring 的 O/X  Mapper 也能胜任。

有一点需要注意：Spring O/X Mapper 只是定义由流行的第三方框架实现的统一的界面。要利用 Spring 的 O/X 功能，您需要一个在 Java 对象和  XML 之间来回转换的实用程序。Castor 就是这样一个流行的第三方工具，本文将使用这个工具。其他这样的工具包括 XMLBeans、Java  Architecture for XML Binding (JAXB)、JiBX 和 XStream。

**注意: 在Spring5版本后, spring-oxm不再支持Castor这个工具**。为了演示方便, 本文采用Castor工具, 以及Spring4版本

> 总结:
>
> ​		oxm(o/xMapping)是spring 3.0的一个新特性, 它的功能是**实体类与xml之间的相互转换**

<!--more-->

## 编组和解组

进行 O/X 映射时，您经常会看到编组（marshalling）和解组（unmarshalling） 这两个术语。

编组 指将 Java bean 转换成 XML 文档的过程，这意味着 Java bean 的所有字段和字段值都将作为 XML 元素或属性填充到 XML 文件中。有时，编组也称为序列化（serializing）。

如您所料，解组 是与编组完全相反的过程，即将 XML 文档转换为 Java bean，这意味着 XML 文档的所有元素或属性都作为 Java 字段填充到 Java bean 中。有时，解组也称为反序列化（deserializing）。

> 总结: 
>
> * 编组(``marshalling``): 将JavaBean转化为xml
> * 解组(``unmarshalling``): 将xml转化为JavaBean

## 使用 Spring 的 O/X Mapper 的好处

使 用 Spring 的 O/X Mapper 的一个最直接的好处是可以通过利用 Spring 框架的其他特性简化配置。Spring 的 bean 库支持将实例化的 O/X 编组器注入（即前面提到过的 “依赖项注入”）使用那些编组器的对象。重申一遍，这将加快应用程序开发和部署。

遵循坚实的面向对象的设计实践，Spring O/X 框架只定义两个接口：Marshaller 和 Unmarshaller，它们用于执行 O/X  功能，这是使用这个框架的另一个重大好处。这些接口的实现完全对独立开发人员开放，开发人员可以轻松切换它们而无需修改代码。例如，如果您一开始使用  Castor 进行 O/X 转换，但后来发现它缺乏您需要的某个功能，这时您可以切换到 XMLBeans  而无需任何代码更改。唯一需要做的就是更改 Spring 配置文件以使用新的 O/X 框架。

使用 Spring 的 O/X Mapper 的另一个好处是统一的异常层次结构。Spring  框架遵循使用它的数据访问模块建立的模式，方法是将原始异常对象包装到 Spring 自身专为 O/X Mapper  建立的运行时异常中。由于第三方提供商抛出的原始异常被包装到 Spring  运行时异常中，您能够查明出现异常的根本原因。您也不必费心修改代码以捕获异常，因为异常已包装到一个运行时异常中。以下几个运行时异常扩展了基础异常  XMLMappingException：GenericMarshallingFailureException、  ValidationFailureException、MarshallingFailureException 和  UnmarshallingFailureException。

> 总结
>
> ​		1.因为spring的bean库支持实例化o/x编组的注入，所以使用xml编写的bean也可以注入spring中使用。这样做可以将程序和配置分类处理。结构更清晰。
>
> ​		2.o/x使用面向接口的形式开发，所以单独的开发者不需要关注其实现细节，并且想要改变其实现方式，只需要修改o/x的实现配置即可。
>
> ​		3.异常类型层次结构化，spring把实现原厂的异常进行了自己的封装。并且是运行时异常！这样做可以更精准的定位异常。

##  入门实例

### (1)导入依赖

编辑pom.xml文件, 添加相关依赖

**注意: 在Spring5版本后, spring-oxm不再支持Castor这个工具。这里使用Spring4版本**

> pom.xml

```xml
 <dependencies>

    <!--spring上下文-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>4.2.5.RELEASE</version>
    </dependency>

    <!--spring-oxm-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-oxm</artifactId>
      <version>4.2.5.RELEASE</version>
    </dependency>

    <!--oxm功能类jar-->
    <dependency>
      <groupId>org.codehaus.castor</groupId>
      <artifactId>castor</artifactId>
      <version>1.3.2</version>
      <type>pom</type>
    </dependency>

    <!--oxm功能类jar-->
    <dependency>
      <groupId>org.codehaus.castor</groupId>
      <artifactId>castor-xml</artifactId>
      <version>1.3.2</version>
    </dependency>

      <!--单元测试-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>
      
</dependencies>
```

### (2)编写Spring配置文件

编写applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">

    <!--将编组和解组功能导入到oxmDemo类中-->
    <bean id="oxmDemo" class="com.spider.OxmDemo">
        <property name="marshaller" ref="castorMarshaller" />
        <property name="unmarshaller" ref="castorMarshaller" />
    </bean>
    <!-- 引入castor包:castor-1.3.2-core.jar,castor-1.3.2-xml.jar -->
    <bean id="castorMarshaller" class="org.springframework.oxm.castor.CastorMarshaller">
        <!--包含映射关系的xml,如果不添加，解组时无法解析root元素-->
        <property name="mappingLocation" value="classpath:mapping.xml" />
    </bean>
</beans>
```

### (3)mapping.xml 文件

```xml
<mapping>
    <class name="com.spider.model.Customer">

        <map-to xml="Customer"/>

        <field name="flag" type="boolean">
            <bind-xml name="flag" node="element"/>
        </field>

        <field name="name" type="string">
            <bind-xml name="name" node="element"/>
        </field>

        <field name="sex" type="string">
            <bind-xml name="sex" node="element"/>
        </field>
    </class>
</mapping>
```

### (4)Customer类

```java
package com.spider.model;

public class Customer {

    private String name;
    private String sex;
    private Boolean flag;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

    public Boolean getFlag() {
        return flag;
    }

    public void setFlag(Boolean flag) {
        this.flag = flag;
    }

    @Override
    public String toString() {
        return "Customer{" +
                "name='" + name + '\'' +
                ", sex='" + sex + '\'' +
                ", flag=" + flag +
                '}';
    }
}
```

### (5)OxmDemo类

```java
package com.spider;

import ...;


public class OxmDemo {


    private Marshaller marshaller;//编组类
    private Unmarshaller unmarshaller;//解组类

    public Marshaller getMarshaller() {
        return marshaller;
    }

    public void setMarshaller(Marshaller marshaller) {
        this.marshaller = marshaller;
    }

    public Unmarshaller getUnmarshaller() {
        return unmarshaller;
    }

    public void setUnmarshaller(Unmarshaller unmarshaller) {
        this.unmarshaller = unmarshaller;
    }

    /**
     * @param object 编码对象
     * @param filepath xml输出路径
     * @throws IOException io异常
     */
    public void converFromObjectToXML(Object object,String filepath) throws IOException {
        FileOutputStream os = null;
        try{
            os = new FileOutputStream(filepath);
            getMarshaller().marshal(object,new StreamResult(os));
        }finally {
            if(os!=null){
                os.close();
            }
        }
    }

    /**
     * @param xmlfile xml文件位置
     * @return
     * @throws IOException
     */
    public Object converFromXMLToObject(String xmlfile) throws IOException{
        FileInputStream is = null;
        try{
            is = new FileInputStream(xmlfile);
            return getUnmarshaller().unmarshal(new StreamSource(is));
        }finally {
            if(is!=null){
                is.close();
            }
        }
    }
}
```

### (6)测试类

```java
package com.spider;

import ...;

public class MyTest {
    private static final String XML_FILE_NAME = "customer.xml";//文件输出位置
    public static void main(String[] args) throws IOException {
        ApplicationContext appContext = new ClassPathXmlApplicationContext("applicationContext.xml");
        OxmDemo oxmDemo = (OxmDemo) appContext.getBean("oxmDemo");
        Customer customer = new Customer();
        customer.setName("xiaowan");
        customer.setFlag(false);
        customer.setSex("man");
        System.out.println("Conver Object to XML");
        oxmDemo.converFromObjectToXML(customer,XML_FILE_NAME);
        System.out.println("Done \n");

        System.out.println("Conver XML to Object");
        Customer result = (Customer) oxmDemo.converFromXMLToObject(XML_FILE_NAME);
        System.out.println(result);
    }
}
```

### (7)运行测试类

运行测试类, 在项目运行目录下, 会产生一个customer.xml文件:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Customer><flag>false</flag><name>xiaowan</name><sex>man</sex></Customer>
```

程序输出的结果:

```bash
Done 

Conver XML to Object
Customer{name='xiaowan', sex='man', flag=false}
```

## 参考文档

[Spring oxm入门实例](https://blog.csdn.net/xiang__liu/article/details/81191850) : https://blog.csdn.net/xiang__liu/article/details/81191850

[spring oxm入门（包含demo）](https://www.cnblogs.com/xuxiuxiu/p/6653060.html) : https://www.cnblogs.com/xuxiuxiu/p/6653060.html

[Spring oxm 入门](https://blog.csdn.net/qq_37151646/article/details/82664846) : https://blog.csdn.net/qq_37151646/article/details/82664846