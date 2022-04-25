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
    ```

    

    

  - XML Schema

## Java解析XML

## XPath路径表达式



# Serlet入门

