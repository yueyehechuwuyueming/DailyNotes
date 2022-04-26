# 1-11周导学

![image-20220425193425263](https://s2.loli.net/2022/04/25/sWY3hPU4v7oiAte.png)

![image-20220425193438430](https://s2.loli.net/2022/04/25/G4tPhnaJT86wbL7.png)

![image-20220425194103966](https://s2.loli.net/2022/04/25/TJt9OGosinNSeXQ.png)

![image-20220425194129445](https://s2.loli.net/2022/04/25/euGs8gyz2iULwpQ.png)

![image-20220425194144718](https://s2.loli.net/2022/04/25/wejB6Co9YmZ7TSh.png)

# XML基础

## XML介绍与用途

### XML定义

- 全称：Extensible Markup Language，可扩展标记语言
- 编写XML就是编写标签，与HTML相似，扩展名.xml
- 良好的人机可读性

### XML与HTML的比较

- XML与HTML非常相似，都是编写标签

- XML没有预定义标签，HTML存在大量预定义标签

- XML重在保存与传输数据，HTML用于显示信息

  ![image-20220425194804000](https://s2.loli.net/2022/04/25/Zlrmex74KgzQ1jq.png)

  ### XML的用途

  - Java程序的配置描述文件

    ![image-20220425195049400](https://s2.loli.net/2022/04/25/vAunM6WLopIUdTN.png)

  - 用于保存程序的产生数据

    ![image-20220425195100850](https://s2.loli.net/2022/04/25/mFTIs3A16BUtHch.png)

  - 网络间的传输

    ![image-20220425195117399](https://s2.loli.net/2022/04/25/EeQNARGc2xJq7Cw.png)

    ### XML文档结构
    
    - 第一行必须是XML声明
    - 有且仅有一个根节点
    - XML标签的书写规则同HTML
    
    ### XML声明
    
    - XML声明说明XML文档的基本信息，包括版本号与字符集，写在XML第一行
    
      ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <!-- 人力资源管理系统 -->
      <hr>
          <employee no="3309">
              <name>张三</name>
              <age>21</age>
              <salary>4000</salary>
              <department>
                  <dname>会计部</dname>
                  <address>金广厦-B103</address>
              </department>
          </employee>
          <employee no="3310">
              <name>李四</name>
              <age>31</age>
              <salary>6000</salary>
              <department>
                  <dname>工程部</dname>
                  <address>金广厦-B103</address>
              </department>
          </employee>
      </hr> 
      ```
    
      

## XML的语法规则

- 合法的标签名

  - 标签名要有意义
  - 建议使用英文、小写字母，单词之间用“-”分割
  - 建议多级标签之间不要重名

- 适当的注释和缩进

- 合理使用属性

  - 标签属性常用于描述标签不可或缺的信息
  - 对标签分组或标签设置为Id时常用属性表示

- 特殊字符与CDARA标签

  - Q：标签体中，出现"<”、">"特殊字符，会破坏文档结构

  - A1：使用实体引用

    | 实体引用 | 对应符号 | 说明   |
    | -------- | -------- | ------ |
    | &It；    | <        | 小于   |
    | &gt；    | >        | 大于   |
    | &amp；   | &        | 和号   |
    | &apos；  | ‘        | 单引号 |
    | &quot；  | “        | 双引号 |

  - A2：使用CDATA标签

    - CDATA指的是不应由XML解析器进行解析的文本数据
    - 格式：`<![CDATA["开始，到"]]>`

    ```xml
    <!-- 不希望content中被当作XML解析 -->
    <lesson>
        <content>
            本节学习CDATA标签
            <body>
                <a href="index.html">首页</a>
            </body>
        </content>
    </lesson>
    <!-- 进行以下修改 -->
    <lesson>
        <content>
            <![CDATA[
            本节学习CDATA标签
            <body>
                <a href="index.html">首页</a>
            </body>
            ]]>
        </content>
    </lesson>
    ```

    

- 有序的子元素

  - 在XML多层的字元素中，标签前后顺序应保持一致

  

## XML语义约束

- XML文档结构正确，但不一定能够有效

  - 例如，员工文档XML中绝不允许出现“植物品种”标签
  - XML语义约束就是用于规定XML文档中允许出现那些元素

- XML语义约束有两种定义方式

  - DTD（Docunment Type Definition 文档类型定义）

    - 定义节点`<!ELEMENT>`
      - 定义hr节点下只允许出现1个employee：子节点。`<IELEMENT hr（employee）>`
      - employee节点下必须包含以下四个节点，且按顺序出现。`<！ELEMENT employee（name，age，salary，department）>`
      - 定义name标签体只能是文本，#PCDATA代表文本元素。`<！ELEMENT name（#PCDATA）>`
    - 定义节点数量
      - hr节点下最少出现1个employee-子节点。`<！ELEMENT hr（employee+）>`
      - hr节点下可出现O.n个employee-子节点。`<！ELEMENT hr（employee*）>`
      - hr节点下最多出现1个employee子节点。`<！ELEMENT hr（employee？）>`
    - XML引用DTD文件 `<！DOCTYPE根节点SYSTEM"dtd文件路径">`
      - 示例`<！DOCTYPE hr SYSTEM"hr.dtd">`

    ```dtd
    <!-- hr.dtd -->
    <?xml version="1.0" encoding="UTF-8"?>
    <!ELEMENT hr(employee+)>
    <!-- employee后有一个空格，尤其注意 -->
    <!ELEMENT employee (name,age,salary,department)>
    <!ATTLIST employee no CDATA "">
    <!-- 纯文本结点 -->
    <!ELEMENT name (#PCDATA)>
    <!ELEMENT age (#PCDATA)>
    <!ELEMENT salary (#PCDATA)>
    <!ELEMENT department (dname,address)>
    <!ELEMENT dename (#PCDATA)>
    <!ELEMENT address (#PCDATA)>
    
    <!-- hr.xml -->
    <?xml version="1.0" encoding="UTF-8"?>
     <!DOCTYPE hr SYSTEM "hr.dtd"  
    <!-- 人力资源管理系统 -->
    <!-- <hr xmlns:xsi="http://w3.org/2001/XMLSchema-instance" xsi:noNameSpaceSchemaLacation="hr.xsd"> -->
    <hr>
        <employee no="3309">
            <name>张三</name>
            <age>21</age>
            <salary>4000</salary>
            <department>
                <dname>会计部</dname>
                <address>金广厦-B103</address>
            </department>
        </employee>
        <employee no="3310">
            <name>李四</name>
            <age>31</age>
            <salary>6000</salary>
            <department>
                <dname>工程部</dname>
                <address>金广厦-B103</address>
            </department>
        </employee>
    </hr> 
    
    ```
  
  - XML Schema
  
    ```xml
    <!-- hr.xsd -->
    <?xml version="1.0" encoding="UTF-8"?>
    <schema xmlns="http://www.w3.org/2001/XMLSchema">
    	<element name="hr">
    		<!-- complexType标签含义是复杂节点，包含子节点时必须使用这个标签 -->
    		<complexType>
    			<sequence>
    				<element name="employee" minOccurs="1" maxOccurs="9999">
    					<complexType>
    						<sequence>
    							<element name="name" type="string"></element>
    							<element name="age">
    								<simpleType>
    									<restriction base="integer">
    										<minInclusive value="18"></minInclusive>
    										<maxInclusive value="60"></maxInclusive>
    									</restriction>
    								</simpleType>
    							</element>
    							<element name="salary" type="integer"></element>
    							<element name="department">
    								<complexType>
    									<sequence>
    										<element name="dname" type="string"></element>
    										<element name="address" type="string"></element>
    									</sequence>
    								</complexType>
    							</element>
    						</sequence>
    						<attribute name="no" type="string" use="required"></attribute>					
    					</complexType>
    				</element>
    			</sequence>
    		</complexType>
    	</element>	
    </schema>
    
    <!-- hr-schema.xml -->
    <?xml version="1.0" encoding="UTF-8"?>
    <!-- 人力资源管理系统 -->
    <hr xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
    xsi:noNamespaceSchemaLocation="hr.xsd">
    	<employee no="3309">
    		<name>张三</name>
    		<age>28</age>
    		<salary>4000</salary>
    		<department>
    			<dname>会计部</dname>
    			<address>XX大厦-B103</address>
    		</department>
    	</employee>
    	<employee no="3310">
    		<name>李四</name>
    		<age>23</age>
    		<salary>3000</salary>
    		<department>
    			<dname>工程部</dname>
    			<address>XX大厦-B104</address>
    		</department>
    	</employee>
    </hr>
    ```
  
  ### DOM文档对象模型
  
  - 缩写：Document Object Medel
  - 定义：定义了访问和操作XML文档的标准方法，DOM把XML文档当作树结构来查看，额能够通过DOM树来读写所有元素
  
  ![image-20220426205041565](https://s2.loli.net/2022/04/26/vPcOarU6QHnVb5E.png)
  
  - Dom4j
    - 一个易用的、开源的库，用于解析XML。它应用于Java平台，具有性能优异、功能强大和极其易使用的特点。
    - Dom4j将XML视为Documenty对象。
    - XML标签被Dom4j定义为Element对象。
    - 需要Java1.8+

### 利用Dom4j遍历XML

- 步骤
  - string一个file的文件地址：xml的文件地址
  - SAXReader出一个reader类，来读取解析XML
  - Document一个文件来读取file
  - Element一个root获取根标签
  - element方法来获取唯一的子节点对象
  - 用elementText方法获取输出

```java
package com.cy.dom4j;

import java.util.List;

import org.dom4j.Attribute;
import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;

public class HrReader {
	public void readXml() {
		String file="F:/Programming/JavaProgram/xml/src/hr.xml";
		//SAXReader类是读取XML文件的核心类，用于将XML解析后以“树”的形式保存在内存中
		SAXReader reader = new SAXReader();
		try {
			Document document = reader.read(file);
			//获取XML文档的根节点，即hr标签
			Element root = document.getRootElement();
			//elements方法用于获取指定的标签集合
			List<Element> employees = root.elements("employee");
			for(Element employee : employees) {
				//element方法用于获取唯一的子节点对象
				Element name = employee.element("name");
				String empName = name.getText();//getText()方法用于获取标签文本
				System.out.println(empName);
				//以下一句等同于前三句
				System.out.println(employee.elementText("age"));
				System.out.println(employee.elementText("salary"));
				Element department = employee.element("department");
				System.out.println(department.element("dname").getText());
				System.out.println(department.element("address").getText());
				Attribute att = employee.attribute("no");
				System.out.println(att.getText());

			}
		} catch (DocumentException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	public static void main(String[] args) {
		HrReader reader = new HrReader();
		reader.readXml();
	}
}
```

### Dom4j更新XML

- 步骤
  - string一个file的文件地址：xml的文件地址
  - SAXReader出一个reader类，来读取解析XML
  - Document一个文件来读取file
  - Element一个root获取根标签
  - addElement方法来添加子节点对象来setText
  - write一个输出流，document写入
  - writer关闭

```java
package com.cy.dom4j;

import java.io.FileOutputStream;
import java.io.OutputStreamWriter;
import java.io.Writer;

import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;

public class HrWriter {
	public void writeXML() {
		String file = "F:/Programming/JavaProgram/xml/src/hr.xml";
		SAXReader reader = new SAXReader();
		try {
			Document document = reader.read(file);
			Element root = document.getRootElement();
			Element employee = root.addElement("employee");
			employee.addAttribute("no","3311");
			Element name = employee.addElement("name");
			name.setText("李铁柱");
			employee.addElement("age").setText("37");
			employee.addElement("salary").setText("3600");
			Element department = employee.addElement("department");
			department.addElement("dname").setText("人事部");
			department.addElement("address").setText("金广厦-B105");
			Writer writer = new OutputStreamWriter(new FileOutputStream(file),"UTF-8");
			document.write(writer);
			writer.close();
			//把报异常的DocumentException提高至Exception
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	public static void main(String[] args) {
		HrWriter hrWriter = new HrWriter();
		hrWriter.writeXML();
	}
}

```

### Xpath路径表达式

- 概念

  - XPath路径表达式是XML 文档中查找数据的语言。

  - 掌握XPath可以极大的提高在提取数据时的开发效率。 

  - 学习XPath本质就是掌握各种形式表达式的使用技巧。

- XPath基本表达式（常用）

  - ![image-20220426224400518](https://s2.loli.net/2022/04/26/BVPkCdOsE8WJnSK.png)

- XPath基本表达式案例

  - ![image-20220426224437805](https://s2.loli.net/2022/04/26/eNIzPoGmZ58hKpH.png)

- XPath谓语表达式

  - ![image-20220426224646404](https://s2.loli.net/2022/04/26/NPCso7c9fwGAqrd.png)



## Java解析XML

## XPath路径表达式



# Serlet入门

