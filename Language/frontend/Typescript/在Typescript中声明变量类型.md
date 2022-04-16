# 第一单元 介绍
在网页界面运行方法
- module.html右击选择open with live server
- 在module下tsc运行即可
# 第二单元 Typescript中的类型概述
## 声明let和const变量
- 区别
    - let声明可以在不进行初始化的情况下完成
    - const声明始终使用值进行初始化。声明分配后，无法再重新分配 ？

### 练习-TypeScript 中的类型推理
- 通过显式/隐式类型推理将类型和变量关联
- 推荐显式，使用`variableName:type`语法
    - `let myVariable:number`：声明为数字类型，但不初始化
    - `let myVariable:number = 10`：声明为数字类型，并初始化
- 隐式，通过类型推理标识变量类型，和js格式相同
    - `let myVariable = 10`:推理变量类型为number，用值10初始化

```TypeScript
let x: number;   //* Explicitly declares x as a number type
let y = 1;       //* Implicitly declares y as a number type
let z;           //* Declares z without initializing it

x = "one";       //* Type 'string' is not assignable to type 'number'

z = 1;           //* declares z as a any type
z = "0ne";
```
## TypeScript 中的类型和子类型
   ![20220317102738](https://s2.loli.net/2022/03/17/6jH984LGCwvNbZT.png)
### 任何类型 （any/unknown）
- any类型(JS)
    - 无限制表示任何JavaScript值的一种类型
    - 允许重新分配不同类型的值
    ```Typescript
        let randomValue: any = 10;
        randomValue = 'Mateo';   // OK
        randomValue = true;      // OK

        console.log(randomValue.name);  // Logs "undefined" to the console
        randomValue();                  // Returns "randomValue is not a function" error
        randomValue.toUpperCase();      // Returns "randomValue is not a function" error
    ```
    - 编译此示例不会引发错误，因为any类型包含每种可能类型的值，不进行类型检查，不强制在调用、构造、访问这些属性之前进行任何检查
    - 此示例中，any类型可以调用：
        - 该类型不存在的属性
        - randomValue作为函数
        - 仅适用于string类型的方法
    - 注意：any的便利以牺牲类型安全性为代价，在TS中尽量避免使用
- unkwown类型（TS）
    - 可以将任何值赋予类型unknown，但无法访问unknown属性，不能调用、构造它们
    ```Typescript
        let randomValue: unknown = 10;
        randomValue = true;
        randomValue = 'Mateo';

        console.log(randomValue.name);  // Error: Object is of type unknown
        randomValue();                  // Error: Object is of type unknown
        randomValue.toUpperCase();      // Error: Object is of type unknown
    ```  
- any和unkwown的核心区别
    - 与unkwown类型的变量进行交互会产生“编译器错误”
    - any绕过编译检查，并在运行时评估对象，若该方法/属性存在，则呈现预期效果


### 基元类型
- 分类：boolean,number,string,void,null,underfined,枚举,enum
- 布尔类型（true、false）
    ```TypeScript
        let flag: boolean;
        let yes = true;
        let no = false;
    ```
- 数字模型和大整数类型
    - 浮点数类型（number）
    - 大整数类型（bigint）
    ```TypeScript
        let x: number;
        let y = 0;
        let z: number = 123.456;
        let big: bigint = 100n;
    ```
- 字符串类型
    - 关键字string表示以 Unicode UTF-16 代码单元的形式存储的字符序列
    - 使用双引号（"）和单引号(')将字符串数据括起来
    ```TypeScript
        let s: string;
        let empty = "";
        let abc = 'abc';
    ```
    - 在TS中，可以使用模板字符串，可跨越多行并具有嵌入式表达式，这些字符串由反撇号/反引号 (`) 字符括起，并且嵌入式表达式的形式为${ expr }   ？
     ```TypeScript
        let firstName: string = "Mateo";
        let sentence: string = `My name is ${firstName}.
        I am new to TypeScript.`;
        console.log(sentence);
        Input:
        My name is Mateo.
        I am new to TypeScript.
    ```   
- void、null、underfined类型
    - void：指示不存在值，例如存在于没有返回值的函数
    - null和underfined类型是所有其他类型的字类型，无法显式引用null和underfined类型，使用null和undefined字面量只能引用这些类型的值
- 枚举类型（enum，TS补充）
    ```Typescript
        enum ContractStatus {
            Permanent = 1,//默认为0，可设置其他值为初始值
            Temp,
            Apprentice
        }

        let employeeStatus: ContractStatus = ContractStatus.Temp;
        console.log(employeeStatus);
        console.log(ContractStatus[employeeStatus]);

        Input:2 Temp
    ```

### 对象类型和类型参数
- 对象类型是所有类、接口、数组和字面量类型（不是基元类型的任何类型）。
- 类和接口类型将通过类和接口声明引入，并通过在其声明中为其指定的名称进行引用。类和接口类型可以是具有一个或多个类型参数的通用类型。
- 举例：Array类型

### 类型断言（类型转换）
- 概述
    - 将变量视为其他数据类型，使用类型断言
    - 不执行数据的特殊检查或重组，告诉编译器“相信我，我知道我在做什么”
    - 对运行无影响，仅由编译器使用
- 语法
    - as语法(首选)
    `(randomValue as string).toUpperCase();//toUpperCase()方法用于把字符串改成大写`
    - “尖括号”语法
    `(<string>randomValue).toUpperCase();`
- 注意
    - as 是首选语法。 使用 < > 进行类型转换时，某些 TypeScript 应用程序（例如 JSX）可能会发生混淆。
```Typescript
    let randomValue: unknown = 10;

    randomValue = true;
    randomValue = 'Mateo';

    if (typeof randomValue === "string") {//typeof 返回未经计算的操作数的类型的类型
        console.log((randomValue as string).toUpperCase());    //* Returns MATEO to the console.
    } else {
        console.log("Error - A string was expected here.");    //* Returns an error message.
    }
```

### 类型保护
- 概述
    - 在if块中使用typeof在运行时检查表达式的类型，即“类型保护”
    `if (typeof randomValue === "string")`
- 相关变量类型
    ![20220320170052](https://s2.loli.net/2022/03/20/nfaWZYwFQ4BsXJu.png)

### 联合类型（Union）
- 联合类型描述的值可以是几种类型之一，当值不受控制时（来自库、API、用户输入值），有很大帮助
- 联合类型将赋值限制为指定的类型，而any类型都没有限制
- 使用竖线（|）分割每种类型
```Typescript
    let multiType: number | boolean;
    multiType = 20;         //* Valid
    multiType = true;       //* Valid
    multiType = "twenty";   //* Invalid   
```
- 使用类型保护，可以轻松地使用联合类型的变量。 在此示例中，add 函数可接受两个值，它们可以是 number 或 string。 如果两个值都是数字类型，则将它们相加。 如果两者都是字符串类型，则将它们连接起来。 否则，将引发错误。
```Typescript
    function add(x: number | string, y: number | string) {
        if (typeof x === 'number' && typeof y === 'number') {
            return x + y;
        }
        if (typeof x === 'string' && typeof y === 'string') {
            return x.concat(y);
        }
        throw new Error('Parameters must be numbers or strings');
    }
    console.log(add('one', 'two'));  //* Returns "onetwo"
    console.log(add(1, 2));          //* Returns 3
    console.log(add('one', 2));      //* Returns error   
```

### 交叉类型（Intersection）
- 组合两个或多个类型以创建具有现有类型的所有属性的新类型
- 将现有类型加在一起，以获得具有所需所有功能的单个类型
- 用与号 (&) 分隔每种类型
- 交叉类型最常与接口一起使用。
```Typescript
    // 以下示例定义了两个接口 Employee 和 Manager，然后创建了一个称为 ManagementEmployee 的新交叉类型，该交叉类型将两个接口中的属性组合在一起。
    interface Employee {
        employeeID: number;
        age: number;
    }
    interface Manager {
        stockPlan: boolean;
    }

    type ManagementEmployee = Employee & Manager;//交叉

    let newManager: ManagementEmployee = {
        employeeID: 12345,
        age: 34,
        stockPlan: true
    };
```

### 文本类型
- 字面量是集合类型的更具体的子类型。
    -  这意味着 "Hello World" 是 string，但类型系统中的 string 不是 "Hello World"。
- TS中提供了三组字面量类型：string、number 和 boolean。
    - 通过使用字面量类型，可以指定字符串，数字或布尔值必须具有的确切值（例如，“是”、“否”或“或许”）。
#### 字符量收缩 ？
- 当在TS使用vet和let声明变量时，告知编译器该变量有可能更改内容，使用let声明变量将键入该变量（例如，作为string）,从而允许无限数量的可能值  ？
- 相反，使用const声明变量将通知TS该对象永不更改。使用const声明会将其键入值（例如，“Hello World”）
- 从无限数量的可能案例变为更小的有限数量的可能案例的过程称为收缩。
#### 定义字符量类型
```TS
    type testResult = "pass" | "fail" | "incomplete";
    let myResult: testResult;
    myResult = "incomplete";    //* Valid
    myResult = "pass";          //* Valid
    myResult = "failure";       //* Invalid
    type dice = 1 | 2 | 3 | 4 | 5 | 6;
    let diceRoll: dice;
    diceRoll = 1;    //* Valid
    diceRoll = 2;    //* Valid
    diceRoll = 7;    //* Invalid
```

### 集合类型
#### 数组
- 含有相同值类型的组
    ```TS
        //用元素类型后跟方括号 ([ ]) 来表示该元素类型的数组
        let list: number[] = [1, 2, 3];
        //通过语法 Array<type> 使用泛型 Array 类型
        let list: Array<number> = [1, 2, 3];
        //注意：不要混用
    ```
#### 元组
- 含有混合类型的组
    ```TS
        //创建包含 string 和 number 的元组
        let person1: [string, number] = ['Marcia', 35];  
        //尝试向数组添加其他项，报错（array中的元素固定，只包含一个string和一个numeric值），值的顺序必须与类型的顺序匹配
        let person1: [string, number] = ['Marcia', 35, true];
    ```

### 在TS中运用类型

### 知识检查
![知识检查](https://docs.microsoft.com/zh-cn/learn/modules/typescript-declare-variable-types/9-knowledge-check)

# 第三单元 在TypeScript中实现接口 
## TypeScript中的接口概述
### 接口
- 使用接口来描述对象、命名和参数化对象的类型，以及将现有的命名对象类型组成新的对象类型
```TS
    //通过类型Employee的变量来实现接口
    //通过传入firstName和lastName属性的值并指定fullname方法需结合使用first和lastname属性并返回结果
    interface Employee {
        firstName: string;
        lastName: string;
        fullName(): string;
    }
```
- 注意
    - 不会初始化/实现其中声明的属性，接口唯一任务是描述类型
    - 定义代码协定所需的内容，实现接口的变量、函数或类通过所需的实现详细信息来满足协定
    - 定义接口后，可以将其用作类型，并可享受到类型检查和 Intellisense 的所有好处
的对象类型
```TS
    let employee: Employee = {
        firstName : "Emil",
        lastName: "Andersson",
        fullName(): string {
            return this.firstName + " " + this.lastName;
        }
    }

    employee.firstName = 10;  //* Error - Type 'number' is not assignable to type 'string'
```

### 在 TypeScript 中使用接口的原因
- 接口通常是任意两个 TypeScript 代码段之间的关键联系点，尤其是在使用现有 JavaScript 代码或内置 JavaScript 对象时
- 可以使用接口执行以下操作
    - 为常用类型创建简写名称。即使是使用一个简单的接口（如前面示例中声明的接口），你仍然可以享受 Intellisense 和类型检查带来的好处。
    - 在一组对象中保持一致性，因为实现接口的每个对象都在相同的类型定义下运行。 当你与开发人员团队合作并想要确保将正确的值传递到属性、构造函数或函数时，这会很有用。 例如，实现接口的对象必须实现接口的所有必需成员。 因此，如果未传递正确类型的所有必需参数，TypeScript 编译器将引发错误。
    - 描述现有的 JavaScript API 并阐明函数参数和返回类型。 这在使用 jQuery 等 JavaScript 库时特别有用。 接口可以让你清楚地了解函数的期望值和返回值，而无需重复访问文档。

### 接口和类型别名的区别
```TS
    type Employee = {
        firstName: string;
        lastName: string;
        fullName(): string;
    }
```
- 相同
    - 类型别名是数据类型（例如联合、基元、交集、元组或其他任何类型）的定义
    - 接口是描述数据形状（例如对象）的一种方法。 类型别名可以像接口一样使用
- 差异
    - 不能重新打开类型别名以添加新属性，而接口始终是可扩展的
    - 此外，只能使用类型别名描述并集或元组

### 在 TypeScript 中声明和实例化接口
- 以interface关键字开头，后接接口名称（标识符）
- 接口名称不能是类型系统中预定义的类型名称之一
- 接口名称采用PascalCase形式（大驼峰）
    - 多个词组成，每个词首字母都大写，如`FisrtName`和`LastName`
- 定义接口的属性（或成员）及其类型
![20220403105048](https://s2.loli.net/2022/04/03/pbLJxqVuyU3mY2l.png)

```TS
//声明接口IceCream（描述类型，属性/方法）
interface IceCream {
   flavor: string;
   scoops: number;
}

//将变量iceCream声明为IceCream类型，分配必需属性
let iceCream: IceCream = {
   flavor: 'vanilla',
   scoops: 2
}

console.log(iceCream.flavor);

//创建tooManyScoops 函数：变量dessert为IceCream类型
function tooManyScoops(dessert: IceCream) {
   if (dessert.scoops >= 4) {
      return dessert.scoops + ' is too many scoops!';
   } else {
      return 'Your order will be ready soon!';
   }
}

console.log(tooManyScoops({flavor: 'vanilla', scoops: 3}));
```

### 在 TypeScript 中扩展接口
- 扩展接口规则
    - 必须从所有接口实现所有必需的属性。
    - 如果属性具有完全相同的名称和类型，则两个接口可以具有相同的属性。
    - 如果两个接口具有名称相同但类型不同的属性，则必须声明一个新属性，以使生成的属性是这两个接口的子类型。
- 扩展接口举例
```TS
interface IceCream {
   flavor: string;
   scoops: number;
}

interface Sundae extends IceCream{
    sauce:'chocolate'| 'caramel'| 'strawberry';
    nuts?:boolean;
    whippedCream?:boolean;
    instruction?:boolean;
}

let myIceCream: Sundae = {
    flavor: 'vanilla',
    scoops: 2,
    sauce: 'caramel',
    nuts: true
}

function tooManyScoops(dessert: Sundae) {
    if (dessert.scoops >= 4) {
        return dessert.scoops + ' is too many scoops!';
    } else {
        return 'Your order will be ready soon!';
    }
}
console.log(tooManyScoops({flavor: 'vanilla', scoops: 5, sauce: 'caramel'}));
```

### 在 Typescript 中使用接口的其他方法
#### 创建可索引类型
```TS
//IceCreamArray接口将索引签名声明为 number 并返回 string 类型
interface IceCreamArray {
    [index: number]: string;
}

let myIceCream: IceCreamArray;
myIceCream = ['chocolate', 'vanilla', 'strawberry'];
let myStr: string = myIceCream[0];
console.log(myStr);

//Run:chocolate
```
#### 使用接口描述JS API
```TS
//fetch API 是一个本机 JavaScript 函数，可用于与 Web 服务进行交互。
//此示例为 JSON 文件中的返回类型声明一个名为 Post 的接口，然后将 fetch 与 async 和 await 结合使用以生成强类型化响应。
TypeScript
const fetchURL = 'https://jsonplaceholder.typicode.com/posts'
// Interface describing the shape of our json data
interface Post {
    userId: number;
    id: number;
    title: string;
    body: string;
}
async function fetchPosts(url: string) {
    let response = await fetch(url);
    let body = await response.json();
    return body as Post[];
}
async function showPost() {
    let posts = await fetchPosts(fetchURL);
    // Display the contents of the first item in the response
    let post = posts[0];
    console.log('Post #' + post.id)
    // If the userId is 1, then display a note that it's an administrator
    console.log('Author: ' + (post.userId === 1 ? "Administrator" : post.userId.toString()))
    console.log('Title: ' + post.title)
    console.log('Body: ' + post.body)
}

showPost();
```

# 使用 TypeScript 开发类型函数
## 在 TypeScript 中创建函数
### 命名函数
TS与JS区别
- 可以为函数的参数和返回值提供类型注释
```TS
//接受两个 number 类型的参数，并返回 number
function addNumbers (x: number, y: number): number {
   return x + y;
}
addNumbers(1, 2);
```

### 匿名函数
- 对比命名函数addNumbers是函数名，匿名函数把函数匿名（没有名称）了，直接把这个function表达式赋值给addNumbers了，使用这个变量即可调用函数
```TS
let addNumbers = function (x: number, y: number): number {
   return x + y;
}
addNumbers(1, 2);

let total = function(input) 

let total = function(input:number[]:number)
```

### 箭头函数