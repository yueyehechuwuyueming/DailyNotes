# 10-11周导学

![image-20220425193425263](https://s2.loli.net/2022/04/25/sWY3hPU4v7oiAte.png)

![image-20220425193438430](https://s2.loli.net/2022/04/25/G4tPhnaJT86wbL7.png)

![image-20220425194103966](https://s2.loli.net/2022/04/25/TJt9OGosinNSeXQ.png)

![image-20220425194129445](https://s2.loli.net/2022/04/25/euGs8gyz2iULwpQ.png)

![image-20220425194144718](https://s2.loli.net/2022/04/25/wejB6Co9YmZ7TSh.png)

# XML基础

## 1 XML介绍与用途

### 1.1 XML定义

- 全称：Extensible Markup Language，**可扩展标记语言**
- 编写XML就是编写标签，与HTML相似，扩展名.xml
- 良好的人机可读性

### 1.2 XML与HTML的比较

- XML与HTML非常相似，都是编写标签

- XML**没有预定义标签**，HTML存在大量预定义标签

- XML重在保存与传输数据，HTML用于**显示信息**

  ![image-20220425194804000](https://s2.loli.net/2022/04/25/Zlrmex74KgzQ1jq.png)


### 1.3 XML的用途

- Java程序的配置描述文件

  ![image-20220425195049400](https://s2.loli.net/2022/04/25/vAunM6WLopIUdTN.png)

- 用于保存程序的产生数据

  ![image-20220425195100850](https://s2.loli.net/2022/04/25/mFTIs3A16BUtHch.png)

- 网络间的传输

  ![image-20220425195117399](https://s2.loli.net/2022/04/25/EeQNARGc2xJq7Cw.png)


### 1.4 XML文档结构

- **第一行必须是XML声明**
- **有且仅有一个根节点**
- XML标签的书写规则同HTML

### 1.5 XML声明

- XML声明说明XML文档的基本信息，**包括版本号与字符集**，写在XML第一行

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


## 2 XML的语法规则

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

- 习题

  - ![image-20220427100444750](https://s2.loli.net/2022/04/27/AgPLV3CSts6Dbeq.png)
  - A:正确，可以用-分割不同单词
  - B:$不符合规范
  - C:要用英文
  - D:多级标签之间不要重名

  

## 3 XML语义约束

### 3.1 XML语义约束概念

- XML文档结构正确，但不一定能够有效

  - 例如，员工文档XML中绝不允许出现“植物品种”标签
  - XML语义约束就是用于规定XML文档中允许出现那些元素

### 3.2 XML语义约束方法至DTD

- DTD（Docunment Type Definition 文档类型定义）

  - 定义节点`<!ELEMENT>`
    - 定义hr节点下只允许出现1个employee：子节点。`<IELEMENT hr（employee）>`
    - employee节点下必须包含以下四个节点，且按顺序出现。`<！ELEMENT employee（name，age，salary，department）>`
    - 定义name标签体只能是文本，#PCDATA代表文本元素。`<！ELEMENT name（#PCDATA）>`
  - 定义节点数量
    - hr节点下最少出现1个employee-子节点。`<！ELEMENT hr（employee+）>`
    - hr节点下可出现O…n个employee-子节点。`<！ELEMENT hr（employee*）>`
    - hr节点下最多出现1个employee子节点。`<！ELEMENT hr（employee？）>`
  - XML引用DTD文件 `<！DOCTYPE根节点SYSTEM"dtd文件路径">`
    - 示例`<！DOCTYPE hr SYSTEM"hr.dtd">`
  - 关于XML语义描述正确的是（B ）（选择两项）
    - A .<！ELEMENT student（name，age，score）>表示student节点必须包含三个子节点，但是可以不按顺序出现
      - ×，必须按照顺序
    - B.<！ELEMENT display-name（#PCDATA）>表示display-name标签体只能是文本
      - √
    - C.<！ELEMENT school（student+）>表示school-节点下最少有一个子节点
      - √
    - D.<！ELEMENT school（student）>表示school-节点下的student节点数不做限制
      - ×，只允许一个节点

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

### 3.3 XML Schema

- element：定义属性的节点，内部可定义最大最小数量等、类型等
- complexType：复杂节点，包含子节点时必须使用这个标签
- sequence：序列节点，里面的节点必须按照顺序严格书写
- simpleType+restriction（minInclusive、maxInclusive）：简单类型约束，可以进行数值范围约束
- attribute name="" type="" use="required":

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
 						<!-- no属性在任何employee属性中必须存在 -->
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



## 4 Java解析XML

### 4.1 DOM文档对象模型

- 缩写：Document Object Medel
- 定义：定义了访问和操作XML文档的标准方法，DOM把XML文档当作树结构来查看，额能够通过DOM树来读写所有元素

![image-20220426205041565](https://s2.loli.net/2022/04/26/vPcOarU6QHnVb5E.png)

- Dom4j
  - 一个易用的、开源的库，用于解析XML。它应用于Java平台，具有性能优异、功能强大和极其易使用的特点。
  - Dom4j将XML视为Documenty对象。
  - XML标签被Dom4j定义为Element对象。
  - 需要Java1.8+

### 4.2 利用Dom4j遍历XML

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

### 4.3 Dom4j更新XML

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

## 5 Xpath路径表达式

### 5.1 Xpath路径表达式

- 概念

  - XPath路径表达式是XML 文档中查找数据的语言。

  - 掌握XPath可以极大的提高在提取数据时的开发效率。 

  - 学习XPath本质就是掌握各种形式表达式的使用技巧。
- XPath基本表达式（常用）

  - ![image-20220426224400518](https://s2.loli.net/2022/04/26/BVPkCdOsE8WJnSK.png)
- XPath基本表达式案例

  - ![image-20220426224437805](https://s2.loli.net/2022/04/26/eNIzPoGmZ58hKpH.png)
  - 例题
    - 关于XPath路径表达式的描述错误的是（）（选择一项）
    - A. school/student表示选取属于school的子元素的所有student元素
    - B. /school表示选取根元素school
    - C. @type 表示选取名为type的属性
      - 错，正确写法是//@type
    - D. //student表示选取所有student子元素
- XPath谓语表达式

  - ![image-20220426224646404](https://s2.loli.net/2022/04/26/NPCso7c9fwGAqrd.png)
  - 例题
    - 关于XPath谓语表达式的描述错误的是（ ）（选择两项） 
    - A. /school/student[0]选取属于school子元素的第一个student元素
      - ×，[1]才是第1个
    - B. //name[@lang] 选取所有拥有名为lang属性的name元素
    - C. /school/student[score>60] 选取school元素的所有student元素，并且其中score的值大于60
    - D. /school/student[last()-1] 选取属于school子元素的最后一个student元素
      - ×，最后一个就是last，没有-1

### 5.2 XPath实验室

- Jaxen是一个Java编写的开源的XPath库。这是适应多种不同的对象模型，包括DOM，XOM，dom4j和JDOM。
- Dom4j底层依赖Jaxen实现KPath查询
- Jaxen下载地址：jaxen.codehaus.org

```xml
package com.cy.dom4j;

import java.util.List;

import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.Node;
import org.dom4j.io.SAXReader;

public class XPathTestor {
	public void xpath(String xpathExp) {
		String file = "F:/Programming/JavaProgram/xml/src/hr.xml";
		SAXReader reader = new SAXReader();
		try {
			Document document = reader.read(file);
			List<Node> nodes = document.selectNodes(xpathExp);
			for(Node node : nodes) {
				Element emp  = (Element)node;
				System.out.println(emp.attributeValue("no"));
				System.out.println(emp.elementText("name"));
				System.out.println(emp.elementText("age"));
				System.out.println(emp.elementText("salary"));
				System.out.println("------------------------");
			}
		} catch (DocumentException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	
	public static void main(String[] args) {
		XPathTestor testor = new XPathTestor();
//		testor.xpath("/hr/employee");
//		testor.xpath("//employee");
//		testor.xpath("//employee[salary<4000]");
//		testor.xpath("//employee[name='李铁柱']");
//		testor.xpath("//employee[@no=3310]");
//		testor.xpath("//employee[1]");//获取编号最小的员工
//		testor.xpath("//employee[last()]");//获取编号最大的员工
//		testor.xpath("//employee[position()<3]");//获取编号前2的员工
		testor.xpath("//employee[1] | //employee[4]");//获取编号1和4的员工	
	}
}
```

## 6 编程练习

6.1 练习XML文件的书写

- ![image-20220427105353870](https://s2.loli.net/2022/04/27/T5JzC1wnLkY3KB8.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<plan>
	<teaching-plan>
		<course no="201">
			<course-name>大学英语</course-name>
			<class-hour>36</class-hour>
			<exam-form>考试</exam-form>
		</course>
		<course no="301">
			<course-name>高等数学</course-name>
			<class-hour>70</class-hour>
			<exam-form>考试</exam-form>
		</course>
		<course no="916">
			<course-name>计算机应用基础</course-name>
			<class-hour>108</class-hour>
			<exam-form>上机考试</exam-form>
		</course>
	</teaching-plan>
</plan>
```

###  6.2 练习dtd文件的书写

- 为之前存储教学计划的plan.xml文件定义语义约束，练习dtd文件的定义和使用，要求：
  1. 创建dtd文件
  2. 在根节点teaching:plan下只能出现course节点，course节点可以有多个
  3. 在course节点下只能出现course-name，class-hour和exam-form三个节点，并设置这三个节点为纯文本节点
  4. 在plan.xml文档导入dtd文件

```xml-dtd
<!-- plan.dtd -->
<?xml version="1.0" encoding="UTF-8"?>
<!ELEMENT teaching-plan (course+)>
<!ELEMENT course (course-name,course-name,exam-form)>
<!ELEMENT course-name (#PCDATA)>
<!ELEMENT age (#PCDATA)>
<!ELEMENT exam-form (#PCDATA)>

<!-- plan.xml -->
<!DOCTYPE hr SYSTEM "plan.dtd">
```

### 6.3 练习Schema文档的书写

- 为之前存储教学计划的plan.xml文件定义语义约束，首先为xml文件的course节点添加id属性，然后练习S chema文件的定义和使用，要求：
  1. 创建xsd文件 
  2. 设置course节点最多有100个 
  3. 定义course-name和exam-form节点为string类型，class-hour节点为integer类型，并设置最小值为 20，最大值为110 
  4. 设置id属性值为string类型，并且属性是必须有的 
  5. 在plan.xml文档中引入xsd文件

```xml
<!-- plan.xsd -->
<?xml version="1.0" encoding="UTF-8"?>
<schema xmlns="http://www.w3.org/2001/XMLSchema" >
	<element name="course-plan">
		<complexType>
			<sequence>
				<element name="course" minOccurs="1" maxOccurs="100">
					<complexType>
						<sequence>
							<element name="course-name" type="string"></element>
							<element name="exam-form" type="String"></element>
							<element name="class-hour">
								<simpleType>
									<restriction>
										<minInclusive value="20"></minInclusive>
										<maxInclusive value="110"></maxInclusive>
									</restriction>					
								</simpleType>
							</element>
						</sequence>
						<attribute name="id" type="string" use="required"></attribute>
					</complexType>
				</element>
			</sequence>
		</complexType>
	</element>
</schema>

<!-- plan.xml -->
<hr xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xsi:noNamespaceSchemaLocation="plan.xsd">
```

### 6.4 Dom4j练习

- 使用Dom4j操作存储课程信息的plan.xml文件
  	1. 为plan.xml文件添加一条新的课程信息
  	1. 遍历plan.xml文件并将节点和属性输出

```java
// PlanWriter.java
package com.cy.dom4j;

import java.io.FileOutputStream;
import java.io.OutputStreamWriter;
import java.io.Writer;

import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;

public class PlanWriter {
	public void writeXml() {
		String file = "F:/Programming/JavaProgram/xml/src/plan.xml";
		SAXReader reader = new SAXReader();
		try {
			Document document = reader.read(file);
			Element root = document.getRootElement();
			Element course = root.addElement("course");
			course.addAttribute("id","408");
			course.addElement("course-name").setText("计算机综合基础");
			course.addElement("class-hour").setText("70");
			course.addElement("exam-form").setText("上机考试");
			Writer writer = new OutputStreamWriter(new FileOutputStream(file),"UTF-8");
			document.write(writer);
			writer.close();			
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	public static void main(String[] args) {
		PlanWriter planWriter = new PlanWriter();
		planWriter.writeXml();
	}	
}

// PlanReader.java
package com.cy.dom4j;

import java.util.List;

import org.dom4j.Attribute;
import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;

public class PlanReader {
	public void readXml(){
		String file = "F:/Programming/JavaProgram/xml/src/plan.xml";
		SAXReader reader = new SAXReader();
		try {
			Document document = reader.read(file);
			Element root = document.getRootElement();
			List<Element> courses = root.elements("course");
			for(Element course : courses) {
				System.out.println(course.elementText("course-name"));
				System.out.println(course.elementText("class-hour"));
				System.out.println(course.elementText("exam-form"));
				Attribute att = course.attribute("id");
				System.out.println(att.getText());
				System.out.println("-------------------");
			}
			
		} catch (DocumentException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	public static void main(String[] args) {
		PlanReader reader = new PlanReader();
		reader.readXml();
	}
}
	

```

### 6.5 XPath练习

- 利用XPath对存储课程信息的plan.xml文档进行查询并将结果输出，要求如下：

   	1.  获取所有课程信息 
   	2.  查询课时小于50的课程信息 
   	3.  查询课程名为高等数学的课程信息 
   	4.  查询属性id为001的课程信息 
   	5.  查询前两条课程信息

  ```java
  package com.cy.dom4j;
  
  import java.util.List;
  
  import org.dom4j.Document;
  import org.dom4j.DocumentException;
  import org.dom4j.Element;
  import org.dom4j.Node;
  import org.dom4j.io.SAXReader;
  
  public class XPathPlanSearcher {
  	public void xpath(String xpathExp) {
  		String file = "F:/Programming/JavaProgram/xml/src/plan.xml";
  		SAXReader reader = new SAXReader();
  		try {
  			Document document = reader.read(file);
  			List<Node> nodes = document.selectNodes(xpathExp);
  			for(Node node : nodes) {
  				Element emp = (Element)node;
  				System.out.println(emp.attributeValue("id"));
  				System.out.println(emp.elementText("course-name"));
  				System.out.println(emp.elementText("class-hour"));
  				System.out.println(emp.elementText("exam-form"));
  				System.out.println("-----------------------");				
  			}
  		} catch (DocumentException e) {
  			// TODO Auto-generated catch block
  			e.printStackTrace();
  		}
  	}
  	
  	public static void main(String[] args) {
  		XPathPlanSearcher searcher =  new XPathPlanSearcher();
  //		searcher.xpath("/teaching-plan/course");
  //		searcher.xpath("//course[class-hour<'50']");
  //		searcher.xpath("//course[course-name='高等数学']");
  //		searcher.xpath("//course[@id='201']");
  		searcher.xpath("//course[position()<3]");		
  	}
  }
  ```

  

# Serlet入门

## Serlet介绍

### 软件结构发展史

- 单机时代—桌面应用
  - 桌面应用俗称单机应用，软件所有数据都保存在电脑本地硬盘中
  - 优点：易于使用，结构简单
  - 缺点：数据难以共享、安全性差、更新不及时
- 联机时代（Client-Server模式）
  - Client/Server结构（C/S结构）是指客户端和服务器
  - 结构优点：数据方便共享，安全性高
  - 缺点：必须安装客户端，**升级与维护困难**
- 互联网时代（Broswer-Server模式）
  - Broswer-Server（B/S）模式即浏览器和服务器架构模式
  - 优点：开发简单，**无需安装客户端**，**数据易于共享**
  - 缺点：相较于C/S模式，执行速度与用户体验相对较弱

### B/S模式执行流程

![image-20220427214156145](https://s2.loli.net/2022/04/27/iYJx3Xse6DuK5ht.png)

![image-20220427214329415](https://s2.loli.net/2022/04/27/eYVJlUFKdZi8RDM.png)

### 请求与相应

- 从浏览器发出送给服务器的数据包称为”请求“
- 从服务器返回给浏览器称为“响应”

### J2EE

- 概念

  - J2EE（Java 2 Platform Enterprise Edition）"Java 2
    企业版"

  - B/S模式开发Web应用就是J2EE最核心的功能

  - J2EE由13个功能模块成

- 13个功能模块

  - ![image-20220427214746006](https://s2.loli.net/2022/04/27/EFi6wDMKHn21qXJ.png)

### Apach Tomcat

- Tomcat是Apache软件基金会旗下一款免费的开放源代码的Web应用服务器程序
- Tomcat是运行Servlet（服务器小程序）的容器

### J2EE与Tomcat的关系

- J2EE是一组技术规范和指南，具体实现由软件厂商决定
- Tomcat是J2EE Web（Servlet和JSP）标准的实现者
- J2SE是J2EE运行的基石，运行Tomcat离不开J2SE

### Servlet

- Servlet（Server Applet）服务器小程序，主要功能用于生成动态Web内容
- Servlet是2EE最重要的组成部分，也是我们学习的重点

### Tomcat与Servlet的关系

![image-20220427215954022](https://s2.loli.net/2022/04/27/3iWnPMDle9Uhguz.png)

### Tomcat安装（略)

## Servlet开发

### 第一个Servlet （见eclipse）

#### 图解执行流程

1. 在浏览器输入`http://localhost:8080/FirstServlet/hi?name=jackson`，该信息通过request发送给Tomcat
2. Tomcat收到信息后
   1. 发送的url是`/hi`,从web.xml配置文件寻找是否有匹配的servlet（url-pattern是否有`/hi`这一项）
   2. 有匹配的url-pattern,映射（mapping）的servlet-name是first
   3. 再次在servlet里寻找是否有first的servlet-name对应的servlet-class
   4. 有匹配的servlet-class，servlet-name是`servlet-class：com.cy.servlet.FirstServlet`对应的别名
3. Tomcat创建service()类对象，并且执行FirstServlet方法，service()类对象就是为FirstServlet方法提供响应支持的
4. FirstServlet打印输出`<h1 style='color:red'>hi," + name + "</h1><hr/>`（name作为参数进行接收），Tomcat将该字符串原封不动给地发送给浏览器（response）
5. 浏览器接收到字符串后，对其进行解释，展现在页面上

![image-20220428082909411](https://s2.loli.net/2022/04/28/OmtTzHMxLJCkvR7.png)

#### 习题

1. 当普通类继承（HttpServlet）就会变为Servlet类
2. ![image-20220428090526098](https://s2.loli.net/2022/04/28/NRfuVGiU1JYg97D.png)
   - servlet-class
3. ![image-20220428090628616](https://s2.loli.net/2022/04/28/DBJcyPoTV8qKpAt.png)
   - B

### 标准的Java Web工程

- ![image-20220428142824352](https://s2.loli.net/2022/04/28/BJDI9nZQ4uLAfkr.png)
- 在WebContent文件夹下创建html/jsp文件，即可在网页端显示
  - ![image-20220428150437847](https://s2.loli.net/2022/04/28/JtS7BTkQDsEeu6Z.png)
- 习题
  - 关于Java Web工程结构，以下说法错误的是？（选择一项）
  - A web.xml文件存放到/WEB-INF/lib目录下
    - ×，存放到WEB-INF目录下，lib下存放web应用依赖的jar包
  - B /WEB-INF是WEB应用的安全目录
  - C web.xml是部署描述符文件
  - D /WEB-INF/classes用于存放编译后的字节码文件

### Sevlet开发步骤

- 创建Servlet类，继承**HttpServlet**
- 重写service方法，编写程序代码
- 配置web.xml，绑定url（`<url-pattern>`）

### Servlet访问方法

- `http://IP地址:端口/context-path/url-mapping`
- 远程访问使用IP地址，本地访问**localhost(127.0.0.1)**
- context-path成为“上下文路径”，默认为工程名

### 请求参数

- 请求参数是指浏览器通过请求向Tomcat提交的数据 
- 请求参数通常是用户输入的数据，待Servlet进行处理 
- 举例：student.xml
  - ![image-20220428164852122](https://s2.loli.net/2022/04/28/djc87DnkbtJHZ9u.png)
  - ![image-20220428164836954](https://s2.loli.net/2022/04/28/MYj3utf5ZporTcC.png)

### Servlet接受请求参数

- request.getParameter() - 接收单个参数
-  request.getParameterValues() - 接收多个**同名参数**

```java
// 1. 创建Servlet类，继承HttpServlet
public class SampleServlet extends HttpServlet {
	//2. 重写service方法，编写程序代码 
	public void service(HttpServletRequest request, HttpServletResponse response) throws IOException {
		String name = request.getParameter("name");
		String mobile = request.getParameter("mobile");
		String sex = request.getParameter("sex");
		String[] specs = request.getParameterValues("spec");
		PrintWriter out = response.getWriter();//向浏览器输出的数据流
		out.println("<h1>name:" + name + "</h1>");
		out.println("<h1>mobile:" + mobile + "</h1>");
		out.println("<h1>sex:" + sex + "</h1>");
		for(int i=0; i<specs.length; i++) {
			out.println("<h2>spec:" + specs[i] + "</h2>");
		}
		out.println("<a href='http://www.baidu.com'>Baidu</a>");
	}
}
```

### Get与Post请求方法

- Get方式是将数据通过在URL附加数据显性向服务器发送数据。（默认采用）
  - `http://localhost:8080/FirstServlet/sample?name=zhangsan`
  - `method="get"`:会在地址栏显示出请求参数
- Post方式会将数据存放在”请求体”中隐性向服务器发送数据
  - `http://localhost:8080/FirstServlet/sample`
  - `method="post"`:地址栏请求参数隐藏
  - 请求体：name=zhangsan
- Get与Post处理方式
  - 所有请求-service()方法
  - Get请求-doGet()方法
  - Post请求-doPost()方法
- Get与Post应用场景
  - Get常用于不包含敏感信息的查询功能
    - 例如:`https://www.baidu.com/s?wd=imooc&rsv_spt=1`
  - Post用于安全性要求较高的功能或者服务器的”写“操作
    - 用户登录 
    - 用户注册 
    - 更新公司账目
- 习题
  - Get和Post请求会经过service()方法进行转发，无论service()方法是否重写
    - ×，可以不经过service，经过doGet()和doPost()
  - Post请求提交的数据，可以在浏览器调试页面的Form Data中查看
    - √
  - Get请求提交的数据，可以在浏览器调试页面的Query String Parameters中查看
    - √
  - Get提交的数据不能在url地址中查看
    - 错，get提交的可以，post的不行

```java
// RequestMethodServlet.java
package com.cy.servlet;

import java.io.IOException;

import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class RequestMethodServlet extends HttpServlet{
	//处理get请求
	public void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
		String name = request.getParameter("name");
		response.getWriter().println("<h1 style='color:green'>" + name + "</h1>");
	}
	//处理post请求
	public void doPost(HttpServletRequest request, HttpServletResponse response) throws IOException {
		String name = request.getParameter("name");
		response.getWriter().println("<h1 style='color:red'>" +  name + "</h1>");
	}
}
```

### Servlet生命周期

1. 装载——web.xml

2. 创建——构造函数

3. 初始化——init()

4. 提供服务——service()

5. 销毁——destroy()

   ![image-20220428210918586](https://s2.loli.net/2022/04/28/QRgq3LlSWB8DhfP.png)

   - 刷新界面，创建+初始化+提供服务
   - debug中进行界面修改，销毁

```java
package com.cy.servlet;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class FirstServlet extends HttpServlet{

	public FirstServlet() {
		System.out.println("正在创建FirstServlet对象");
	}
		
	@Override
	public void init(ServletConfig config) throws ServletException {
		System.out.println("正在初始化FirstServlet对象");
	}

	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		//接受请求来的参数
		String name = request.getParameter("name");
		String html = "<h1 style='color:red'>hi," + name + "</h1><hr/>";
		System.out.println("返回给浏览器的相应数据为：" + html);
		PrintWriter out = response.getWriter();
		out.println(html);//将html发送回浏览器
	}
	
	@Override
	public void destroy() {
		System.out.println("正在销毁servlet对象"); 
	}
}
```

## 注解简化设置

### 使用注解简化配置

- Servlet 3.x 之后引入了“注解Annotation”特性
- 注解用于**简化**Web应用程序的配置过程
- Servlet核心注解：@WebServlet
- 习题
  - 使用注解配置了Servlet，web.xml中也可以再同样的配置一遍
    - ×，报错，Server Tomcat v9.0 Server at localhost failed to start
  - 使用注解配置了Servlet后，还可以使用web.xml再配置另一个url-pattern的值，不和注解配置的重名就行
    - √，经测试两个url都可以运行
  - 配置Servlet的注解的正确写法是@Servlet("/imooc")
    - ？
  - 配置Servlet注解中的参数指的是Servlet的映射地址
    - ？

```xml
<!-- @WebServlet("/anno")等同于以下配置文件，在该类上@即可 -->
  <servlet>
  	<servlet-name>annotation</servlet-name>
	<servlet-class>com.cy.servlet.AnnotationServlet</servlet-class>
  </servlet>
  <servlet-mapping>
  	<servlet-name>annotation</servlet-name>
  	<url-pattern>/anno</url-pattern>
  </servlet-mapping>
</web-app>
```

### 启动时加载Servlet

- web.xml使用`<load-on-startup>`设置启动加载
- `<load-on-startup>0~9999</load-on-startup>`
- 启动时加载在工作中常用于系统的预处理

```xml
<!-- //urlPatterns="/unused"用不到，但得有 --> 
<!-- @WebServlet(urlPatterns="/unused",loadOnStartup=2)等于以下配置 --> 
<!-- 按照<load-on-startup>中0，1，2的顺序启动加载 --> 
  <servlet>
	  <servlet-name>analysis</servlet-name>
 	  <servlet-class>com.cy.servlet.AnalysisServlet</servlet-class>
 	  <load-on-startup>2</load-on-startup>
   </servlet> 
```

## 自由编程

### 1.Servlet传参

使用Servlet在页面输出商品类别名称，商品类别名称通过url地址进行传递，在Servlet中获取类别名称并输出。url地址如下：`localhost:8080/ServletProj/ShopServlet?category=book`

- 见项目ServletProj

### 2.

使用Servlet计算n以内自然数的累加和，并输出，参数n通过url地址传递

![image-20220428223127251](https://s2.loli.net/2022/04/28/6DnU9OKYCQjm425.png)

提示：在Servlet中获取的参数是字符串类型，需要使用Integer.parselnt(String s)方法转换为整型再进行计算。

### 3.

- 使用Servlet完成加法计算器：

  1. 创建一个html页面，定义一个表单，点击计算按钮，提交给Servleti进行处理

  2. 将表单数据传递给Servlet，并将计算结果打印输出在页面上.

     运行效果参见下图：

![image-20220428223229818](https://s2.loli.net/2022/04/28/alunYC9mEBdrSAH.png)
