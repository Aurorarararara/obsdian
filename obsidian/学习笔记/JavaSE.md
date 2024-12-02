# 1. IDEA包

## 1.1 包的命名

### 1.1.1 命名规则

只能包含数字、字母、下划线、小圆点。但不能用数字开头，不能是关键字或保留字

### 1.1.2 命名规范

一般是小写字母+小圆点  
一般是com.公司名字.项目名.业务模块名

### 1.1.3 常用的包

- java.lang.* //lang包是基本包，默认引入，不需要再引入
- java.util.*  //util包，系统提供的工具包，工具类，使用Scanner
- java.net.*  //网络包，网络开发
- java.awt.* //是做Java的界面开发，GUI

## 1.2 访问修饰符

java提供四种访问控制修饰符号，用于控制方法和属性(成员变量)的访问权限(范围)：

1. 公开级别：用public修饰，对外公开
2. 受保护级别：用protected修饰，对子类和同一包中的类公开
3. 默认级别：没有修饰符号，向同一个包的类公开
4. 私有级别：用private修饰，只有类本身可以访问，不对外公开

|   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|
||访问级别|访问控制修饰符|同类|同包|子类|不同包|
|1|公开|public|✔|✔|✔|✔|
|2|受保护|protected|✔|✔|✔|❌|
|3|默认|没有修饰符|✔|✔|❌|❌|
|4|私有|private|✔|❌|❌|❌|
|使用事项：|||||||

- 修饰符可以用来类中的属性，成员方法以及类
- 只有默认的和public才能修饰类，并且遵循上述访问权限的特点
- 成员方法的访问规则和属性完全一样

# 2. java基础

## 2.1 Hello World

```
public class Hello {
	//编写一个主方法main
	public static void main(String[] args){
		System.out.println("hello,world~");
	}
}
```

【解释】：

1. public class Hello 表示Hello是一个类，是一个public的公有的类
2. Hello{ }表示一个类的开始和结束
3. public static void main(String[] args)表示主方法 程序的入口
4. main(){}表示方法的开始和结束
5. System.out.println("hello,world~")表示输出hello world到屏幕
6. ;表示语句结束

### 2.1.1 Java开发的注意事项

- 一个原文件**最多只能有一个public的类**，其他类个数不限(编译后，每一个类都对应一个class)
- 如果原文件包含一个public类，文件名必须和public类同名
- 可以将main写在非public类中，这样入口方法就是非public的main方法

### 2.1.2 Java的代码规范

- 类和方法的注释要以javadoc的方法来写
- 源文件要保存成UTF-8
- 行宽不用超过80字符

#### 2.1.1.1 DOS命令（了解）

##### 2.1.1.1.1相对路径&绝对路径

- 相对路径：从当前目录开始定位，形成的一个路径
- 绝对路径：从顶级目录d，开始定位，形成的路径

##### 2.1.1.1.2常用命令

1. 查看当前目录有什么内容 dir
2. 切换到C盘 cd /D c
3. 切换到上一级 cd ..
4. 切换到根目录 cd \
5. 查看指定目录下的所有子级目录 tree
6. 清屏 cls
7. 退出DOC exit
8. 创建目录 md
9. 删除目录 rd
10. 拷贝文件 copy
11. 删除文件 del
12. 输入内容到文件 echo
13. 输入到一个空文件type
14. 剪切 move

### 2.1.3 Java API文档

Java提供的基本编程接口，中文在线文档： [https://www.matools.com](https://www.matools.com)

## 2.2 计算机基础

### 2.2.1 转义字符

|   |   |
|---|---|
|转义字符|功能|
|\t|一个制表位，实现对齐的功能|
|\n|换行符|
|\\|一个\|
|\"|一个"|
|\'|一个'|
|\r|一个回车|

### 2.2.2 注释

- 单行注释  
    格式：//注释文字
- 多行注释  
    格式：/ /
- 文档注释
- 格式

```
/**
	*
	*
	*
*/
```

网页生成：javadoc -d f:\\temp -author -version Hello.java

### 2.2.3 +号的使用

1. 当左右两边都是数值型时，则做加法运算
2. 当左右两边有一方为字符串，则做拼接运算
3. 运算顺序从左到右

- 100 + 98 = 198
- "100" + 98 = 10098
- 100 + 3 + "hello" = 103hello
- "hello" + 100 + 3 = hello1003

### 2.2.4 基本数据类型转换

#### 2.2.4.1 自动类型转换

当java程序在进行赋值或者运算时，**精度小的类型自动转换为精度大的数据类型**，这个就是自动类型转换  
数据类型按精度（容量）大小排序

- char -> int -> long -> float -> double
- byte -> short -> int -> long -> float ->double

#### 2.2.4.2 强制类型转换

自动类型转换的逆过程，将容量大的数据类型转换为容量小的数据类型。使用时加上强制转换符()，但可能会造成精度降低或者溢出

#### 2.2.4.3 基本数据类型和String类型的转换

- 基本类型转String类型  
    语法：将基本类型的值+""即可
- String类型转基本数据类型  
    语法：通过基本类型的包装类调用passXX方法即可

### 2.2.5 逻辑运算符

- a&b: &   逻辑与：  
    规则：当a和b同时为true，则结果为true，否则为false
- a&&b: &&   短路与  
    规则：当a和b同时为true，则结果为true，否则为false
- a|b: |叫逻辑或  
    规则：当a和b，有一个为true，则结果为true，否则为false
- a||b: ||叫短路或  
    规则：当a和b，有一个为true，则结果为true，否则为false
- !a：叫取反，非运算  
    规则: 当a为true，则结果为false，当a为false，结果为true
- a^b：叫逻辑异或  
    规则：当a和b不同时，则结果为true没否则为false

**&&与和&的区别**  
1.&&短路与：如果第一个为false，则第二个条件不会判断，最终结果为false，效率高  
2.&逻辑与：不管第一个条件是否为false，第二个条件都要判断，效率低  
3.开发中，使用的基本是短路与&&，效率高

### 2.2.6 键盘输入

- 导入该类所在的包
- 创建该类对象(声明变量)
- 调用里面的功能

```
import java.until.Scanner;//把java.until下的Scanner导入
public class Input{
	public static void main(String[] args){
	Scanner scanner = new Scanner(System.in);
	System.out.println("请输入名字");
	}
}
```

### 2.2.7 进制

对于整数有四种表示方式：

1. 二进制：0, 1 满2进1 以ob或者oB开头
2. 十进制：0-9 满10进1
3. 八进制：0-7 满8进1，以数字0开头表示
4. 十六进制：0-9及（10）-F（15） 满16进1 以0x或0X开头表示。此处的A-F不区分大小写

```
//n1 二进制
int n1 = ob1010;//10
//n2 十进制
int n2 = 1010;//1010
//n3 八进制
int n3 = 01010;//520
//n4 十六进制
int n4 = 0x10101;//65793
```

### 2.2.8 位运算符

- **按位与 &** 两位全为1，结果为1否则为0
- **按位或 |** 两位有一个为1，结果为1，否则为0
- **按位异或 ^** 两位有一个为0，一个为1，结果为1，否则为0
- **按位取反 ~** 0->1, 1->0
- **算数右移>>** 低位溢出，符号位不变，并用符号位补溢出的高位  **进行/2的运算**
- **算数左移>>** 符号位不变，低位补0   **进行x2的运算**
- 逻辑右移也叫无符号右移，运算规则是：低位溢出，高位补0

### 2.2.9 原码、反码、补码

1. 二进制的最高位是符号位，0表示整数，1表示负数(0->0 1->-)
2. 正数的原码、反码、补码都一样(三码合一)
3. 负数的反码=它的原码符号不变，其他位取反(0->1 1->0)
4. 负数的补码=他的反码+1，负数的反码=负数的补码-1
5. 0的反码，补码都是0
6. java没有无符号
7. 在计算机运算的时候，都是以补码的方式来运算的
8. 当我们看运算结果的时候，要看他的源码

## 2.3 选择结果

### 2.3.1 单分支

基本语法：

```
if(条件表达式){
		执行代码块;(可以有多条语句)
}
```

### 2.3.2 双分支

基本语法

```
if(条件表达式){
		执行代码块1;
}
else{
		执行代码块2;
}
```

### 2.3.3 多分支

基本语法：

```
if(条件表达式1){
		执行代码块1;
}
else if(条件表达式2){
		执行代码块2;
}
……
else{
		执行代码块n;
}
```

## 2.4 循环结构

### 2.4.1 switch分支结构

基本语法:

```
switch(表达式){
	case 常量1:
	语句块1;
	break;

	case 常量2:
	语句块2;
	break;

	default语句块;
	break;
}
```

【解读switch】

- switch关键字，表示switch分支
- 表达式，对应一个值
- case 常量1:当表达式的值等于常量1，就执行语句块1
- break：表示退出switch
- 如果和case常量1匹配，就执行语句块1，如果没有匹配，就继续匹配case常量2
- 如果一个都没有匹配上，就执行default

【switch的细节讨论】

- 表达式的数据类型，应和case后的常量类型基本一致，或者可以自动转成可以相互比较的类型，比如输入的是字符，而常量是int
- switch(表达式)中表达式的返回值必须是：(byte, short, int, char, enum[枚举], String)
- case子句中的值必须是常量，而不能是变量
- default语句是可选的

#### 2.4.1.1 switch & if-else

- 如果判断的具体数值不多，而且符合byte、short、int、char、enum、String这6种类型。**建议使用switch语句**
- 其他情况：对区间判断，对结果为boolean类型判断，使用if，if的使用范围更广

### 2.4.2 for循环控制

基本语法：

```
for(循环变量初始化;循环条件;循环变量迭代){
		循环操作(语句);
}
```

【说明】for四要素：

- 循环变量初始化
- 循环条件
- 循环操作
- 循环变量迭代

### 2.4.3 while循环

基本语法：

```
循环变量初始化；
while(循环条件){
	循环体(语句);
	循环变量迭代;
}
```

### 2.4.4 do while循环

基本语法：

```
循环变量初始化；
do{
	循环体(语句);
	循环变量迭代;
}while(循环条件);
```

【说明】：先执行再判断=一定会执行一次

## 2.5 跳转控制语句

### 2.5.1 break

**当某个条件满足时，终止循环**

#### 2.5.1.1 标签的使用

```
label1:{...
label2:  {...
label3:    {...
				break label2;
			}
		  }
		}
```

- 可以通过标签指明要终止的是哪一层的语句块  
    【解读】
- break语句可以指定退出哪层
- label1是标签，名字有程序员指定
- break后指定到那个label就退出到那里
- 在实际的开发中尽量不要使用标签
- 如果没有指定break，默认退出最近的循环体

### 2.5.2 continue

基本介绍：

- continue语句用于结束本次循环，继续执行下一次循环
- continue也可以通过标签跳转(同break)

### 2.5.3 return

return使用在方法，表示跳出所在的方法  
==注意：==如果return写在main方法中，则退出程序

## 2.6 数组

### 2.6.1 声明数组变量

```
dataType[] arrayRefVar;//首选方法
或
dataType arrayRefVar[];//效果相同，但不是首选方法
```

### 2.6.2 创建数组

```
arrayRefVar = new dataType[arraySize]
```

- 使用dataType[arraySize]创建了一个数组
- 把新创建的数组的引用赋值给变量arryRefVar

### 2.6.3 For-Each循环

- 一种循环类型
- 能在不使用下标的情况下遍历数组

```
for(type element: array)
{
	System.out.println(element)
}
```

### 2.6.4 多维数组

#### 2.6.4.1 多维数组的动态初始化

```
type[][] typeName = new type[typeLength1][typeLength2];
int[][] a = new int[2][3]
```

### 2.6.5 初始化

--初始化数组中的数据

```
int[] arr = new int[4];

int[] arr = {1,4,5,8};

int[] arr = new int []{1,4,5,8};
```

### 2.6.6访问

```
//通过(数组名.length)可以获得数组的长度(元素的个数)
int[] arr = new int[5];
System.out.println(arr.length)

//通过下标/索引来访问数组中的元素
//下标从0开始，最大到(数组长度-1)
int[] arr = new int[3];

arr[0] = 100;
arr[1] = 100;
arr[2] = 100;
arr[3] = 400;
System.out.println(arr.length);
System.out.printkn(arr[arr.length-1]);
```

### 2.6.7 数组拷贝

编写代码 实现数组拷贝(内容复制) ==ArrayCopy.java==

- 将int[] arr1 = {10,20,30};拷贝到 arr2数组，要求数据空间是独立的

```
public class ArrayCopy{

	public static void main(String[] args){
	
		int[] arr1 = {10,20,30};
		//创建一个新的数组arr2，开辟新的数据空间
		//大小保证和arr1一样大
		int[] arr2 = new int[arr.length]
		//遍历arr1，把每个元素拷贝到对应的位置
		for(int i = 0; i < arr1.length; i++){
			arr2[i] = arr1[i];
		}
	}
}
```

## 2.7 方法

### 2.7.1 定义

五要素：修饰词 返回类型 方法名（参数列表）{ 方法体 }

```
public static double add(double d1,double d2){
	return d1+d2;
}
```

```
public class Task2 {    
    public static void average() {
        int java = 0;
        int sql = 0;
        int oracle = 0;
        java.util.Scanner input = new java.util.Scanner(System.in);
        System.out.print("请输入Java成绩：");
        java = input.nextInt();
        System.out.print("请输入SQL成绩：");
        sql = input.nextInt();
        System.out.print("请输入Oracle成绩：");
        oracle = input.nextInt();
        double result1 = (java + sql + oracle) * 1.0 / 3;
        System.out.println("该新生的平均成绩是:"+result1);
    } 
    public static void main(String[] args) {
        average();//第一次方法调用。        
        average();//第二次方法调用。
        average();//第三次方法调用。    
    }
}
```

### 2.7.2 重载

**注意点

- 方法名：必须相同
- 形参列表：不必相同(形参类型或个数或顺序，至少有一样不同，参数名无要求)
- 返回类型：无要求

```
public class OverLoad{

	public static void main(Stringp args){
	
	}
}

class myCakulator{
	//两个整数的和
	public int calculate(int n1, int n2) {
		return n1 + n2;
	}
	//一个整数，一个double的和
	public double calculate(int n1, double n2){
		return n1 + n2;
	}
	//一个double，一个int和
	calculate(double n2, int n1){
		return n1 + n2;
	}
	//三个int的和
	calculate(int n1,int n2,int n3){
		return n1 + n2 + n3;
	}
}
```

# 3. 面向对象

## 3.1 基本介绍

### 3.1.1 面向对象编程的三大特征

- 封装
- 继承
- 多态

## 3.2 封装

### 3.2.1 定义

把抽象出来的数据[属性]和对数据的操作[方法]封装在一起，数据被保护在内部，程序的其它部分只有通过被授权的操作(方法)，才能对数据进行操作

### 3.2.2封装的实现步骤

(1)将属性进行私有化【不能直接修改属性】  
(2)提供一个公共的(public)set方法，用于对属性判断并赋值  
public void setXxx(类型 参数名){  
//加入数据验证的业务逻辑  
属性 = 参数名;  
}  
(3)提供一个公共的get方法，用于获取属性的值  
public XX getXxx(){ //权限判断  
return xx;  
}

```
package com.cwz.encap;  
  
public class encap {  
    public static void main(String[] args) {  
        Person person = new Person();  
        person.setName("jack");  
        person.setAge(30);  
        person.setSalary(30000);  
        System.out.println(person.info());;  
  
    }  
}  
  
class Person{  
    public String name; //名字公开  
    private int age; //年龄私有化  
    private double salary; //工资私有化  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public int getAge() {  
        return age;  
    }  
  
    public void setAge(int age) {  
        this.age = age;  
        //判断  
        if(age >= 1 && age <= 120)  
        {  
            this.age = age;  
        }else{  
            System.out.println("你设置的年龄不对，需要在(1-120),给你默认年龄18岁");  
            this.age = 18;//给一个默认的年龄  
        }  
    }  
  
    public double getSalary() {  
        //加入对数据的校验,相当于增加了业务能力  
        if(name.length() >= 2 && name.length() <= 6){  
            this.name = name;  
        }else{  
            System.out.println("名字的长度不对，需要(2-6)个字符，默认名字");  
            this.name = "无名人";  
        }  
        return salary;  
    }  
  
    public void setSalary(double salary) {  
        this.salary = salary;  
    }  
    //写一个方法，返回属性信息  
    public String info(){  
        return "信息为 name= " + name + " age=" + age + " 薪水为 salary= " + salary;  
    }  
}
```

### 3.2.3 构造器与setXxx结合

```
package com.cwz.encap;  
  
public class encap {  
    public static void main(String[] args) {  
//        Person person = new Person();  
//        person.setName("jack");  
//        person.setAge(30);  
//        person.setSalary(30000);  
//        System.out.println(person.info());  
  
        //如果我们自己使用构造器指定属性  
        Person person = new Person("smith", 20, 50000);  
        System.out.println(person.info());  
        System.out.println(person.getSalary());  
  
    }  
}  
  
class Person{  
    public String name; //名字公开  
    private int age; //年龄私有化  
    private double salary; //工资私有化  
  
    //构造器 alt+insert    public Person(){  
  
    }  
  
    //有三个属性的构造器  
    public Person(String name, int age, double salary) {  
//        this.name = name;  
//        this.age = age;  
//        this.salary = salary;  
        //我们可以将set方法写在构造器中，这样仍然可以验证  
        setName(name);  
        setAge(age);  
        setSalary(salary);  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public int getAge() {  
        return age;  
    }  
  
    public void setAge(int age) {  
        this.age = age;  
        //判断  
        if(age >= 1 && age <= 120)  
        {  
            this.age = age;  
        }else{  
            System.out.println("你设置的年龄不对，需要在(1-120),给你默认年龄18岁");  
            this.age = 18;//给一个默认的年龄  
        }  
    }  
  
    public double getSalary() {  
        //加入对数据的校验,相当于增加了业务能力  
        if(name.length() >= 2 && name.length() <= 6){  
            this.name = name;  
        }else{  
            System.out.println("名字的长度不对，需要(2-6)个字符，默认名字");  
            this.name = "无名人";  
        }  
        return salary;  
    }  
  
    public void setSalary(double salary) {  
        this.salary = salary;  
    }  
    //写一个方法，返回属性信息  
    public String info(){  
        return "信息为 name= " + name + " age=" + age + " 薪水为 salary= " + salary;  
    }  
}
```

## 3.3 继承

- 利用继承来解决代码的复用性

### 3.3.1 继承的基本语法

class 子类 extends 父类{  
}

- 子类就会自动用于父类定义的属性和方法
- 子类又叫超类，基类
- 子类又叫做派生类

`student.java`

```
package com.cwz.extend_.xuesheng02;  
  
//父类，是 pupil 和 Graduate 的父类  
public class Student {  
    //共有属性  
    public String name;  
    public int age;  
    private double score;  
    //共有的方法  
    public void setScore(double score) {  
        this.score = score;  
    }  
    public void showInfo(){  
        System.out.println("学生名 " + name + " 年龄 " + age + " 成绩 " + score);  
    }  
}
```

`Pupil.java`

```
package com.cwz.extend_.xuesheng02;  
  
//让pupil继承Students  
public class Pupil extends Student{  
    public void testing(){  
        System.out.println("小学生 " + name + " 正在考小学数学..");  
    }  
}
```

`Graduate`

```
package com.cwz.extend_.xuesheng02;  
//让Graduate继承Students  
public class Graduate extends Student{  
    public void testing(){//和Pupil不一样  
        System.out.println("大学生 " + name + " 正在考大学数学..");  
    }  
}
```

`extends02`

```
package com.cwz.extend_.xuesheng02;  
  
import com.cwz.extend_.xuesheng01.Graduate;  
import com.cwz.extend_.xuesheng01.Pupil;  
  
public class extends02 {  
    public static void main(String[] args) {  
        com.cwz.extend_.xuesheng01.Pupil pupil = new Pupil();  
        pupil.name = "银角大王";  
        pupil.age = 10;  
        pupil.testing();  
        pupil.setScore(60);  
        pupil.showInfo();  
  
        System.out.println("======");  
  
        com.cwz.extend_.xuesheng01.Graduate graduate = new Graduate();  
        graduate.name = "金角大王";  
        graduate.age = 22;  
        graduate.testing();  
        graduate.setScore(100);  
        graduate.showInfo();  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712024194202-e3706702-3b6d-4107-8e8c-4689bc1cc7fd.png)

### 3.3.2 继承的细节

1. 子类继承了所有的属性和方法，但是私有属性不能在子类直接访问，要通过公共的方法去访问
2. 子类必须调用父类的构造器，完成父类的初始化
3. 当创建子类对象时，不管使用子类的哪个构造器，默认情况下总会去调用父类的无参构造器，如果父类没有提供无参构造器，则必须在子类的构造器中用super去指定使用的那个构造器完成对父类的初始化工作，否则编译器不会通过
4. 如果希望去指定调用父类的某个构造器，则显示的调用一下
5. super在使用时，需要放在构造器第一行
6. super()和this()都只能放在构造器第一行，因此这两个方法不能共存一个构造器
7. java所有类都是Object类的子类
8. 父类构造器的调用不限于直接父类！将一直往上回溯知道Object类(顶级父类)
9. 子类最多能继承一个父类(指直接继承)，即java中是单继承机制
10. 不能滥用继承，子类和父类之间必须满足is-a的逻辑关系

### 3.3.3 继承的本质分析(==重要==)

案例：分析当子类继承父类，创建子类对象时，内存到底发生了什么？  
==建立的查找关系==

`Father.java`

```
package com.cwz.extend_.Theory;  
  
public class Father extends GrandPa { //父类  
    String name = "大头爸爸";  
    int age = 39;  
}
```

`GrandPa.java`

```
package com.cwz.extend_.Theory;  
  
public class GrandPa { //爷爷类  
    String name = "大头爷爷";  
    String hobby = "旅游";  
}
```

`Son.java`

```
package com.cwz.extend_.Theory;  
  
public class Son extends Father { //子类  
    String name = "大头儿子";  
}
```

`extendsTheory.java`

```
package com.cwz.extend_.Theory;  
  
/**  
 * 讲解继承的本质  
 */  
public class extendsTheory {  
    public static void main(String[] args) {  
        Son son = new Son(); //内存的布局  
        //?-> 这时请大家注意，要按照查找关系来返回信息  
        //(1) 首先看子类是否有该属性  
        //(2) 如果子类有这个属性，并且可以访问，则返回信息  
        //(3)如果子类没有这个属性，就看父类有没有这个属性(如果父类有该属性，并且可以访问，就返回信息..)  
        //(4)如果父类没有就按照(3)的规则，继续找上级父类，知道Object...  
        System.out.println(son.name); //返回的就是大头儿子  
        System.out.println(son.age); //返回的就是39  
        System.out.println(son.hobby); //返回的就是旅游  
    }  
}
```

### 3.3.4 super关键字

#### 3.3.4.1 基本介绍

super代表父类的引用，用于访问父类的属性、方法、构造器

#### 3.3.4.2 基本语法

1. 访问父类的属性，但不能访问父类的private属性
2. 访问父类的方法，不能访问父类的private方法
3. 访问父类的构造器:suepr(参数列表)；只能放在构造器的第一句，只能出现一句

`A.java`

```
package com.cwz.super_;  
  
public class A {  
    public int n1 = 100;  
    protected int n2 = 200;  
    int n3 = 300;  
    private int n4 = 400;  
  
    public A(){}  
    public A(String name){}  
    public A(String name,int age){}  
    public void  test100(){  
  
    }    protected void  test200(){  
  
    }    void  test300(){  
  
    }    private void test400(){  
  
    }
}
```

`b.java`

```
package com.cwz.super_;  
  
public class B extends A{  
  
    //访问父类的属性，但不能访问父类的private属性  
    public void hi(){  
        System.out.println(super.n1 + " " + super.n2 + " " + super.n3 + " ");  
    }  
  
    //当问父类的方法，但不能访问父类的私有方法  
    public void ok(){  
        super.test100();  
        super.test200();  
        super.test300();  
        //super.test400(); 不能访问父类的私有方法  
    }  
  
    //访问父类的构造器:super(参数列表)；只能放在构造器的第一季，只能出现一句  
    public B(){  
        //super(); 无参  
        super("jack");  
    }  
}
```

**super给变成带来的便利**

1. 调用父类的构造器的好处(分工明确，父类属性由父类初始化，子类的属性由子类初始化)
2. 当子类中有和父类中的成员(属性和方法)重名时，为了访问父类的成员，必须通过super。如果没有重名，使用super、this、直接访问的效果是一样的。

`A.java`

```
package com.cwz.super_;  
  
public class A {  
    public int n1 = 100;  
    protected int n2 = 200;  
    int n3 = 300;  
    private int n4 = 400;  
  
    public A(){}  
    public A(String name){}  
    public A(String name,int age){}  
  
    public void cal(){  
        System.out.println("A类的cal方法");  
    }  
    public void  test100(){  
    }    protected void  test200(){  
    }    void  test300(){  
  
    }    private void test400(){  
    }}
```

`B.java`

```
package com.cwz.super_;  
  
public class B extends A{  
  
    //访问父类的属性，但不能访问父类的private属性  
    public void hi(){  
        System.out.println(super.n1 + " " + super.n2 + " " + super.n3 + " ");  
    }  
  
    public  void sum(){  
        System.out.println("B类的sum方法");  
        //希望调用父类A的cal方法  
        //这时，因为子类B没有cal方法，因此我可以使用下面三种方式：  
  
        //找cal方法时，顺序是，先找本类，如果有，则调用，如果没有，则找父类(如果有，并可以调用，则调用）  
        //如果父类没有，则继续找父类的父类  
        //提示：如果查找方法大的过程中，找到了但是不能访问，则报错  
        //     如果没找到，则提示不存在  
        cal();  
  
        //this代表当前，与不带this等价  
        this.cal();  
  
        //没有查找本类的过程，直接进行父类查找  
        super.cal();  
    }  
  
    //当问父类的方法，但不饿能访问父类的私有方法  
    public void ok(){  
        super.test100();  
        super.test200();  
        super.test300();  
        //super.test400(); 不能访问父类的私有方法  
    }  
  
    //访问父类的构造器:super(参数列表)；只能放在构造器的第一季，只能出现一句  
    public B(){  
        //super(); 无参  
        super("jack");  
    }  
}
```

`super01.java`

```
package com.cwz.super_;  
  
public class super01 {  
    public static void main(String[] args) {  
        B b = new B();  
        b.sum();  
    }  
}
```

1. super的访问不限于直接父类，如果爷爷类和本类中有同名的成员，也可以使用super去访问爷爷类的成员；如果多个基类中都有同名的成员，使用super访问遵循就近原则

- **super和this的比较**

|   |   |   |   |
|---|---|---|---|
|No.|区别点|this|super|
|1|访问属性|访问本类中的属性，如果本类没有此属性则从父类中继续查找|访问父类中的属性|
|2|调用方法|访问本类中的方法，如果本类没有此方法则从父类继续查找|直接访问父类中的方法|
|3|调用构造器|调用本类构造器，必须放在构造器的首行|调用父类构造器，必须放在子类构造器的首行|
|4|特殊|表示当前对象|子类中访问父类对象|

### 3.3.5 方法重写/方法覆盖

#### 3.3.5.1 基本介绍

方法覆盖(重写)子类有一个方法，和父类的某个方法的名称、返回类型、参数一样，那么我们就说子类的这个方法覆盖了父类的方法。

`Animal.java`

```
package com.cwz.override;  
  
public class Animal {  
    public void cry(){  
        System.out.println("动物叫唤..");  
    }  
}
```

`Dog.java`

```
package com.cwz.override;  
  
public class Dog {  
    //1.因为dog是animal的子类  
    //2.dog的cry方法和animal的cry定义形式一样(名称、返回类型、参数)  
    //3.这时我们就说dog的cry方法，重写了animal的cry方法  
    public void cry(){  
        System.out.println("小狗汪汪叫..");  
    }  
}
```

`override.java`

```
package com.cwz.override;  
  
public class override {  
    public static void main(String[] args) {  
        //演示方法重写的情况  
        Dog dog = new Dog();  
        dog.cry();  
    }  
}
```

#### 3.5.5.2 注意事项和细节

1. 子类方法的==参数，方法名称==，要和父类方法的参数，方法名称完全一样
2. 子类方法的返回类型和父类方法返回类型一样，或者是父类返回类型的子类
3. 子类方法不能缩小父类方法的访问权限

## 3.4 多态

### 3.4.1 基本介绍

方法或对象具有多种形态。

### 3.4.2 多态的具体体现

1. 方法的多态：重写和重载就体现多态
2. 对象的多态(核心)：

- 一个对象的编译类型和运行类型可以不一致
- 编译类型在定义对象时，就确定了，不能改变
- 运行类型是可以变化的
- 编译类型看定义时 = 号，运行类型看 = 号的右边  
    Animal animal = new Dog();【animal编译类型是Animal，运行类型是Dog】  
    animal = new Cat();【animal的运行类型变成了Cat，编译类型仍然是Animal】

`Animal.java`

```
package com.cwz.poly;  
  
public class Animal {  
    public void  cry(){  
        System.out.println("Animal cry() 动物在叫...");  
    }  
}
```

`Dog.java`

```
package com.cwz.poly;  
  
public class Dog extends Animal{  
    public void cry(){  
        System.out.println("Dog cry() 小狗汪汪叫");  
    }  
}
```

`Cat.java`

```
package com.cwz.poly;  
  
public class Cat extends Animal{  
  
    public void cry(){  
        System.out.println("Cat cry() 小猫喵喵叫");  
    }  
}
```

`Polyobject.java`

```
package com.cwz.poly;  
  
import jdk.internal.org.objectweb.asm.tree.analysis.Analyzer;  
  
public class PolyObject {  
    public static void main(String[] args) {  
        //体现对象多态的特点  
  
        Animal animal = new Dog();  
        animal.cry(); //因为运行时，这时就执行到该行时，animal运行类型是Dog,所有这个cry就是Dog的cry  
  
        //animal 编译类型 Animal，运行类型就是 Cat        
        animal = new Cat();  
        animal.cry(); //小猫喵喵叫  
  
    }  
}
```

运行图：

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712024267911-5b4325f6-9e1d-477a-9191-1123ea3d505f.png)

### 3.4.3 多态注意事项和细节讨论

- 多态的向上转型

1. 本质：父类的引用指向了子类的对象
2. 语法：父类类型 引用名 = new 子类类型();
3. 特点：编译类型看左边，运行类型看右边。  
    可以调用父类中的所有成员(需遵循访问权限)  
    不能调用子类中特有成员  
    最终运行成果看子类的具体呈现

`Animal.java`

```
package com.cwz.poly.detail;  
  
public class Animal {  
    String name = "动物";  
    int age = 10;  
    public void sleep(){  
        System.out.println("睡");  
    }  
    public void run(){  
        System.out.println("跑");  
    }  
    public void eat(){  
        System.out.println("吃");  
    }  
    public void show(){  
        System.out.println("hello,你好");  
    }  
}
```

`Cat.java`

```
package com.cwz.poly.detail;  
  
public class Cat extends Animal{  
    public void eat(){//方法重写  
        System.out.println("猫吃鱼");  
    }  
    public void catchMouse(){//Cat特有的方法  
        System.out.println("猫抓老鼠");  
    }  
}
```

`Polydetail.java`

```
package com.cwz.poly.detail;  
  
public class Polydetail {  
    public static void main(String[] args) {  
  
        //向上转型：父类的引用指向了子类的对象  
        //语法：父类类型引用名 = new 子类类型();  
        Animal animal = new Cat();  
        Object boj = new Cat();//可以运行，Object也是Cat的父类  
  
        //可以调用父类所有成员(需遵守访问权限)  
        //但是不能调用子类的特有成员  
        //因为在编译阶段，能调用那些成员，是由编译类型来决定的  
        //animal.catchMouse()错误  
        //最终运行效果看子类的具体实现  
        //最终运行效果看子类的具体实现，即调用方法时，按照从子类开始查找方法  
        animal.eat();//猫吃鱼  
        animal.run();  
        animal.show();  
        animal.sleep();  
    }  
}
```

## 3.5 多态的向下转型

1. 语法：子类类型   引用名 = (子类类型) 父类引用
2. 只能强转父类的引用，不能强转父类的对象
3. 要求父类的引用必须指向的是当前目标类型的对象
4. 当向下转型后可以调用子类类型中所有的成员

```
//老师希望，可以调用Cat的 catchMouse方法  
//多态的向下转型  
//语法：子类类型 引用名 = (子类类型) 父类引用  
//编译类型Cat 运行类型 Cat
Cat cat = (Cat) animal;  
cat.catchMouse();  
  
//要求父类的引用必须指向的是当前目标类型的对象  
//Dog dog = (Dog) animal; 不可以
```

### 3.5.1 多态的注意事项和细节

- 属性没有重写之说！属性的值看编译类型
- instanceof比较操作符，用于判断对象的==运行==类型是否为xx类型或xx类型的子类型

```
package com.cwz.poly.PolyDetail;  
  
public class PolyDetail {  
    public static void main(String[] args) {  
        BB bb = new BB();  
        System.out.println(bb instanceof BB); //true  
        System.out.println(bb instanceof AA); //true  
  
        //aa编译类型 AA， 运行类型是BB  
        AA aa = new BB();  
        System.out.println(aa instanceof AA);  
        System.out.println(aa instanceof BB);  
        Object boj = new Object();   
        String str = "Hello";  
        System.out.println(str instanceof Object);  
  
    }  
}  
  
class AA{} //父类  
class BB extends AA{} //子类
```

### 3.5.2 java的动态绑定机制(非常非常重要)

- 当调用对象方法的时候，该方法会和该对象的内存地址/运行类型绑定
- 当调用对象属性时，没有动态绑定机制，哪里声明，哪里使用

### 3.5.3 多态的应用

1. 多态数组  
    数组的定义类型为父类类型，里面保存到的实际元素类型为子类类型

应用实例：现有一个继承结构如下：要求创建一个Person对象，2个Student对象和2个Teacher对象，统一放在数组中，并调用say方法

应用实例升级：如何调用子类特有的方法，比如Teacher有一个teach，Student有一个study怎么调用

`Person.java`

```
package com.cwz.poly.polyarr;  
  
public class Person {//父类  
    private  String name;  
    private int age;  
  
    public Person(String name, int age) {  
        this.name = name;  
        this.age = age;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public int getAge() {  
        return age;  
    }  
  
    public void setAge(int age) {  
        this.age = age;  
    }  
  
    public String say(){//返回年龄名字  
        return name + "\t" + age;  
    }  
}
```

`Student.java`

```
package com.cwz.poly.polyarr;  
  
public class Student extends Person{  
    // 如果没有指明是什么类型，默认使用private类型  
    private double score;  
  
    public Student(String name, int age, double score) {  
        super(name, age);  
        this.score = score;  
    }  
  
    public double getScore() {  
        return score;  
    }  
  
    public void setScore(double score) {  
        this.score = score;  
    }  
  
    //重写父类的say()方法  
  
    @Override  
    public String say() {  
        return super.say() + " score=" + score;  
    }  
  
    //特有方法  
    public void study(){  
        System.out.println("学生" + getName() + "正在学java课程");  
    }  
}
```

`Teacher.java`

```
package com.cwz.poly.polyarr;  
  
public class Teacher extends Person{  
    private double salary;  
  
    public double getSalary() {  
        return salary;  
    }  
  
    public void setSalary(double salary) {  
        this.salary = salary;  
    }  
  
    public Teacher(String name, int age, double salary) {  
        super(name, age);  
        this.salary = salary;  
    }  
    //重写父类的say方法  
  
    @Override  
    public String say() {  
        return super.say() + " salary=" + salary;  
    }  
  
    //特有方法  
    public void teach(){  
        System.out.println("老师" + getName() + "正在讲java课程");  
    }  
  
  
}
```

`Polyarr.java`

```
package com.cwz.poly.polyarr;  
  
public class PolyArray {  
    public static void main(String[] args) {  
        //应用实例：现有一个继承结构如下：要求创建一个Person对象，2个Student对象和2个Teacher对象，统一放在数组中，并调用say方法  
  
        Person[] person = new Person[5];  
        person[0] = new Person("jack", 20);  
        person[1] = new Student("marry", 18, 100);  
        person[2] = new Student("smith", 18, 30);  
        person[3] = new Teacher("scott", 30, 20000);  
        person[4] = new Teacher("king", 50, 25000);  
  
        //循环遍历多态数组，调用say  
        for (int i = 0; i < person.length; i++) {  
            //Person[i] 编译类型是Person 运行类型是其对应的类型  
            System.out.println(person[i].say()); //动态绑定机制  
  
            if (person[i] instanceof Student) {//判断person[i] 的运行类型是不是Student  
                Student student = (Student)person[i];  
                student.study();  
                //((Student) person[i]).study();//向下转型  
  
            }else if(person[i] instanceof Teacher){  
                ((Teacher)person[i]).teach();  
            }else if(person[i] instanceof Person){  
            }else {  
                System.out.println("你的类型有误，请检查");  
            }  
        }  
    }  
}
```

2.多态参数

- 方法定义的形参为父类类型，实参类型允许为子类型

(1)定义员工类Employee，包含姓名和月工资[private],以及计算年工资getAnnual的方法。普通员工和经理继承了员工，经理类多了奖金bonus属性和管理manage方法，普通员工多了work方法，普通员工和经理类分别重写getAnnual方法

(2)测试类中添加一个方法showEmpAnnual(Employee e),实现获取任何员工对象的年工资，并咋main方法中调用该方法(e.getAnnual)

(3)测试类中添加一个方法，testWork，如果是普通员工，则调用work方法，如果是经理，则调用manage方法

`Employee.java`

```
package com.cwz.poly.paramaster;  
  
public class Employee {  
    private String name;  
    private double salary;  
  
    public Employee(String name, double salary) {  
        this.name = name;  
        this.salary = salary;  
    }  
    //得到年工资的方法  
    public double getAnnual(){  
        return 12 * salary;  
    }  
  
  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public double getSalary() {  
        return salary;  
    }  
  
    public void setSalary(double salary) {  
        this.salary = salary;  
    }  
}
```

`Manager.java`

```
package com.cwz.poly.paramaster;  
  
public class Manager extends  Employee{  
  
    private double bonus;  
  
    public Manager(String name, double salary, double bonus) {  
        super(name, salary);  
        this.bonus = bonus;  
    }  
  
    public double getBonus() {  
        return bonus;  
    }  
  
    public void setBonus(double bonus) {  
        this.bonus = bonus;  
    }  
  
    public void manage(){  
        System.out.println("经理 " + getName() + " is managing");  
    }  
  
    @Override  
    public double getAnnual() {  
        return super.getAnnual() + bonus;  
    }  
}
```

`worker.java`

```
package com.cwz.poly.paramaster;  
  
public class worker extends Employee{  
    public worker(String name, double salary) {  
        super(name, salary);  
    }  
    public void work(){  
        System.out.println("普通员工 "+ getName() + " is working");  
    }  
  
    @Override  
    public double getAnnual() {//因为普通员工没有其他收入，所有不做出改变  
        return super.getAnnual();  
    }  
}
```

Polyparameter.java`

```
package com.cwz.poly.paramaster;  
  
import javafx.concurrent.Worker;  
  
public class Polyparameter {  
    public static void main(String[] args) {  
        worker tom = new worker("tom", 2500);  
        Manager milan = new Manager("milan", 5000, 200000);  
        Polyparameter polyparameter = new Polyparameter();  
        polyparameter.showEmpAnnual(tom);  
        polyparameter.showEmpAnnual(milan);  
  
        polyparameter.testWork(tom);  
        polyparameter.testWork(milan);  
    }  
  
    //showEmpAnnual(Employee e)  
    //实现获取任何员工对象的年工资，并在main方法中调用该方法  
    public void showEmpAnnual(Employee e){  
        System.out.println(e.getAnnual());  
    }  
  
    //添加一个方法，testWork,如果是普通员工，则调用work方法，如果是经理，则调用manage方法  
    public void testWork(Employee e) {  
        if (e instanceof worker){  
            ((worker) e).work();//有一个向下转型操作  
        }else if(e instanceof  Manager){  
            ((Manager) e).manage();  
        }else{  
            System.out.println("不做处理");  
        }  
  
    }  
}
```

## 3.6 Object类详解

### 3.6.1 equals方法

- equals：是Object类中的方法，只能判断引用类型
- 默认判断的是地址是否相等，子类中往往重写该方法，用于判断内容是否相等

**Object的equals方法是判断两个地址是否相等**  
**String类(例子)的equals方法就是将Object的equals方法重写了，变成了比较两个字符串的值是否相等**

### 3.6.2 hashCode

1. 提高具有哈希结构的容器的效率
2. 两个引用，如果指向的是同一个对象，则哈希值肯定是不一样的
3. 两个引用，如果指向的不是对象，则哈希值是不一样的
4. 哈希值注意根据地址号来的，不能完全将哈希值等价于地址
5. 后面在集合中哈市Code如果需要的话，也会重写

```
package com.cwz.HashCode;  
  
public class HashCode {  
    public static void main(String[] args) {  
  
        AA aa = new AA();  
        AA aa2 = new AA();  
        //两个引用，如果指向的是不同对象，则哈希值是不一样的  
        System.out.println("aa.hashCode()= " + aa.hashCode());  
        System.out.println("aa2.hashCode()= " + aa.hashCode());  
        AA aa3 = aa;  
        //两个引用，如果指向的是同一对象，则哈希值肯定是一样的  
        System.out.println("aa.hashCode()= " + aa.hashCode());  
    }  
}  
  
class AA{}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712024292934-94c6b2e1-6ea3-4427-80e5-eb135f17f364.png)

### 3.6.3 toString方法

#### 3.6.3.1 基本介绍

默认返回：全类名(包名+类名）+@+哈希值的十六进制，【查看Object的toString方法】  
子类往往重写toString方法，用于返回对象的属性信息

```
package com.cwz.Object;  
  
public class ToString {  
    public static void main(String[] args) {  
        /*  
        Object的toString() 源码  
        (1)getClass().getName() 类的全类名(包名+类名）  
        (2)Integer.toHexString(hashCode()) 将对象的hashCode值转成16进制字符串  
        
        public String toString() {            
        return getClass().getName() + "@" + Integer.toHexString(hashCode());                                  
        }
        */        
	}  
}
```

- 重写toString方法，打印对象或拼接对象时，都会自动调用该对象的toString形式(输出属性信息)
- 当直接输出一个对象时，toString方法会被默认的调用

```
package com.cwz.Object;  
  
public class ToString {  
    public static void main(String[] args) {  
        /*  
        Object的toString() 源码  
        (1)getClass().getName() 类的全类名(包名+类名）  
        (2)Integer.toHexString(hashCode()) 将对象的hashCode值转成16进制字符串  
        public String toString() {            
	        return getClass().getName() + "@" + Integer.toHexString(hashCode());                
	     }
		 */  
        Monster monster = new Monster("小妖怪", "巡山的", 1000);  
		System.out.println(monster.toString() + 
		" hashcode= " + monster.hashCode());  

		System.out.println("==当直接输出一个对象时，toString方法会被默认地调用");  
		System.out.println(monster); //等价 monster.toString()
    }  
}  
class Monster{  
    private String name;  
    private String job;  
    private double sal;  
  
    public Monster(String name, String job, double sal) {  
        this.name = name;  
        this.job = job;  
        this.sal = sal;  
    }  
  
    //重写toString方法，输出对象的属性  
    //使用快捷键即可生成 alt + insert -> toString  
    @Override  
    public String toString() { //默认：重写后，一般是把对象的属性值输出，当然也可以自己设定  
        return "Monster{" +  
                "name='" + name + '\'' +  
                ", job='" + job + '\'' +  
                ", sal=" + sal +  
                '}';  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712024410450-d0df6875-4e94-4306-8d25-c1ec299cad07.png)

### 3.6.4 finalize方法

1. 当对象被回收时，系统自动调用该对象的finalize方法。子类可以重写该类方法，做一些释放资源的操作
2. 什么时候被回收：当某个对象没有任何引用时，则jvm就认为这个对象是一个垃圾对象，就会使用垃圾回收机制来销毁对象，在销毁该对象前，会先调用finalize方法
3. 垃圾回收机制的调用，是由系统来决定的，也可以通过System.gc()主动出发垃圾回收机制)

==我们在实际开发中，几乎不会运用finalize==

## 3.7 断点调试

### 3.7.1 基础介绍

- ==在断点调试过程中，是运行状态，是以对象的运行类型来执行的==
- 断点调试是指在程序的某一行设置一个断点，调试时，程序运行到这一行会停住，然后你可以一步一步往下调，调试过程中可以看到各个变量当前的值，出错的话，调试到出错误即现时错误，停下，进行分析从而找到bug

### 3.7.2 快捷键

|   |   |
|---|---|
|快捷键|功能|
|F7|跳入(跳入方法内)|
|F8|跳过(逐行执行代码)|
|shift+F8|跳出(跳出方法)|
|F9|resume，执行到下一个断点|

## 3.8 类变量和类方法

### 3.8.1 类变量

#### 3.8.1.1 解释

类变量也叫静态变量/静态属性，是该类的所有对象共享的变量，任何一个该类的对象去访问它时，取到的都是相同的值，同样任何一个该类的对象去修改它时，修改的也是同一个变量。

#### 3.8.1.2 定义类变量

**定义语法：**

- 访问修饰符 static 数据类型 变量名;【推荐使用】
- static 访问修饰符 数据类型 变量名;

#### 3.8.1.3 访问类变量

- 类名.类变量名【推荐使用】
- 对象名.类对象名[静态变量的访问修饰fu符的访问权限和范围和普通属性是一样的]

#### 3.8.1.4 类变量使用注意事项和细节讨论

- 什么时候需要用类变量  
    当我们需要让某个类的所有对象都共享一个变量时，就可以考虑使用类变量(静态变量)：  
    比如:定义学生类，统计所有学生共交多少钱。  
    Student(name,fee)
- 类变量与实例变量(普通属性)区别  
    类变量是该类的所有对象共享的，而实例变量是每个对象独享的
- 加上static成为类变量或静态变量，否则称实例变量/普通变量/非静态变量
- 类变量我们可以通过 类名.类变量名 或者 对象名.类变量名来访问，但java设计者推荐使用类名.类变量名的方式访问【前提：满足访问修饰符的权限】

```
package com.cwz.static_;  
  
public class VisitStatic {  
  
    public static void main(String[] args) {  
  
        //类名.类变量名  
        //说明：类变量是随着类的加载二创建，所以即使没有创建对象实例也可以访问  
        System.out.println(A.name);  
        A a = new A();  
        //通过对象名.类对象名  
        System.out.println("a.name：" + a.name);  

    }  
}  
  
class A{  
    //类变量  
    //类变量的访问，必须遵守相关的访问权限  
    public static String name = "韩顺平教育";  
    //普通属性/普通成员变量/非静态属性/非静态成员变量/实例变量  
    private  int num = 10;  
  
}
```

- 实例变量不能通过 类名.类变量名 方式访问
- 类变量在加载时就初始化了，也就是说，即使你没有创建对象，只要类加载了，就可以使用类变量
- 类变量的生命周期是随类的加载开始，随类消亡而销毁的

```
package com.cwz.static_;  
  
public class StaticDetail {  
  
    public static void main(String[] args) {  
        B b = new B();  
        //System.out.println(B.n1);  
        System.out.println(B.n2);  
  
        //静态变量时类加载的时候，就创建了，所以我们没有创建对象实例  
        //也可以通过类名.类变量名来访问  
        System.out.println(C.address);  
            }  
}  
  
class B{  
    public int n1 = 100;  
    public static int n2 = 100;  
}  
  
class C{  
    public static String address = "北京";  
}
```

### 3.8.2 类方法

#### 3.8.2.1 解释

类方法也叫静态方法  
形式如下：

- 访问修饰符 static 数据返回类型 方法名（）{ } 【推荐】
- static 访问修饰符 数据返回类型 方法名（）{ }

#### 3.8.2.2 类方法的调用

使用方式：类名.类方法名 或者 对象名.类方法名【前提时满足访问修饰符的访问权限和范围】

```
package com.cwz.static_;  
  
public class StaticMethod {  
    public static void main(String[] args) {  
  
        //创建两个学生对象  
        Stu tom = new Stu("Tom");  
        tom.payFee(100);  
        Stu.payFee(100);  
  
        Stu marry = new Stu("marry");  
        marry.payFee(200);  
  
        //输出当前收到的总学费  
        Stu.showFee();  
    }  
}  
  
class Stu{  
    private String name;//普通成员  
    //定义一个静态变量，来类继学生的学费  
    private static double fee = 0;  
  
    public Stu(String name) {  
        this.name = name;  
    }  
  
    //说明  
    //1.当方法使用static修饰后，该方法就是静态方法  
    //2，静态方法就可以访问静态属性/变量  
    public static void payFee(double fee){  
        Stu.fee += fee;//累计到  
    }  
    public static void showFee(){  
        System.out.println("总学费有：" + Stu.fee);  
    }  
}
```

#### 3.8.2.3 类方法使用注意事项和细节讨论

- 类方法和普通方法都是随着类的加载而加载，将结构信息存储在方法区：

- 类方法中无this的参数
- 普通方法中隐含着this的参数

- 类方法可以通过类名调用，也可以通过对象名调用
- 普通方法和对象有关，需要通过对象名的调用，比如对象名.方法名（参数)，不能通过类名调用
- 类方法中不允许使用和对象有关的关键字，比如this和super，普通方法(成员方法)可以
- 类方法(静态方法)中，只能访问 静态变量 或静态方法，也可以访问静态变量(方法)
- 普通成员方法，既可访问非静态成员也可以访问静态成员

小结：==静态方法只能访问静态的成员==，非静态的方法，可以访问静态成员和非静态成员(必须遵守访问权限)

### 3.8.3 类变量和类方法

#### 3.8.3.1 类方法的经典使用场景

- 当方法中不涉及到任何和对象相关的成员，则可以将方法设计成静态方法，提高开发效率

作用：不创建实例，也可以调用某个方法（即当作工具来使用）

比如：工具类中的方法 utils  
Math类、Arrays类、Collections集合类

小结：  
在程序员实际开发过程中，往往会将一些通用的方法，设计成静态成员方法，这样我们不需要创建对象就可以使用了，比如打印一维数组，冒泡排序，完成某个计算任务

```
class MyTools{
	//求两个数的和
	public static calSum(double n1, double n2){
		return n1 + n2;
	}
}
```

```
system.out.println(MyTools.calSum(10,30));
```

## 3.9 main方法语法

### 3.9.1 深入理解mwian方法

解释main方法的形式: public static void main(String[] args){}

1. main方法是java虚拟机调用的
2. java虚拟机需要调用main()方法，所有该方法的访问权限必须是public
3. java虚拟机在执行main()方法时不必创建对象所有该方法必须是static
4. 该方法接受String类型的数组参数，该数组中保存执行java命令时传递给所运行的类的参数
5. java 执行的程序 参数1 参数2 参数3

### 3.9.2 特别提醒

1. 在main()方法中，我们可以调用main方法所在类的静态方法或静态属性
2. 但是，不能直接去访问该类的非静态成员，必须创建该类的一个实例对象后，才能通过这个对象去访问类中的非静态成员

```
package com.cwz.main;  
  
public class Main01 {  
  
    //静态的变量/属性  
    private static String name = "educate";  
    //非静态的属性  
    private int n1 = 10000;  
  
    //静态方法  
    public static void hi() {  
        System.out.println("Main01的hi方法");  
    }  
    //非静态方法  
    public void cry(){  
        System.out.println("Main01的hi方法");  
    }  
  
    public static void main(String[] args) {  
  
        //可以直接使用name  
        //1.静态方法可以访问本类的静态成员  
        System.out.println("name=" + name);  
        hi();  
        //2.静态方法main，不可以访问本类的非静态成员  
        //System.out.println("n1=" + n1);//错误  
        //cry()//错误  
        //3.调用非静态成员需要先创建对象，再调用即可  
        Main01 main01 = new Main01();  
        System.out.println(main01.n1);  
        main01.cry();  
    }  
}
```

## 3.10 代码块

### 3.10.1 基本介绍

代码块又称为初始化块，属于类中的成员【即 是类的一部分，类似于方法，将逻辑语句封装在方法体中，通过{}包围起来】  
但和方法不同，没有方法名，没有返回，没有参数，只有方法体，而且不用通过对象或类显示调用，而是加载类，或创建对象时隐式调用

### 3.10.2 基本语法

[修饰符]{  
代码  
};

注意：

1. 修饰符可选，要写的话也只能写static
2. 代码块分为两类，使用static修饰的叫静态代码块，没有static修饰的，叫普通代码块
3. 逻辑语句可以为任何逻辑语句(输入、输出、方法调用、循环、判断等)
4. ；号可以写上，也可以省略

### 3.10.3 代码块的好处

1. 相当于另外一种形式的构造器(对构造器的补充机制)，可以做到初始化的操作
2. 如果多个构造器中有重复的语句，可以抽取到初始化块中，提高代码的重要性

```
package com.cwz.codeblock;  
  
public class CodeBlock01 {  
    public static void main(String[] args) {  
  
        new Movie("你好，李焕英");  
    }  
}  
  
class Movie{  
    private String name;  
    private double price;  
    private String director;  
  
    //3个构造器->重载  
    //(1)下面三个构造器有相同的语句  
    //(2)代码看起来比较多余  
    //(3)我们可以把相同的语句，放到一个代码块中，即可  
    //(4)这样不管我们调用那个构造器，创建对象，都会先调用代码块的内容  
    //(5)代码块调用的顺序优先于构造器  
    {  
        System.out.println("电影屏幕打卡");  
        System.out.println("电影正式开始");  
    };  
  
    public Movie(String name) {  
//        System.out.println("电影屏幕打卡");  
//        System.out.println("电影正式开始");  
        this.name = name;  
    }  
  
    public Movie(String name, double price) {  
//        System.out.println("电影屏幕打卡");  
//        System.out.println("电影正式开始");  
        this.name = name;  
        this.price = price;  
    }  
  
    public Movie(String name, double price, String director) {  
//        System.out.println("电影屏幕打卡");  
//        System.out.println("电影正式开始");  
        this.name = name;  
        this.price = price;  
        this.director = director;  
    }  
}
```

### 3.10.4 代码块使用注意事项和细节

1. static代码块也叫静态代码块，作用就是对类进行初始化，而且它随着类的加载而执行，并且指挥执行一次，如果时普通代码块，每创建一个对象，就执行
2. 类什么时候被加载

- 创建对象实例时(new)
- 创建子类对象实例，父类也会被加载
- 使用类的静态成员时(静态属性，静态方法)

3. 普通的代码块，在创建对象实例时，会被隐藏的调用。  
    被创建一次，就会调用一次  
    如果只是使用类的静态成员时，普通代码块不会执行
4. 创建一个对象时，在一个类的调用顺序：

- 调用静态代码块和静态属性初始化(注意：静态代码块和静态属性初始化调用的优先级一样，如果多个静态代码块和多个静态变量初始化，则按他们定义的顺序调用)
- 调用普通代码块和普通属性的初始化(注意：普通代码块和普通属性初始化用的优先级一样，如果有多个普通代码块和多个普通属性初始化，则按定义顺序调用)
- 调用构造方法

5. 构造方法(构造器)的最前面其实隐含了super()和调用普通代码块，新写一个类演示，静态相关的代码块，属性初始化，在类加载时，就执行完毕，因此时优先于构造器和普通代码块执行的

```
class A{
	public A(){//构造器
	//(1)super();//这个知识点-继承
	//(2)调用普通代码块的
	System.out.println("");
	}
}
```

```
package com.cwz.codeblock;  
  
public class CodeBlockDetail03 {  
  
    public static void main(String[] args) {  
        BBB bbb = new BBB();  
  
    }  
}  
  
class AAA{//父类Object  
  
    public AAA() {  
        //super();  
        System.out.println("AAA() 构造器被调用...");  
    }  
}  
  
class BBB extends AAA{  
    //(1)super();  
    //(2)调用本类的普通代码块  
    {  
        System.out.println("BBB的普通代码块");  
    }  
  
    public BBB() {  
        System.out.println("BBB() 构造器被调用");  
    }  
}
```

!![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712024587337-cd93a145-0303-4157-99ef-39751777e39b.png)

6. 创建一个子类时(继承关系)，他们的静态代码块，静态属性初始化，普通代码块，普通属性初始化，构造方法额调用顺序

- 父类的静态代码块和静态属性(优先级一样，按定义顺序执行)
- 子类的静态代码块和静态属性(优先级一样，按定义顺序执行)
- 父类的普通代码块和普通属性初始化(优先级一样，按定义顺序执行)
- 父类的构造方法
- 子类的普通代码块和普通属性初始化(优先级一样，按定义顺序执行)
- 子类的构造方法

7. 静态代码块只能直接调用静态成员(静态属性和静态方法)，普通代码块可以调用任意成员

## 3.11 单设计模式

### 3.11.1 概念

单例(单个的实例)

- 所谓类的单例设计模式，就是采取一定的方法保证在整个的软件系统中，对某个类只能存在一个对象实例，并且该类只提供一个取得其对象实例的方法  
    ->在软件运行保证只有一个类运行
- 单例模式有两种方法：

- 饿汉式
- 懒汉式

### 3.11.2 单例模式应用实践

#### 3.11.2.1 步骤

- 构造器私有化 -> 防止直接new
- 类的内部创建对象
- 向外暴露一个静态的公共方法 ->getInstance

#### 3.11.2.2饿汉式

类还未加载对象就创建(还没有用到该对象就已经创建好了)

```
package com.cwz.single;  
  
public class SingelTon01 {  
    public static void main(String[] args) {  
  
        //通过方法获取对象  
        GirlFriend instance = GirlFriend.getInstance();  
        System.out.println(instance);  
    }  
}  
  
//有一个类，GirlFriend  
//只能有一个女朋友  
class GirlFriend{  
  
    private String name;  
  
    //为了能够在静态方法中，返回gf对象，需要将其修饰为static  
    private static GirlFriend gf = new GirlFriend("小红");  
    //如何保障我们只能创建一个girlfriend对象  
    //1.将构造器私有化  
    //2.在类的内部直接创建  
    //3.提供一个公共的static方法，返回gf对象  
    private GirlFriend(String name) {  
        this.name = name;  
    }  
  
    public static GirlFriend getInstance(){  
        return gf;  
    }  
  
    @Override  
    public String toString() {  
        return "GirlFriend{" +  
                "name='" + name + '\'' +  
                '}';  
    }  
}
```

#### 3.11.2.3 懒汉式

只有当用户使用方法时，才会返回cat对象，后面再次调用时，再次返回上次创建的对象

```
package com.cwz.single;  
  
/**  
 * 演示懒汉式的单例模式  
 */  
public class SingelTon02 {  
    public static void main(String[] args) {  
        Cat instance = Cat.getInstance();  
        System.out.println(instance);  
  
    }  
}  
  
//希望在程序运行过程中，只能创建一个Cat对象  
class Cat {  
    private String name;  
    private static Cat cat;//默认是null  
    //步骤  
    //1.构造器私有化  
    //2.定义一个static属性对象  
    //3.提供一个public的static方法，可以返回一个Cat对象  
    private Cat(String name) {  
        this.name = name;  
    }  
  
    public static Cat getInstance(){  
  
        if(cat == null){ //如果还没有创建cat对象  
            cat = new Cat("小可爱");  
        }  
        return  cat;  
    }  
  
    @Override  
    public String toString() {  
        return "Cat{" +  
                "name='" + name + '\'' +  
                '}';  
    }  
}
```

#### 3.11.2.4饿汉式VS懒汉式

1. 二者最主要的区别在于创建对象的==时机==不同：饿汉式是在类加载就创建了对象实例，而懒汉式是在使用时才创建
2. 饿汉式不存在线程安全问题，懒汉式存在线程安全问题
3. 饿汉式存在浪费资源的可能。因为如果程序员一个对象实例都没有使用，那么饿汉式常见的对象就浪费了，懒汉式是使用时才创建，就不存在这个问题

## 3.12 final关键字

### 3.12.1 基本介绍

final可以修饰类、属性、方法和局部变量

1. 当不希望类被继承时，可以用final修饰
2. 当不希望父类的某个方法被子类覆盖/重写(override)时，可以用final关键字修饰
3. 当不希望类的某个属性的值被修改，可以用final修饰
4. 当不希望某个局部变量被修改，可以用final修饰

```
package com.cwz.final__;  
  
import sun.awt.geom.Crossings;  
  
public class final_ {  
  
    public static void main(String[] args) {  
        E e = new E();  
        //e.TAX_RATE = 0.1;  
    }  
}  
  
//如果要求A类不能被其他类继承  
//可以用final修饰A类  
final class A{ }  
  
//class B extends A{ } 该代码会报错  
  
class C{  
    //如果我们要求hi不能被子类重写  
    //可以使用final修饰 hi方法  
    public final void hi(){ }  
}  
  
/*  
class D extends C {  
    @Override    public void hi() {        System.out.println("重写了C类的hi方法");  
    }}  
*/  
  
//当不希望类的某个值被修改，可以使用final修饰  
class E{  
    public final double TAX_RATE = 0.08;  
}  
  
//当不希望局部变量被修改，可以使用final修饰  
class F{  
    public void cry() {  
        //这时，NUM也成为局部常量  
        final double NUM = 0.01;  
        //NUM = 0.9;  
        System.out.println("NUM" + NUM);  
    }  
}
```

### 3.12.2 final使用注意事项和细节讨论

1. final修饰的属性又叫常量，一般用XX_XX_XX来命名
2. final修饰的属性在定义时，必须赋初值，并且以后不能再修改，赋值可以在如下位置之一【选择一个位置赋初值即可】:

- 定义时：如 public final double TAX_RATE = 0.08;
- 在构造器中
- 在代码块中

3. 如果final修饰的属性是静态的，则初始化的位置只能是

- 定义时
- 在静态代码块 不能在构造器中赋值

4. final类不能继承，但可以实例化对象
5. 如果类不是final类，但是含有final方法，则该方法虽然不能重写，但是可以被继承
6. 一般来说，如果一个类已经是final类了，就没有必要再将方法修饰成final方法
7. final不能修饰构造方法(即构造器)
8. final和static往往搭配使用，效率更高，不会导致类的加载，底层编译器做了优化处理
9. 包装类(Integer，Double，Float，Boolean都是final)，String也是final类

## 3.13 抽象类

### 3.13.1 基本介绍

当父类的某些方法，需要声明，但是不确定如何实现时，可以将其声明为抽象方法，那么这个类就是抽象类  
->父类方法不确定性

1. 用abstract关键字来修饰一个类，这个类就叫抽象类  
    访问修饰符 abstract 类名{}
2. 用abstract 关键字来修饰一个方法时，这个方法就是抽象方法  
    访问修饰符 abstract 返回类型 方法名(参数列表)；//没有方法体
3. 抽象类的价值更多在于设计，是设计者设计好后，让子类继承并实现抽象类

```
package com.cwz.abstract_;  
  
public class Abstract01 {  
  
    public static void main(String[] args) {  
  
    }}  
abstract class Animal{  
    private String name;  
  
    public Animal(String name) {  
        this.name = name;  
    }  
  
    //思考：这里eat 这里实现了，其实没什么意义  
    //即：父类方法不确定性的问题  
    //===> 考虑将该方法设计为抽象(abstract)方法  
    //===> 所谓抽象方法就是没有实现的方法  
    //===> 所谓没有实现就是指没有方法体  
    //===> 当一个类中存在抽象方法时，需要将该类声明为abstract类  
    //===> 一般来说，抽象类会被继承，有其子类来实现抽象方法  
//    public void eat(){  
//        System.out.println("这是一个动物，但是不知道吃什么");  
//    }  
    public abstract void  eat();  
}
```

### 3.13.2 抽象类使用的注意事项和细节讨论

1. 抽象类不能被实例化
2. 抽象类不一定要包含abstract方法。也就是说，抽象类可以没有abstract方法
3. 一旦类包含了abstract方法，则这个类必须声明为abstract
4. abstract只能修饰类和方法，不能修饰属性和其他的

```
package com.cwz.abstract_;  
  
public class AbstractDerail01 {  
  
    public static void main(String[] args) {  
        //抽象类不能被实例化  
        // new A();  
    }  
}  
  
//抽象类不一定要包含abstract方法。也就是说，抽象类可以没有abstract方法  
abstract class A{  
    }
```

5. 抽象类可以有任意成员【抽象类本质还是类】，比如：非抽象方法、构造器、静态属性等
6. 抽象方法不能有主体，即不能实现
7. 如果一个类继承了抽象类，则它必须实现抽象类中的所有抽象方法，除非它自己也声明为abstract类
8. 抽象方法不能使用private、final和static来修饰，因为这些关键字都是和重写相违背的

```
package com.cwz.abstract_;  
  
public class AbstractDerail02 {  
  
    public static void main(String[] args) {  
  
    }}  
//抽象类的本质还是类，所有可以有类的各种成员  
abstract class D{  
    public int n1 = 10;  
    public static String name = "老八";  
    public void hi(){  
        System.out.println("hi");  
    }  
    public abstract void hello();  
    public static void ok(){  
        System.out.println("ok");  
    }  
}  
  
abstract class E{  
    public abstract void hi();  
}  
  
class F extends E{  
    @Override  
    public void hi() {  
        //这里相等于E类实现了父类E的抽象方法，所谓实现方法，就是有方法体  
    }  
}
```

## 3.14 接口

### 3.14.1 快速入门

`接口：InterFace01.java`

```
package com.cwz.interface_;  
  
public interface UsbInterface { //接口  
    //规定接口的相关方法即规范  
    public void start();  
    public void stop();  
}
```

`Phone.java`

```
package com.cwz.interface_;  
  
//Phone 类 实现 UsbInterface//解读1.即 phone类需要实现 UsbInterface接口 规定/声明方法  
public class Phone implements UsbInterface{  
  
    @Override  
    public void start() {  
        System.out.println("手机开始工作...");  
    }  
  
    @Override  
    public void stop() {  
        System.out.println("手机停止工作...");  
    }  
}
```

`Camera.java`

```
package com.cwz.interface_;  
  
public class Camera implements UsbInterface{ //实现接口  
  
  
    @Override  
    public void start() {  
        System.out.println("相机开始工作了...");  
    }  
  
    @Override  
    public void stop() {  
        System.out.println("相机停止工作");  
    }  
}
```

`Computer.java`

```
package com.cwz.interface_;  
  
public class Computer {  
    //编写一个方法  
    public void work(UsbInterface usbInterface){  
        usbInterface.start();  
        usbInterface.stop();  
    }  
}
```

`InterFace01.java`

```
package com.cwz.interface_;  
  
public class InterFace01 {  
  
    public static void main(String[] args) {  
        //创建手机、相机对象  
        Camera camera = new Camera();  
        Phone phone = new Phone();  
        //创建计算机  
        Computer computer = new Computer();  
        computer.work(phone);//把手机接入到计算机  
        System.out.println("==========");  
  
        computer.work(camera);//把相机接入计算机  
  
    }  
}
```

### 3.14.2 基本介绍

接口就是给出一些没有实现的方法，封装到一起，到某个类要使用的时候，再根据具体情况把这些方法写出来

```
语法：
interface 接口名{
	//属性
	//方法(1.抽象方法 2.默认实现方法 3.静态方法)
}

class 类名 implements 接口{
	自己属性;
	自己方法;
	必须实现的接口的抽象方法
}
```

小结：

1. 在Jdk.7.0前 接口里的所以要方法都没有方法体，即都是抽象方法
2. Jdk8.0后接口类可以有静态方法，默认方法，也就是说接口中可以有方法的具体实现

`AInterFace.java`

```
package com.cwz.interface_.InterFace02;  
  
public interface AInterface {  
    //写属性  
    public int n1 = 10;  
    //写方法  
    //在接口中，抽象方法可以省略abstract抽象方法关键字  
    public void hi();  
    //在jdk8后，可以有默认实现方法，需要使用default关键字修饰  
    default public void ok(){  
        System.out.println("ok..");  
    }  
    //在jdk8后，可以有静态方法  
    public static void cry(){  
        System.out.println("cry...");  
    }  
}
```

`InterFace02.java`

```
package com.cwz.interface_.InterFace02;  
  
public class Interface02 {  
  
    public static void main(String[] args) {  
  
  
    }}  
  
//如果一个类 implements 实现接口  
//需要将该接口的所有抽象方法都实现  
class A implements AInterface{  
    @Override  
    public void hi() {  
        System.out.println("hi...");  
    }  
}
```

### 3.14.3 注意事项和细节

1. 接口不能被实例化
2. 接口中所有的方法是public方法，接口中抽象方法，可以不用abstract修饰
3. 一个普通类实现接口，就必须将该接口的所有方法都实现
4. 抽象类实现接口，可以不用实现接口的方法

```
package com.cwz.interface_.InterFaceDetail;  
  
public class InterFaceDetail {  
    public static void main(String[] args) {  
        //接口不能被实例化  
        //new IA()  
    }  
}  
  
  
interface IA{  
    //接口中所有的方法是public方法，接口中抽象方法，可以不用abstract修饰  
    void say();//修饰符 public    void hi();  
}  
  
class Cat implements IA{  
    //一个普通类实现接口，就必须将该接口的所有方法都实现，可以使用alt+enter来解决  
    @Override  
    public void say() {  
  
    }  
    @Override  
    public void hi() {  
  
    }}  
  
//抽象类去实现接口时，可以不实现接口的抽象方法  
abstract class Tiger implements IA{  
    }
```

5. 一个类同时可以实现多个接口
6. 接口中的属性，只能是final的，而且是public，static，final修饰符。比如:int a = 1;实际上是public static final int a = 1;（必须初始化)
7. 接口中属性的访问形式:接口名.属性
8. 一个接口不能继承其他类，但是可以继承多个别的接口
9. 接口的修饰符，只能是public和默认，这点和类的修饰符是一样的

```
package com.cwz.interface_.InterFaceDetail02;  
  
public class InterFaceDetail02 {  
    public static void main(String[] args) {  
        System.out.println(IB.n1);//静态属性的最根本的用法 -> n1为static  
    }  
}  
  
interface IB{  
    //接口中的属性，只能是final的，而且是public static final修饰符  
    int n1 = 10;//等价 public static final int n1 = 10;    void hi();  
}  
interface IC{  
    void say();  
}  
  
//一个类同时可以实现多个接口  
class Pig implements IB,IC{  
  
    @Override  
    public void hi() {  
  
    }  
    @Override  
    public void say() {  
  
    }}
```

### 3.14.4 实现接口 VS 继承类

小结：

- 当子类继承父类，就自动拥有父类的功能
- 如果子类需要扩展功能，可以通过实现接口的方式扩展  
    可以理解 实现接口 是对java单继承机制的一种补充

1. 接口和继承解决的问题不同  
    继承的价值主要在于:解决代码的复用性和可维护性  
    接口的价值主要在于：设计，设计好各种规范(方法),让其它类去实现这些方法
2. 接口比继承更加灵活  
    接口比继承更加灵活，继承是满足is-a的关系，而接口只需要满足like-a的关系
3. 接口在一定程序上实现代码解耦【即 接口的规范性+动态绑定】

```
package com.cwz.interface_.Extend_VS_Interface;  
  
public class Extend_VS_Interface {  
    public static void main(String[] args) {  
        LittleMoney wukong = new LittleMoney("悟空");  
        wukong.climbing();  
        wukong.swimming();  
        wukong.flying();  
  
    }  
}  
  
//猴子  
class Monkey{  
    private String name;  
  
    public Monkey(String name) {  
        this.name = name;  
    }  
  
    public void climbing(){  
        System.out.println(name + "会爬树...");  
    }  
  
    public String getName() {  
        return name;  
    }  
}  
  
//接口  
interface Fishable{  
    void swimming();  
}  
  
interface Birdable{  
    void flying();  
}  
  
  
//继承  
class LittleMoney extends Monkey implements Fishable,Birdable{  
    public LittleMoney(String name) {  
        super(name);  
    }  
  
    @Override  
    public void swimming() {  
        System.out.println(getName() + "通过学习，可以像小鱼一样游泳...");  
    }  
  
    @Override  
    public void flying() {  
        System.out.println(getName() + "通过学习，可以像鱼儿一样飞翔...");  
    }  
}
```

### 3.14.5 接口的多态特性

1. 多态参数  
    在前面的Usb接口案例 Usb usb，既可以接收手机对象，又可以接收相机对象，就体现了接口多态(接口引用可以指向实现了接口的类的对象)
2. 多态数组  
    给Usb数组中，存放Phone和相机对象，Phone类还有一个特有的方法call(),请遍历数组，如果Phone对象，除了调用Usb接口定义的方法外，还需要调用Phone特有方法call
3. 接口存在多态传递现象

```
public class InterfacePolyPass {
	public static void main(String[] args){
		//接口类型的变量可以指向，实现了该接口的类的对象实例
		IG ig = new Teacher();
		//如果 IG 继承了 IH 接口 而Teacher 类实现了 IG接口
		//相当于Teacher 类也实现了IH接口
		IH ih = new Teacher();
	}
}

interface IH {
	
}
interface IG extemnds {}
class Teacher implements IG {
	
}
```

## 3.15 内部类

### 3.15.1 基本介绍

一个类的内部又完整嵌套了另一个类结构。被嵌套的类成为内部类，嵌套其他的类称为外部类。是我们类的五大成员，内部类最大的特点就是可以直接访问私有属性，并且可以体现类鱼类之间的包含关系，注意：内部类是学习的难点也是重点

【思考：类的五大成员有哪些】  
属性、方法、构造器、代码块、内部类

```
基本语法：
class Outer{ //外部类
	class Inner{  //内部类
	
	}
}
class Other{  //外部其他类
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712024598118-96ff102c-70b0-48c5-861f-157be0d505aa.png)

```
package com.cwz.innerclass;  
  
public class InnerClass01 {//外部其他类  
    public static void main(String[] args) {  
            }  
}  
class Outer{//外部类  
    private int n1 = 100;//属性  
  
    public Outer(int n1) {//构造器  
        this.n1 = n1;  
    }  
  
    public void m1(){//方法  
        System.out.println("m1()");      
}  
    {        System.out.println("代码块...");  
    }  
    class Inner{//内部类，在Outer类内部  
        }  
}
```

### 3.15.2四种内部类

- 定义在外部类局部位置上(比如方法内)

- 局部内部类(有类名)
- 匿名内部类(没有类名，重点！！！)

- 定义在外部类的成员位置上

- 成员内部类(没有static修饰)
- 静态内部类(使用static修饰)

#### 3.15.2.1 局部内部类

说明：局部内部类是定义在外部类的局部位置，比如方法中，并且有类名

1. 可以直接访问外部类的所有成员，包含私有的
2. 不能添加访问修饰符，因为它的地位就是一个局部变量。局部变量不能使用修饰符的。但是可以使用final修饰，因为局部变量也可以使用final
3. 作用域：仅仅在定义它的方法和代码块中
4. 局部内部类---访问--->外部类的成员[访问方式：直接访问]
5. 外部类---访问---->局部内部类的成员
6. 访问方式:创建对象，再访问(注意：必须在作用域内)
7. 外部其他类---->不能访问----->局部内部类(因为 局部内部类地位是一个局部变量)
8. 如果外部类和局部内部类的成员重名时，默认遵循就近原则，如果想访问外部类的成员，则可以使用(外部类名.this.成员)去访问  
    System.out.println("外部类的n2=" + 外部类名.this.n2)  
    Outer02.this 本质就是外部类的对象，即那个对象调用了m1,Outer02.this就是哪个对象

记住：

- 局部内部类定义在方法中/代码块
- 作用域在方法体或者代码中
- 本质仍然是一个类

```
package com.cwz.innerclass;  
  
/**  
 * 演示局部内部类的使用  
 */  
public class LocalInnerClass {  
    public static void main(String[] args) {  
        //演示  
        Outer02 outer02 = new Outer02();  
        outer02.m1();  
    }  
}  
  
class Outer02{  
    private int n1 = 100;  
    private void m2(){  
        System.out.println("Outer02 m2()");  
    }//私有方法  
    public void m1(){//方法  
        //局部内部类是定义在外部类的局部位置，通常在方法  
        //不能添加访问修饰符,但是可以使用final修饰，因为局部变量也可以使用final  
        //作用域：仅仅在定义它的方法和代码块中  
        final class Inner02{//局部内部类(本质仍然是一个类)  
            //可以直接访问外部类的所有成员，包含私有的  
            public void f1(){  
                //局部内部类---访问--->外部类的成员[访问方式：直接访问]  
                System.out.println("n1=" + n1);  
                m2();  
            }  
        }  
  
        //class Inner03 extends Inner02{  
        //}  
        //外部类在方法中，可以创建Inner02对象，然后调用方法即可  
        Inner02 inner02 = new Inner02();  
        inner02.f1();  
    }  
}
```

#### 3.15.2.2匿名内部类

##### 3.15.2.2.1匿名内部类使用(重要)

(1)本质是类  
(2)内部类  
(3)该类没有名字

说明：匿名内部类是定义在外部类的局部位置，比如方法中，并且没有类名

```
匿名内部类的基本语法：
new 类或接口(参数列表){
		类体
};
```

**匿名内部类基于接口的演示**

```
package com.cwz.innerclass;  
  
/**  
 * 演示匿名内部类的使用  
 */  
public class AnonymousInnerClass {  
    public static void main(String[] args) {  
        Outer04 outer04 = new Outer04();  
        outer04.method();  
    }  
}  
class Outer04{ //外部类  
    private int n1 = 10;//属性  
    public void method(){//方法  
        //基于接口的匿名内部类  
        //1.需求：想使用接口IA接口，并创建对象  
        //2.传统方式，是写一个类，实现该接口，并创建对象  
//        Tiger tiger = new Tiger();  
//        tiger.cry();  
        //3.需求是Tiger 类只是使用一次，之后再不使用  
        //4.可以使用匿名内部类来简化  
        IA tiger = new IA(){  
            @Override  
            public void cry() {  
                System.out.println("老虎叫唤");  
            }  
        };  
        tiger.cry();  
        //5.tiger的编译类型是什么?IA  
        //6.tiger的运行类型是什么?就是匿名内部类 xxxx => Outer04$1        
        /*我们看底层  
            class XXXX implements IA{            
	            @Override            
	            public void cry() {                
		            System.out.println("小狗汪汪叫");  
	        }         
	        */        
	    //7.jdk底层再创建匿名内部类 Outer04$1，立即马上就创建了Outer04$1实例  
        //8.并且把地址返回给 tiger        
        //9.匿名内部类使用一次，就不能再使用了  

        //演示基于类的匿名内部类  
        //1.father编译类型Father  
        //2.father运行类型 Outer04$2        
        Father father = new Father("jack"){  
            //注意("jack")参数列表会传递给 构造器  
            @Override  
            public void test() {  
                System.out.println("匿名内部类重写了test方法");  
            }  
        };  
        System.out.println("father对象的运行类型=" + father.getClass());//Outer04&2  
  
        //基于抽象类的匿名内部类  
        Animal animal = new Animal(){  
            @Override  
            void eat() {  
                System.out.println("小狗吃骨头");  
            }  
        };  
        animal.eat();  
    }  
}  
interface IA{//接口  
    public void cry();  
}  
  
//class Dog implements IA{  
//    @Override  
//    public void cry() {  
//        System.out.println("小狗汪汪叫");  
//    }  
//}  
//  
//class Tiger implements IA{  
//    @Override  
//    public void cry() {  
//        System.out.println("老虎叫唤");  
//    }  
//}  
  
class Father{  
    public Father(String name){//构造器  
        System.out.println("name=" + name);  
    }  
    public void test(){  
    }}  
  
abstract class Animal{//抽象类  
    abstract void eat();  
}
```

#### 3.15.2.3匿名内部类细节

1. 可以直接访问外部类的所有成员,包含私有的
2. 不能添加访问修饰符，因为它的地位就是一个局部变量
3. 作用域：仅仅子啊定义它的方法和代码块中
4. 匿名内部类--->访问--->外部类成员【访问类型：直接访问】
5. 外部其他类--->不能访问--->匿名内部类(因为 匿名内部类地位是一个局部变量)
6. 如果外部类和内部类的成员重名时，匿名内部类访问的话，默认遵循就近原则，如果想访问外部类的成员，则可以使用(外部类名.this.成员)去访问

```
package com.cwz.innerclass;  
  
public class AnonymousInnerClassDetail {  
    public static void main(String[] args) {  
  
        Outer05 outer05 = new Outer05();  
        outer05.f1();  
  
    }  
}  
class Outer05{  
    private int n1 = 99;  
    public void f1(){  
        //创建一个基于类的匿名内部类  
        //不能添加访问修饰符，因为它的地位就是一个局部变量  
        //作用域：仅仅在定义它的方法或代码块中 只能使用一次  
        Person p = new Person(){  
            @Override  
            public void hi() {  
                //可以直接访问外部的所有成员，包含私有的  
                System.out.println("匿名内部类重写了hi方法 n1=" + n1) ;  
            }  
        };  
        p.hi();//动态绑定，真实运行类型是 Outer05  
        //也可以直接调用,匿名内部类本身也是返回对象  
        new Person(){  
            @Override  
            public void hi() {  
                System.out.println("hi,哈哈哈哈");  
            }  
        }.hi();  
    }  
}  
class Person{  
    public void hi(){  
        System.out.println("Person hi()");  
    }  
}  
//抽象类/方法...
```

#### 3.15.2.4 成员内部类

说明：成员内部类是定义在外部类的成员位置，并且没有static修饰

1. 可以直接访问外部类的所有成员，包含私有的
2. 可以添加任意访问修饰符(public、protected、默认、private)，因为它的地位就是一个成员

```
package com.cwz.innerclass;  
  
public class MemberInnerClass {  
    public static void main(String[] args) {  
        Outer08 outer08 = new Outer08();  
        outer08.t1();  
    }  
}  
  
class Outer08{ //外部类  
    private int n1 = 10;  
    public String name = "张三";  
    //注意成员内部类是定义在外部内的成员位置上  
    class Inner08{//成员内部类  
        public void say(){  
            //可以直接访问外部类的所有成员，包含私有的  
            System.out.println("n1= " + n1 + " name = " + name);  
        }  
    }  
  
    //写方法  
    public void t1(){  
        Inner08 inner08 = new Inner08();  
        inner08.say();  
    }  
}
```

3. 作用域和外部类的其他成员一样，为整个类体比如前面案例，在外部类的成员方法中创建内部类对象，再调用方法
4. 成员内部类--->访问--->外部类(比如：属性)[访问方式:直接访问]
5. 外部类--->访问--->成员内部类[访问方式:创建对象，再访问]
6. 外部其他类--->访问--->成员内部类
7. 如果外部类和内部类的成员重名时。内部类想访问的话，默认遵循就近原则，如果想访问外部类的成员，则可以使用(外部类.this.成员)去访问

```
package com.cwz.innerclass;  
  
public class MemberInnerClass {  
    public static void main(String[] args) {  
        Outer08 outer08 = new Outer08();  
        outer08.t1();  
        //外部其他类，使用成员内部类的三种方式  
        //outer08.new Inner08(); 相当于把Inner08()当作是outer08的成员  
        //这就是一个语法，不需要特别纠结  
        //第一种方式  
        Outer08.Inner08 inner08 = outer08.new Inner08();  
        inner08.say();  
        //第二种方式  
        Outer08.Inner08 inner08Instance = outer08.getInner08Instance();  
        inner08.say();  
        }  
}  
  
class Outer08{ //外部类  
    private int n1 = 10;  
    public String name = "张三";  
    private void hi(){  
        System.out.println("hi方法");  
    }  
    //注意成员内部类是定义在外部内的成员位置上  
    class Inner08{//成员内部类  
        private double sal = 99.8;  
        public void say(){  
            //可以直接访问外部类的所有成员，包含私有的  
            System.out.println("n1= " + n1 + " name = " + name);  
            hi();  
        }  
    }  
    //该方法返回Inner08的实例  
    public Inner08 getInner08Instance(){  
        return new Inner08();  
    }  
  
    //写方法  
    public void t1(){  
        //使用成员内部类  
        //创建成员内部类的对象，然后使用相关的方法  
        Inner08 inner08 = new Inner08();  
        inner08.say();  
        System.out.println(inner08.sal);  
    }  
}
```

### 3.15.3 静态内部类

说明：静态内部类是定义再外部类的成员位置上，并且有static修饰

1. 可以直接访问外部类的所有静态成员，包含私有的，但不能直接访问非静态成员
2. 可以添加任何访问修饰符(public、protected、默认、private)，因为它的地位就是一个成员
3. 作用域：同其他的成员，为整个类体
4. 静态内部类--->访问--->外部类(你如：静态属性)[访问方式:直接访问所有静态成员]
5. 外部类---访问--->静态内部类 访问方式:创建对象，再访问
6. 外部其他类--->访问--->静态内部类
7. 如果外部类和静态内部类的成员重名时，静态内部类访问时，默认遵循就近原则，如果想访问外部类的成员，则可以使用(外部类名.成员)去访问

```
package com.cwz.innerclass;  
  
public class StaticInnerClass {  
    public static void main(String[] args) {  
        Outer10 outer10 = new Outer10();  
        outer10.m1();  
  
        //外部其他类 使用静态内部类  
        //方式1  
        //因为静态内部类，是可以通过类名直接访问(前提是满足访问权限)  
        Outer10.Inner10 inner10 = new Outer10.Inner10();  
        inner10.say();  
        //方式2  
        //编写一个方法，可以返回静态内部类方法的实例  
        Outer10.Inner10 inner101 = outer10.getInner10();  
        System.out.println("==========");  
        inner101.say();  
  
        Outer10.Inner10 inner10_ = Outer10.getInner10_();  
        System.out.println("***********");  
        inner10_.say();  
    }  
}  
  
class Outer10{ //外部类  
    private int n1 = 10;  
    private static String name = "张三";  
    private static void cry(){}  
    //Inner10就是静态内部类  
    //1，放在外部类的成员位置  
    //2.使用static修饰  
    static class Inner10{  
        private static String name = "cwz";  
        public void say(){  
            //如果外部类和静态内部类的成员重名时，静态内部类访问时，默认遵循就近原则  
            //如果想访问外部类的成员，则可以使用(外部类名.成员)去访问  
            //3.可以访问所有外部的静态成员，包含私有的，但不能直接访问非静态成员  
            System.out.println(name);  
            System.out.println("外部类mame= " + Outer10.name);  
        }  
    }  
    public void m1(){  
        Inner10 inner10 = new Inner10();  
        inner10.say();  
    }  
  
    public Inner10 getInner10(){  
        return new Inner10();  
    }  
  
    public static Inner10 getInner10_(){  
        return new Inner10();  
    }  
}
```

### 小结

（1）内部类有四种：局部内部类  匿名内部类  成员内部类  静态内部类  
（2）重点还是掌握 匿名内部类使用  
new 类/接口(参数列表){  
//...  
};  
（3）成员内部类，静态内部类是是放在外部类的成员位置 本质就是一个成员

# 4. 房屋出租系统

`House.java`

```
package com.cwz.houserent.domain;  
  
/**  
 * House的对象表示一个房屋信息  
 */  
public class House {  
    //编号  房屋  电话  地址  月租  状态(未出租/已出租)  
    private int id;  
    private String name;  
    private String phone;  
    private String address;  
    private int rent;  
    private String state;  
    //构造器和setter，getter  
  
    public House(int id, String name, String phone, String address, int rent, String state) {  
        this.id = id;  
        this.name = name;  
        this.phone = phone;  
        this.address = address;  
        this.rent = rent;  
        this.state = state;  
    }  
  
    public int getId() {  
        return id;  
    }  
  
    public void setId(int id) {  
        this.id = id;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public String getPhone() {  
        return phone;  
    }  
  
    public void setPhone(String phone) {  
        this.phone = phone;  
    }  
  
    public String getAddress() {  
        return address;  
    }  
  
    public void setAddress(String address) {  
        this.address = address;  
    }  
  
    public int getRent() {  
        return rent;  
    }  
  
    public void setRent(int rent) {  
        this.rent = rent;  
    }  
  
    public String getState() {  
        return state;  
    }  
  
    public void setState(String state) {  
        this.state = state;  
    }  
    //为了方便输出对象信息，我们实现toString方法  
  
  
    @Override  
    public String toString() {  
        return   id +  
                "\t\t" + name +  
                "\t" + phone +  
                "\t\t" + address +  
                "\t" + rent +  
                "\t" + state ;  
    }  
}
```

`HouseService.java`

```
package com.cwz.houserent.service;  
  
import com.cwz.houserent.domain.House;  
  
/**  
 * HouseService.java<=>类[业务层]  
 * //定义House[],保存House对象  
 * 1.相应HouseView的调用  
 * 2.完成对房屋系统的各种操作(增删改查c[create]r[read]u[update]d[delete])  
 */public class HouseService {  
  
    private House[] houses;//保存House对象  
    private int housesNums = 1;//记录当前有多少个房屋信息  
    private int idCounter = 1;//记录当前的id的增长到哪个值  
    public HouseService(int size){  
        //new houses  
        houses = new House[size];//当创建HouseService对象，指定数组大小  
        //为配合测试列表信息，初始化一下这个house对象  
        houses[0] = new House(1,"jack","112","海淀区",2000,"未出租");  
    }  
  
    //find方法,返回house对象  
    public House findById(int findId){  
  
        //遍历数组  
        for (int i = 0; i < housesNums; i++) {  
            if(findId == houses[i].getId()){  
                return houses[i];  
            }  
        }  
  
        return null;  
    }  
  
  
    //del方法，删除一个房屋信息  
    public boolean del(int delID){  
        //应当先找到要删除的房屋信息对应的下标  
        //一定要搞清楚下标和房屋下标不是一回事  
        int index = -1;  
        for (int i = 0; i < housesNums; i++) {  
            if(delID == houses[i].getId()){//要删除的房屋(id)，在数组下标为i的元素  
                index = i;//使用index记录i  
            }  
        }  
  
        if(index == -1){//说明delID在数组中不存在  
            return false;  
        }  
        for (int i = 0; i < housesNums - 1; i++) {  
            houses[i] = houses[i+1];  
        }  
        houses[--housesNums] = null;//当前存在的房屋信息的最后一个设置null  
  
        return true;  
    }  
  
    //add方法，添加新对象，返回boolean  
    public boolean add(House newHouse){  
        //判断是否还可以继续添加(我们暂时不考虑数组扩容的问题  
        if(housesNums == houses.length){//不能添加了  
            System.out.println("数组已满，不能再添加了...");  
            return false;        }  
  
        //把newHouse对象加入到  
        houses[housesNums] = newHouse;  
        housesNums++;//新增加了一个房屋  
        //houses[houseNums++] = newHouse;  
        //我们程序员需要设计一个id自增长的机制,更新newHouse的id  
        idCounter++;  
        newHouse.setId(idCounter);  
        return true;    }  
  
    //list方法，返回houses  
    public House[] list(){  
        return houses;  
    }  
}
```

`Utility.java`

```
package com.cwz.houserent.Utility;  
  
/**  
   工具类的作用:  
   处理各种情况的用户输入，并且能够按照程序员的需求，得到用户的控制台输入。  
*/  
  
import java.util.*;  
/**  
  
   */  
public class Utility {  
   //静态属性。。。  
    private static Scanner scanner = new Scanner(System.in);  
  
    /**  
     * 功能：读取键盘输入的一个菜单选项，值：1——5的范围  
     * @return 1——5  
     */   public static char readMenuSelection() {  
        char c;  
        for (; ; ) {  
            String str = readKeyBoard(1, false);//包含一个字符的字符串  
            c = str.charAt(0);//将字符串转换成字符char类型  
            if (c != '1' && c != '2' &&   
                c != '3' && c != '4' && c != '5') {  
                System.out.print("选择错误，请重新输入：");  
            } else break;  
        }  
        return c;  
    }  
  
   /**  
    * 功能：读取键盘输入的一个字符  
    * @return 一个字符  
    */  
    public static char readChar() {  
        String str = readKeyBoard(1, false);//就是一个字符  
        return str.charAt(0);  
    }  
    /**  
     * 功能：读取键盘输入的一个字符，如果直接按回车，则返回指定的默认值；否则返回输入的那个字符  
     * @param defaultValue 指定的默认值  
     * @return 默认值或输入的字符  
     */  
    public static char readChar(char defaultValue) {  
        String str = readKeyBoard(1, true);//要么是空字符串，要么是一个字符  
        return (str.length() == 0) ? defaultValue : str.charAt(0);  
    }  
   /**  
     * 功能：读取键盘输入的整型，长度小于2位  
     * @return 整数  
     */  
    public static int readInt() {  
        int n;  
        for (; ; ) {  
            String str = readKeyBoard(2, false);//一个整数，长度<=2位  
            try {  
                n = Integer.parseInt(str);//将字符串转换成整数  
                break;  
            } catch (NumberFormatException e) {  
                System.out.print("数字输入错误，请重新输入：");  
            }  
        }  
        return n;  
    }  
    /**  
     * 功能：读取键盘输入的 整数或默认值，如果直接回车，则返回默认值，否则返回输入的整数  
     * @param defaultValue 指定的默认值  
     * @return 整数或默认值  
     */  
    public static int readInt(int defaultValue) {  
        int n;  
        for (; ; ) {  
            String str = readKeyBoard(10, true);  
            if (str.equals("")) {  
                return defaultValue;  
            }  
         //异常处理...  
            try {  
                n = Integer.parseInt(str);  
                break;            } catch (NumberFormatException e) {  
                System.out.print("数字输入错误，请重新输入：");  
            }  
        }  
        return n;  
    }  
  
    /**  
     * 功能：读取键盘输入的指定长度的字符串  
     * @param limit 限制的长度  
     * @return 指定长度的字符串  
     */  
  
    public static String readString(int limit) {  
        return readKeyBoard(limit, false);  
    }  
  
    /**  
     * 功能：读取键盘输入的指定长度的字符串或默认值，如果直接回车，返回默认值，否则返回字符串  
     * @param limit 限制的长度  
     * @param defaultValue 指定的默认值  
     * @return 指定长度的字符串  
     */  
   public static String readString(int limit, String defaultValue) {  
        String str = readKeyBoard(limit, true);  
        return str.equals("")? defaultValue : str;  
    }  
  
  
   /**  
    * 功能：读取键盘输入的确认选项，Y或N  
    * 将小的功能，封装到一个方法中.  
    * @return Y或N  
    */    public static char readConfirmSelection() {  
        System.out.println("请输入你的选择(Y/N)");  
        char c;  
        for (; ; ) {//无限循环  
           //在这里，将接受到字符，转成了大写字母  
           //y => Y n=>N  
            String str = readKeyBoard(1, false).toUpperCase();  
            c = str.charAt(0);  
            if (c == 'Y' || c == 'N') {  
                break;  
            } else {  
                System.out.print("选择错误，请重新输入：");  
            }  
        }  
        return c;  
    }  
  
    /**  
     * 功能： 读取一个字符串  
     * @param limit 读取的长度  
     * @param blankReturn 如果为true ,表示 可以读空字符串。   
*                   如果为false表示 不能读空字符串。  
     *             
* 如果输入为空，或者输入大于limit的长度，就会提示重新输入。  
     * @return  
     */  
    private static String readKeyBoard(int limit, boolean blankReturn) {  
        //定义了字符串  
      String line = "";  
  
      //scanner.hasNextLine() 判断有没有下一行  
        while (scanner.hasNextLine()) {  
            line = scanner.nextLine();//读取这一行  
           //如果line.length=0, 即用户没有输入任何内容，直接回车  
         if (line.length() == 0) {  
                if (blankReturn) return line;//如果blankReturn=true,可以返回空串  
                else continue; //如果blankReturn=false,不接受空串，必须输入内容  
            }  
  
         //如果用户输入的内容大于了 limit，就提示重写输入    
//如果用户如的内容 >0 <= limit ,我就接受  
            if (line.length() < 1 || line.length() > limit) {  
                System.out.print("输入长度（不能大于" + limit + "）错误，请重新输入：");  
                continue;            }  
            break;  
        }  
  
        return line;  
    }  
}
```

`TestUtility.java`

```
package com.cwz.houserent.Utility;  
  
  
public class TestUtility {  
    public static void main(String[] args) {  
  
        //这时一个测试类，使用完毕，就可以删除  
        //要求输入一个字符串，长度最大为3  
        String s = Utility.readString(3);  
  
        //要求输入一个字符串，长度最大为10，如果用户直接回车，就给一个默认值  
        System.out.println("请输入字符串：");  
        String s2 = Utility.readString(10, "cwz");  
        System.out.println("s2=" + s2);  
  
        //这里直接使用 类.方法（） =>因为当一个方法是static时，就是一个静态方法  
        //注意：静态方法可以直接通过类名调用  
        A.cry();  
        //A.hi(); 不是静态方法不能调用  
    }  
}  
  
class A{  
    public static void cry(){}  
    public void hi(){}  
}
```

`HouseView.java`

```
package com.cwz.houserent.view;  
  
import com.cwz.houserent.Utility.Utility;  
import com.cwz.houserent.domain.House;  
import com.cwz.houserent.service.HouseService;  
  
import javax.swing.plaf.IconUIResource;  
  
/**  
 * 1.显示界面  
 * 2.接受用户的输入  
 * 3.调用HouseService完成对房屋信息的各种操作  
 */  
public class HouseView {  
  
    private boolean loop = true;//控制显示菜单  
    private char key = ' ';//接受用户的选择  
    private HouseService houseService = new HouseService(10);//设置数组的大小为10  
  
  
    //根据id修改房屋信息  
    public void update(){  
        System.out.println("============修改房屋信息============");  
        System.out.println("请选择待修改房屋编号(-1表示退出)");  
        int updateId = Utility.readInt();  
        if(updateId == -1){  
            System.out.println("============你放弃修改房屋信息============");  
            return ;        }  
  
        //根据输入的updateId查找对象  
        House house = houseService.findById(updateId);//返回的是引用类型[即：就是数组的元素]  
        //因此在后面对house.setXxx().就会修改HouseService中的houses数组的元素  
        if(house == null){  
            System.out.println("============修改的房屋信息编号不存在..============");  
            return ;        }  
        System.out.print("姓名("+house.getName()+"): ");  
        String name = Utility.readString(8,"");//这里如果用户直接回车表示不修改该信息，默认""  
        if(!"".equals(name)){//修改  
            house.setName(name);  
        }  
  
        System.out.print("电话("+house.getPhone()+"): ");  
        String phone = Utility.readString(12,"");  
        if(!"".equals(phone)){//修改  
            house.setPhone(phone);  
        }  
  
        System.out.print("地址("+house.getAddress()+"): ");  
        String address = Utility.readString(18,"");  
        if(!"".equals(address)){  
            house.setAddress(address);  
        }  
  
        System.out.print("租金("+house.getRent()+"): ");  
        int rent = Utility.readInt(-1);  
        if(rent != -1){  
            house.setRent(rent);  
        }  
  
        System.out.print("状态("+house.getState()+"): ");  
        String state = Utility.readString(3, "");  
        if(!"".equals(state)){  
            house.setState(state);  
        }  
        System.out.println("============修改房屋信息成功============");  
    }  
  
    //根据id查找房屋信息  
    public void findHouse(){  
        System.out.println("============查找房屋信息============");  
        System.out.println("请输入要查找的id：");  
        int findId = Utility.readInt();  
        //调用方法  
        House house = houseService.findById(findId);  
        if(house != null){  
            System.out.println("============查找房屋信息ID不存在============");  
        }  
    }  
  
    //完成退出确认  
    public void exit(){  
        //这里我们使用Utility提供的方法，完成确认  
        char c = Utility.readConfirmSelection();  
        if(c == 'Y') {  
            loop = false;  
        }  
    }  
  
    //编写delHouse()接收输入，创建House对象，调用add方法  
    public void delHouse(){  
        System.out.println("============添加房屋信息============");  
        System.out.println("请输入待删除房屋的编号(-1退出)：");  
        int delID = Utility.readInt();  
        if(delID == -1){  
            System.out.println("============放弃删除房屋信息============");  
            return;        }  
        char choice = Utility.readConfirmSelection();  
        //注意该方法本身就有循环判断逻辑，必须输入Y/N  
        if(choice == 'Y'){//真的删除  
            if(houseService.del(delID)){  
                System.out.println("============删除房屋信息成功============");  
            }else{  
                System.out.println("============房屋编号不存在，删除失败============");  
            }  
        }else{  
            System.out.println("============放弃删除房屋信息============");  
        }  
    }  
  
  
    //编写addHouse()接受输入，创建House对象，调用add方法  
    public void addHouse(){  
        System.out.println("============添加房屋============");  
        System.out.println("姓名：");  
        String name = Utility.readString(8);  
        System.out.println("电话：");  
        String phone = Utility.readString(12);  
        System.out.println("地址：");  
        String address = Utility.readString(16);  
        System.out.println("月租：");  
        int rent = Utility.readInt();  
        System.out.println("状态：");  
        String state = Utility.readString(3);  
        //创建一个新的house对象  
        //注意id时系统分配的，用户不能输入  
        House newHouse = new House(0, name, phone, address, rent, state);  
        if(houseService.add(newHouse)){  
            System.out.println("添加房屋成功");  
        }else{  
            System.out.println("添加房屋失败");  
        }  
  
  
    }  
  
    //编写listHouse（）显示房屋列表  
    public void listHouse(){  
        System.out.println("============房屋列表============");  
        System.out.println("编号\t\t  房屋\t\t 电话\t\t  地址\t\t  月租\t\t  状态(未出租/已出租)");  
        House[] houses = houseService.list();//得到所有的房屋信息  
        for (int i = 0; i < houses.length; i++) {  
            if(houses[i] == null){  
                break;  
            }  
            System.out.println(houses[i]);  
        }  
        System.out.println("============房屋列表显示完毕============");  
    }  
    //显示一个主菜单  
    public void mainMenu(){  
  
        do{  
            System.out.println("\n============房屋出租系统菜单============");  
            System.out.println("\t\t\t1 新 增 房 源");  
            System.out.println("\t\t\t2 查 找 房 屋");  
            System.out.println("\t\t\t3 删 除 房 屋 信 息");  
            System.out.println("\t\t\t4 修 改 房 屋 信 息");  
            System.out.println("\t\t\t5 显 示 房 屋 信 息");//房屋列表  
            System.out.println("\t\t\t6 退           出");  
            System.out.print("请输入你的请求(1-6): ");  
            key = Utility.readChar();  
            switch (key){  
                case '1' :  
                    addHouse();  
                    break;                case '2' :  
                    findHouse();  
                    break;                case '3' :  
                    delHouse();  
                    break;                case '4' :  
                    update();  
                    break;                case '5' :  
                    listHouse();  
                    break;                case '6' :  
                    exit();  
                    break;            }  
  
        }while(loop);  
  
    }  
}
```

`HouseRentApp.java`

```
package com.cwz.houserent;  
  
import com.cwz.houserent.domain.House;  
import com.cwz.houserent.view.HouseView;  
  
public class HouseRentApp {  
    public static void main(String[] args) {  
        //创建HouseView对象，并且显示主菜单，是整个程序的入口  
        new HouseView().mainMenu();//创建匿名对象  
        System.out.println("===你退出房屋出租系统===");  
  
    }  
}
```

# 5. 枚举

## 5.1 枚举引出

创建Season对象有如下的特点

1. 季节的值只有限定的几个值
2. 只读，不需要修改

解决方案-枚举

1. 枚举对应英文(enumeration,简写enum)
2. 枚举是一组常量的集合
3. 可以这里理解:枚举属于一种特殊的类，里面只包含一组有限的特定的对象

```
package com.cwz.enum_;  
  
public class Enumeration01 {  
    public static void main(String[] args) {  
        //使用  
        Season spring = new Season("春天", "温暖");  
        Season summer = new Season("夏天", "炎热");  
        Season winter = new Season("冬天", "寒冷");  
        Season autumn = new Season("秋天", "凉爽");  
        //因为对于季节而言，它的对象(具体值)，是固定四个，不会有更多  
        //不能体现季节时固定的四个对象  
        //因此这样设计不好====> 枚举类[把具体对象一个个列举出来]  
        Season other = new Season("红天","~~~");  
  
    }  
}  
  
class Season{ //类  
    private String name;  
    private String desc;//描述  
  
    public Season(String name, String desc) {  
        this.name = name;  
        this.desc = desc;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public String getDesc() {  
        return desc;  
    }  
  
    public void setDesc(String desc) {  
        this.desc = desc;  
    }  
}
```

## 5.2 自定义实现枚举

1. 不需要提供seXxx方法，因为枚举对象值通常只读
2. 对枚举对象/属性使用final + static共同修饰，实现底层优化
3. 枚举对象名通常使用全部大写，常量的命名规范
4. 枚举对象根据需要，也可以有多个属性

```
package com.cwz.enum_;  
  
/**  
* @author  陈文臻  
*/  
public class Enumeration02 {  
    public static void main(String[] args) {  
        System.out.println(Season1.AUTUMN);  
    }  
}  
  
//演示自定义枚举实现  
class Season1{ //类  
    private String name;  
    private String desc;//描述  
    //3.在Season内部，直接创建固定好的对象  
    //定义了四个对象  
    //4.优化可以加入final修饰符  
    public final static Season1 SPRING = new Season1("春天", "温暖");  
    public final static Season1 SUMMER = new Season1("夏天", "炎热");  
    public final static Season1 WINTER = new Season1("冬天", "寒冷");  
    public final static Season1 AUTUMN = new Season1("秋天", "凉爽");  
  
    //1.将构造器私有化，防止直接被new出来  
    private Season1(String name, String desc) {  
        this.name = name;  
        this.desc = desc;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    //2.去掉set的相关方法 防止属性被修改  
//    public void setName(String name) {  
//        this.name = name;  
//    }  
  
    public String getDesc() {  
        return desc;  
    }  
  
    public void setDesc(String desc) {  
        this.desc = desc;  
    }  
  
    @Override  
    public String toString() {  
        return "Season1{" +  
                "name='" + name + '\'' +  
                ", desc='" + desc + '\'' +  
                '}';  
    }  
}
```

## 5.3 enum关键字实现枚举

1. 当我们使用enum关键字开发一个枚举类时，默认会继承Enum类
2. 传统的public static final Season2 SPRING = new Season2(“传统”， “温暖”);简化成SPRING("春天", “温暖”)，这里必须知道，它调用的是哪个构造器
3. 如果使用无参构造器 创建 枚举对象，则实参列表和小括号就可以省略
4. 当多个枚举对象时，使用,间隔，最后一个分号结尾
5. 枚举对象必须放在枚举类的行首

```
package com.cwz.enum_;  
  
/**  
 * @author 陈文臻  
 */  
public class Enumeration03 {  
    public static void main(String[] args) {  
        System.out.println(Season2.AUTUMN);  
    }  
}  
  
  
//演示自定义枚举实现  
enum Season2{//类  
    //1.使用关键字enum替代class  
    //2.public static final Season SPRING = new Season("春天", "温暖")直接使用  
    //  SPRING("春天", "温暖") 解读 常量名(实参列表)  
    //3.将构造器私有化，防止直接被new出来  
    //4.如果有多个常量(对象)，使用逗号间隔即可  
    //如果使用enum来实现枚举，要求将定义常量对象，写在前面  
  
    SPRING("春天", "温暖"), SUMMER("夏天", "炎热"), WINTER("冬天", "寒冷"), AUTUMN("秋天", "凉爽");  
    private String name;  
    private String desc;  
    private Season2(String name, String desc) {  
        this.name = name;  
        this.desc = desc;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    //2.去掉set的相关方法 防止属性被修改  
//    public void setName(String name) {  
//        this.name = name;  
//    }  
  
    public String getDesc() {  
        return desc;  
    }  
  
    public void setDesc(String desc) {  
        this.desc = desc;  
    }  
  
    @Override  
    public String toString() {  
        return "Season1{" +  
                "name='" + name + '\'' +  
                ", desc='" + desc + '\'' +  
                '}';  
    }  
    }
```

## 5.4 enum的常用方法

|   |   |
|---|---|
|方法名|详细描述|
|valueOf|传递枚举类型的Class对象和枚举常量名称给静态方法valueOf，会得到与参数匹配的枚举常量|
|toString|得到当前枚举常量的名称。你就而已通过重写这个方法来使得得到的结构更易读|
|equals|在枚举类型中可以直接使用 == 来比较两个枚举常量是否相等。Enum提供的这个equals()方法，也是直接使用 == 实现的。它的存在是为了在Set、List和Map中使用。注意，equals是不可变的|
|hashCode|Enum实现了hashCode()来和equals()保持一致。它也是不可变的|
|getDeclaringClass|得到枚举常量所属枚举类型的Class对象。可以用它来判断两个枚举常量是否属于同一个枚举类型|
|name|得到当前枚举常量的名称。建议优先使用toString|
|ordinal|得到当前枚举常量的次序|
|compareTo|枚举类型实现了Comparable接口，这样可以比较两个枚举常量的大小(按照声明的顺序排序)|
|clone|枚举类型不能被clone。为了防止类实现克隆方法，Enum实现了一个仅抛出CloneNotSupportException异常的不变Clone()|
|||

1. toString: Enum类已经重写过了，返回的是当前对象名，子类可以重写该方法，用于返回对象的属性信息
2. name: 返回当前对象名(常量名), 子类中不能重写
3. ordinal: 返回当前对象的位置号，默认从0开始
4. values：返回当前枚举类中的所有的常量
5. valueOf：将字符串转换成枚举对象，要求字符串必须为己有的常量名，否则报异常
6. compareTo：比较两个枚举常量，比较的就是编号

```
package com.cwz.enum_;  
  
/**  
 * @author 陈文臻  
 * 演示enum类的各种方法的演示  
 */  
public class EnumMethod {  
    public static void main(String[] args) {  
        //使用season2 枚举类，来演示各种方法  
        Season2 autumn = Season2.AUTUMN;  
        //输出枚举对象的名称  
        System.out.println(autumn.name());  
        //输出该枚举对象的次序/编号，从0开始编号  
        System.out.println(autumn.ordinal());  
        System.out.println();  
        //从反编译可以看出 values方法，返回Season2[]  
        //含有定义的所有枚举对象  
        System.out.println("===遍历取出枚举对象===");  
        Season2[] values = Season2.values();  
        for(Season2 season: values){//增强for循环  
            System.out.println(season);  
        }  
        //valueOf：将字符串转换成枚举对象，要求字符串必须为己有的常量名，否则报异常  
        //执行流程  
        //1.根据你输入的"AUTUMN"到Season2的枚举对象去查找  
        //2.如果找到了，就返回，如果没找到，就报错  
        Season2 autumn1 = Season2.valueOf("AUTUMN");  
        System.out.println("autumn=" + autumn1);  
        //autumn和autumn1是同一对象  
        System.out.println(autumn1 == autumn);//返回true  
  
        //compareTo：比较两个枚举常量，比较的就是编号  
        //1.就是把 Season2.AUTUMN 枚举对象的编号和 Season2.SUMMER枚举对象的编号比较  
        //2.看看结果  
        /*  
        public final int compareTo(E o){  
            return self.ordinal - other.ordinal;        }        Season2.AUTUMN的编号 - Season2.SUMMER的编号  
         */        System.out.println(Season2.AUTUMN.compareTo(Season2.SUMMER));  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712024611331-ac1b6a11-0f30-44ef-89be-0780aeed5cbc.png)

## 5.5 enum实现接口

1. 使用enum关键字后，就不能再继承其他类了，因为enum会隐式继承Enum，而Java是单继承模式
2. 枚举类和普通类一样，可以实现接口

- enum 类名 implements 接口1,接口2{ }

# 6. 注解

## 6.1 基本介绍

1. 注解(Annotation)也被称为元数据，用于修饰解释 包、类、方法、属性、构造器、局部变量等数据信息
2. 和注释一样，注解不影响程序逻辑，但注解可以被编译或运行，相当于嵌入再代码中的补充信息
3. 在JavaSE中，注解的使用的目的比较简单，例如标记过的功能，忽略警告等。在JavaEE中注解占据了更重要的角色，例如用来配置应用程序的任何页面，代替Java EE旧版的繁杂代码和XML配置等

## 6.2 基本的Annotation介绍

使用Annotation时要在前面增加@符号，并把该Annotation当成一个修饰符使用。用于修饰它支持的程序元素  
->三个基本的Annotation

1. @Override:限定某个方法，是重写父类方法，该注解只能用于方法
2. @Deprecated:用于表示某个程序元素(类，方法等)已过时
3. @SuppressWarnings:抑制编译器警告

### 6.2.1 [@Override](/Override)

Override使用说明

1. @Override表示只当重写父类的方法(从编译层面验证)，如果父类没有fly方法，则会报错
2. 如果不屑@Override注解，而父类仍有public void fly(){},则仍然构成重写
3. [@Override](/Override) 只修饰方法，不能修饰其他类，包，属性等等
4. 查看@Override注解源码为@Target(ElementType.METHOD),说明只能修饰方法
5. [@Target](/Target) 是修饰注解的注解，称为元注解

```
package com.cwz.annotation;  
  
  
/**  
 * @author 陈文臻  
 */  
public class Override {  
    public static void main(String[] args) {  
  
    }}  
class Father {//父类  
    public void fly(){  
        System.out.println("father fly...");  
    }  
}  
  
class Son extends Father{//子类  
    //1.@Override 注解放在fly方法上，表示子类的fly方法重写了父类的fly方法  
    //2.这里如果没有写 @Override 还是重写了父类fly  
    //3.如果你写了 @Override注解，编译器就会检查该方法是否真的重写了父类的方法  
    //  如果，的确重写了，则编译通过，否则，则编译错误  
    @java.lang.Override//说明  
    public void fly() {  
        System.out.println("Son fly...");  
    }  
}
```

### 6.2.2 [@Deprecated](/Deprecated)

1. 用于表示某个程序元素(类，方法)已过时
2. 可以修饰方法，类，字段，包，参数等等
3. @Target(value={CONSTRUCTOR,FIELD,LOCAL_VARIABLE,METHOD,PACKAGE,PARAMETER,TYPE})
4. @Deprecated的作用可以做到新旧版本的兼容过度

```
package com.cwz.annotation;  
  
/**  
 * @author 陈文臻  
 */  
public class Deprecated {  
    public static void main(String[] args) {  
        A a = new A();  
        a.hi();  
        System.out.println(a.n1);  
    }  
}  
  
//1.@Deprecated 修饰某个元素，表示该元素已经过时  
//2，即不推荐使用，但是仍然可以使用  
@java.lang.Deprecated  
class A{  
    @java.lang.Deprecated  
    public int n1 = 10;  
    @java.lang.Deprecated  
    public void hi(){  
            }  
}
```

### 6.2.3 [@SuppressWarnings](/SuppressWarnings)

|   |   |   |
|---|---|---|
|符号|作用||
|all|抑制所有警告||
|cast|抑制与强转型作业相关的警告||
|boxing|抑制与封装/拆装作业相关的警告||
|dep-ann|抑制与淘汰注释相关的警告||
|deprecation|抑制与淘汰相关的警告||
|fallthrough|抑制与switch陈述式中遗漏break相关的警告||
|finally|抑制与未传回finally区块相关的警告||
|hiding|抑制与以隐藏变数的区域相关的警告||
|incomplete-switch|抑制与switch陈述式(enum case)中遗漏项目相关的警告||
|javadoc|抑制与javadoc相关的警告||
|nls|抑制与非nls字串文字相关的警告||
|null|抑制与控制分析相关的警告||
|rawtypes|抑制与使用raw类型相关的警告||
|resource|抑制与使用Cloneable类型的资源相关的警告||
|restriction|抑制与使用不建议或禁止参照相关的警告||
|serial|抑制与可序列化的类别遗漏serialVersionUID栏位相关的警告||
|static-acess|抑制与存取不正确相关的警告||
|static-method|抑制与可能宣告为static的方法相关的警告||
|super|抑制与置换同步方法而遗漏同步化的警告||
|synthetic-access|抑制与内部类别的存取未最佳化相关的警告||
|sync-override|抑制因为置换同步方法而遗漏同步化的警告||
|unchecked|抑制与未检查的作业相关的警告||
|unqualified-ffield-access|抑制与栏位存取不合格相关的警告||
|unused|抑制与未用的程序码及停用的程序码相关的警告||

```
package com.cwz.annotation;  
  
import java.util.ArrayList;  
import java.util.List;  
  
/**  
 * @author 陈文臻  
 */  
public class SuppressWarnings {  
    //1.当我们不希望看到这些警告的时候，可以使用 SuppressWarnings 注解来抑制警告信息  
    //2.在大括号中可以写入你希望抑制(不显示)警告信息  
    //3.关于SuppressWarnings的作用范围是和你放置的位置相关  
    //  比如@SuppressWarnings放置在main方法，那么抑制警告的范围就是main  
    //4.通常我们可以放在具体的语句、方法、类  
    @java.lang.SuppressWarnings({"all"})  
    public static void main(String[] args) {  
        List list = new ArrayList();  
        list.add("");  
        list.add("");  
        list.add("");  
        int i;  
        System.out.println(list.get(1));  
    }  
}
```

## 6.3 JDK的元

### 6.3.1 基本介绍

JDK的元Annotation用于修饰其他Annotation  
元注解：本身作用不大，讲这个原因希望同学们，看源码时，可以知道他是干什么  
==修饰注解的注解==

### 6.3.2元注解的种类

(使用不多，了解，不用深入研究)

1. Retention //指定注解的作用范围，三种SOURCE,CLASS,RUNTIME
2. Target //指定注解可以在哪些地方使用
3. Documented //指定该注解是否会在javadoc体现
4. Inherited //子类会继承父类注解

### 6.3.3 [@Retention](/Retention) 注解

#### 6.3.3.1 说明:

只能用于修饰一个Annotation定义，用于指定该Annotation可以保留多长时间，@Rentention包含一个 RetentionPolicy类型的成员变量，使用@Rentention时必须为该value成员变量指定值

#### 6.3.3.2 @Retention的三种值

1. RetentionPolicy.SOURCE:编译器使用后，直接丢弃这种策略的注释
2. RetentionPolicy.CLASS:编译器将把注释记录在class文件中.当运行Java程序时，JVM不会保留注解。这是默认值
3. RetentionPolicy.RUNTIME:编译器将把注解记录在class文件中。当运行Java程序时，JVM会保留注释，程序可以通过反射获取该注解

### 6.3.4 [@Target](/Target)

#### 6.3.4.1 基本说明

用于修饰Annotation定义，用于指定被修饰的Annotation能用于修饰哪些程序元素。@Target也包含一个名为value的成员变量

### 6.3.5 [@Documented](/Documented)

#### 6.3.5.1 基本说明

@Documented:用于指定被该元Annotation修饰的Annotation类将被Javadoc工具提取成文档，即在生成文档时，可以看到该注释

说明：定义为Documented的注解必须设置Retention值为RUNTIME

### 6.3.6[@Inherited](/Inherited)

把它修饰的Annotation将具有继承性。如果某个类使用了被@Inherited修饰的Annotation，则其子类将自动具有该注解

# 7. 异常处理

## 7.1 异常引入

```
package com.cwz.exception;  
  
/**  
 * @author 陈文臻  
 */  
public class Exception01 {  
    public static void main(String[] args) {  
        int num1 = 10;  
        int num2 = 0;  
        //1.num1 / num2 => 10 / 0  
        //2.当执行到 num1 / num2 因为num2 = 0，程序就会出现(抛出)异常 ArithmeticException        //3.当抛出异常后，程序就退出，奔溃了，下面的代码就不在执行  
        //4.大家想想这样的程序好吗？不好，不应该出现一个不算致命的问题，就导致整个系统奔溃  
        //5.java设计者，提供一个叫 异常处理机制来解决该问题  
//        int res = num1 / num2;  
        //如果程序员认为一段代码可能出现异常/问题，可以使用try-catch异常处理机制来解决  
        //从而保证程序的健壮性  
        //将改代码块选中 ctrl + alt + t 选中6  
        //6.那么进行异常处理，那么即使出现异常，程序可以继续执行  
        try {  
            int res = num1 / num2;  
        } catch (Exception e) {  
            //e.printStackTrace();  
            System.out.println(e.getMessage());//输出异常信息  
        }  
  
        System.out.println("程序正在运行...");  
  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712024502193-b380ea8b-20e7-4ab7-b461-07c3485be104.png)

## 7.2 基本概念

Java语言中，将程序执行中发生的不正常情况称为"异常"。(开发过程中的语法错误和逻辑错误不是异常)

- 执行过程中发生的异常事件可以分为两类

1. Error(错误)：Java虚拟机无法解决的严重问题。如:JVM系统内部错误、资源耗尽等严重情况。比如:StackOverflowError[栈溢出]和OOM(out of memory),Error是严重错误，程序会奔溃
2. Exception：其他因编程错误或偶然的外在因素导致的一般性问题，可以再使用针对性的代码进行处理。例如空指针访问，试图读取不存在的文件，网络连接中断等等，Exception 分为两大类:运行时异常[]和编译时异常[]

## 7.3 异常体系图(!!!)

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712024619232-81e8bd47-591b-493e-a865-5b5817117b45.png)

1. 异常分为两大类，运行异常和编译异常
2. 运行时异常，编译器检测不出来，编译器不要求强制处置的异常。一般指编程时的逻辑错误，时程序员应该避免其出现的异常
3. 对于运行异常，可以不做处理，因为这类异常很普通，若全处理可能会对程序的可读性和运行效率产生影响
4. 编译时异常，是编译器要求必须处置的异常

## 7.4 常见的异常

1. NullPointException 空指针异常
2. AirthmeticException 数字运算异常
3. ArrayIndexOutOfBoundsException 数字下标越界异常
4. ClassCastException 类型转换异常
5. NumberFormatException 数字格式不正确异常

### 7.4.1 NullPointException 空指针异常

当应用程序试图在需要对象的地方使用null时，抛出该异常

```
public class NullPointException {  
    public static void main(String[] args) {  
  
        String name = null;  
        System.out.println(name.length());  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712024631789-1b23cb65-2398-474e-a16b-f3638bff269d.png)

### 7.4.2 ArrayIndexOutOfBoundsException 数字下标越界异常

当出现异常的运算条件时，抛出此异常。例如，一个整数"除以零"时，抛出此类的一个实例

```
public class ArrayIndexOutOfBoundsException {  
    public static void main(String[] args) {  
        int[] arr = {1,2,4};  
        for (int i = 0; i <= arr.length; i++) {  
            System.out.println(arr[i]);  
        }  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712024641136-66be18f1-5e0e-417c-b8d2-8638e0c38393.png)

### 7.4.3ClassCastException 类型转换异常

当试图将对象强制转换为不是实例的子类时，抛出该异常

```
package com.cwz.exception;  
  
/**  
 * @author 陈文臻  
 */  
public class ClassCastException {  
    public static void main(String[] args) {  
        A b = new B();//向上转型  
        B b2 = (B)b;//向下转型，这里是ok的  
        C c2 = (C)b;//这里抛出ClassCastException  
    }  
}  
class A {}  
class B extends A {}  
class C extends A {}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712024648416-98899fc2-378e-4014-8934-dcced217e16a.png)

### 7.4.4 NumberFormatException 数字格式不正确异常

当应用程序试图将字符串转换成一种数值类型，但该字符串不能转换为适当格式时，抛出该异常 => 使用异常我们可以确保输入是满足条件数字

```
public class NumberFormatException {  
    public static void main(String[] args) {  
        String name = "陈文臻";  
        //将String 转成 int        int num = Integer.parseInt(name);  
        System.out.println(num);  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712024656028-3140844e-5e50-4965-9838-5d267b023cef.png)

## 7.5 编译异常

编译异常是指编译期间，就必须处理的异常，否则代码不能通过编译

**常见的编译异常**

|   |   |
|---|---|
|异常|内容|
|SQLException|操作数据库时，查询表可能发生异常|
|IOException|操作文件时，发生的异常|
|FileNotFoundException|当操作一个不存在的文件时，发生异常|
|EOFException|操作文件，到文件末尾，发生异常|
|IllegalArguementException|参数异常|

### 7.5.1 异常处理

#### 7.5.1.1 基本概念

异常处理就是当异常发生时，对异常处理的方式

**异常处理的方式**

1. try-catch-finally  
    程序员在代码中捕获发生的异常，自行处理
2. throws  
    将发生的异常抛出，交给调用者(方法)来处理，最顶级的处理者就是JVM

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712024676438-8a888a5b-beb2-42df-bfb6-b05d3e62e8e6.png)

### 7.5.2 try-catch异常处理

#### 7.5.2.1 基本介绍

1. java提供try和catch块来处理异常。try块用于包含可能出错的代码。catch块用于处理try块中发生的异常。可以根据需求在程序中有多个数量的try...catch块
2. 基本语法

```
try{
	//可疑代码
	//将异常生成对应的异常对象，传递给catch块
	}catch(异常){
	//对异常的处理
}

//如果没有finally。语法可以通过
```

#### 7.5.2.2 注意事项

- 如果异常发生了，则异常发生后面的代码不会执行，直接进入catch块
- 如果异常没有发生，则顺序执行try的代码块，不会进入到catch
- 如果希望不管是否发生异常，都执行某段代码(比如关闭连接，释放资源等)则使用finally{}

```
public class TryCatchDetail {  
    public static void main(String[] args) {  
        //ctrl + alt + t  
        //如果异常发生了，则异常发生后面的代码不会执行，直接进入catch块  
        try {  
            String str = "陈文臻";  
            int a = Integer.parseInt(str);  
            System.out.println("数字:" + a);  
        } catch (NumberFormatException e) {  
            System.out.println("异常信息=" + e.getMessage());  
        }finally {  
            System.out.println("finally代码块被执行");  
        }  
  
        System.out.println("程序继续...");  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712026893795-1de99446-faa9-4c1b-9722-9f2f26864396.png)

- 可以有多个catch语句，捕获不同的异常(进行不同的业务处理)，要求父类异常在后，子类异常在前，比如(Exceptition在后， NullPointerException在前)，如果发生异常，就会匹配一个catch

```
public class TryCatchDetail02 {  
    public static void main(String[] args) {  
        //如果try代码块可能有多个异常  
        //可以使用多个catch 分别捕获不同的异常，相应处理  
        //要求子类异常写在前面，父类异常写在后面  
        try {  
            Person person = new Person();  
            System.out.println(person.getName());//空指针异常  
            int n1 = 10;  
            int n2 = 0;  
            int res = n1 / n2;//算数异常  
        }catch (NullPointerException e){  
            System.out.println("空指针异常= " + e.getMessage());  
        }  
        catch (ArithmeticException e){  
            System.out.println("算数异常= " + e.getMessage());  
        } catch (Exception e) {  
            System.out.println(e.getMessage());  
        }finally {  
  
        }    }  
}  
  
class Person{  
    private String name;  
  
    public String getName() {  
        return name;  
    }  
}
```

- 可以进行try-finally配合使用，这种用法相当于没有捕获异常，因此程序会直接崩掉/退出。应用场景:不管是否发生异常，都必须执行某个业务逻辑

```
public class TryCatchDetail03 {  
    public static void main(String[] args) {  
  
        try {  
            int n1 = 10;  
            int n2 = 0;  
            System.out.println(n1 / n2);  
        }finally {  
            System.out.println("执行finally...");  
        }  
  
        System.out.println("程序继续执行");  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712026908451-4282e9f5-f70f-40a9-a026-8a85dbf935cf.png)

### 7.5.3 throws异常处理

#### 7.5.3.1 基本介绍

- 如果一个方法(中的语句执行时)可能称为某种异常，但是并不能确定如何处理这些异常，则此方法应显示地声明抛出异常，表明该方法将不对这些异常进行处理，而该方面的==调用者负责处理
- 在方法声明中用throws语句可以声明抛出异常的列表，throws后面的异常类型可以是方法中产生的异常类型，也可以是它的父类

```
public class Throws01 {  
    public static void main(String[] args) {  
  
  
    }  
    public void f2() throws Exception/*FileNotFoundException*/{  
        //创建了一个文件流对象  
        //异常处理:  
        //1. 这里的异常时一个FileNOotFoundException 编译异常  
        //2，使用前面讲过的try-catch-finally  
        //3. 使用throws，抛出异常,让调用f1方法的调用者(方法)处理  
        //4. 在方法声明中用throws语句可以声明抛出异常的列表，  
        //  throws后面的异常类型可以是方法中产生的异常类型，也可以是它的父类  
        //5. throws 关键字后也可以时 异常列表，即可以抛出多个异常  
  
//        try {  
//            FileInputStream fis = new FileInputStream("d://a.txt");  
//        } catch (FileNotFoundException e) {  
//            e.printStackTrace();  
//        }  
  
        FileInputStream fis = new FileInputStream("d://a.txt");  
    }  
  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712026927086-837b5183-fd8d-4d64-81f6-4fd32d46a308.png)

#### 7.5.3.2 注意事项

1. 对于编译异常，程序中必须处理，比如try-catch或者throws
2. 对应运行时异常，程序中如果没有处理，默认就是throws的方式处理
3. 子类和重写父类的方法时，对抛出异常的规定:子类重写的方法，所抛出的异常类型要么和父类额异常一致，要么为父类抛出的异常的类型的子类型
4. 在throws过程中，如果有方法try-catch，就相当于处理异常，就可以不必throws

### 7.5.4 自定义异常

步骤

1. 定义类:自定义异常类名(程序员自己写)继承Exception或RuntimeException
2. 如果继承Exception，属于编译异常
3. 如果继承RuntimeException，属于运行异常(一般来说，继承RuntimeException)

```
public class CustomException {  
    public static void main(String[] args) {  
  
        int age = 80;  
        //要求范围在 18 - 120 之间，否则抛出一个自定义异常  
        if(!(age >= 18 && age <= 120)) {  
            //这里可以通过构造器设置信息  
            throw new AgeException("年龄需要在 18~120之间");  
        }  
        System.out.println("你的年龄范围正确");  
    }  
}  
//自定义异常  
//1.一般情况下，自定义异常时继承RuntimeException  
//2.即自定义异常做成运行时异常，好处是，我门可以使用默认的处理机制  
//3.即比较方便  
class AgeException extends RuntimeException{  
    public AgeException(String message) {//构造器  
        super(message);  
    }  
}
```

### 7.5.5 throw和throws的对比

|   |   |   |   |
|---|---|---|---|
||意义|位置|后面跟的东西|
|thorws|异常处理的一种方式|方法声明处|异常类型|
|throw|手动生成异常对象的关键字|方法体中|异常对象|

# 8. 常用类

## 8.1 包装类

### 8.1.1 包装类的分类

1. 针对八种基本数据类型定义相应的引用类型——包装类
2. 有了类的特点就可以调用类的方法

|   |   |
|---|---|
|基本数据类型|包装类|
|boolean|Boolean|
|char|Character|
|byte|Byte|
|short|Short|
|int|Integer|
|long|Long|
|float|Float|
|double|Double|

### 8.1.2 包装类和基本数据的转换

1. jdk5 前的手动装箱和拆箱方式，==装箱: 基本类型 -> 包装类型==，反之，拆箱
2. jdk5 以后(含jdk5)的自动装箱和拆箱方式
3. 自动装箱底层调用的是valueOd方法
4. 其他包装类的用法类似

```
package com.cwz.wrapper;  
  
/**  
 * @author 陈文臻  
 */  
public class Integer01 {  
    public static void main(String[] args) {  
        //演示int <---> Integer 的装箱和拆箱  
        //jdk5前是手动装箱和拆箱  
        //手动装箱  
        int n1 = 100;  
        Integer integer = new Integer(n1);  
        Integer integer1 = Integer.valueOf(n1);  
        //手动拆箱  
        //Integer->int  
        int i = integer.intValue();  
  
        //jdk5后，就可自动装箱和拆箱  
        int n2 = 200;  
        //自动装箱 int->Integer        
        Integer integer2 = n2;//底层使用的是 Integer.valueOf(n2)        
        //自动拆箱 Integer->int        
        int n3 = integer2;//底层仍然使用的是 inValue()方法  
    }  
}
```

### 8.1.3 包装类型和String类型的相互转换

```
public class WrapperVSString {  
    public static void main(String[] args) {  
        //包装类(Integer)->String  
        Integer i =100;//自动装箱  
        //方式1  
        String Str1 = i + "";  
        //方式2  
        String str2 = i.toString();  
        //方式3  
        String str3 = String.valueOf(i);  
        //String  -> 包装类(Integer)  
        String str4 = "12345";  
        Integer i2 = Integer.parseInt(str4);//使用到自动装箱  
        Integer i3 = new Integer(str4);//构造器  
    }  
}
```

### 8.1.4 Integer类和Character类的常用方法

|   |   |
|---|---|
|方法|作用|
|Integar.MIN_VALUE|返回最小值|
|Integer.MAX_VALUE|返回最大值|
|Character.isDigit('a')|判断是不是数字|
|Charactet.isLetter('a')|判断是不是字母|
|Character.isUpperCase('a')|判断是不是大写|
|Character.isLowerCase('a')|判断是不是小写|
|Character.isWhitespace('a')|判断是不是空格|
|Character.toUpperCase('a')|转成大写|
|Character.toLowerCase('A')|转成小写|

## 8.2 String类

### 8.2.1 String类的理解和创建对象

1. String对象用于保存字符串，也就是一组字符序列
2. 字符串常量对象是用双引号括起的字符序列。例如"你好"、"12.97"、"boy"等
3. 字符串的字符使用Unicode字符编码，一个字符(不区分字母还是汉字)占两个字节
4. String类较常用构造方法(其他手册):

- String s1 = new String();
- String s2 = new String(String original);
- String s3 = new String(char[] a);
- String s4 = new String(char[] a, int startlndex, int count);

```
package com.cwz.string;  
  
/**  
 * @author 陈文臻  
 */  
public class String01 {  
    public static void main(String[] args) {  
        //1.String 对象用于保存字符串，也就是一组字符序列  
        //2."jack"字符串常量，双引号括起的字符串序列  
        //3.字符串的字符使用Unicode字符编码，一个字符(不区分分母还是汉字)占两个字节  
        //4。String类有很多构造器，构造器的重载  
        //5.String类实现了接口 Serializable【String可以串行化:可以在网络传输】  
        //                   Comparable 【String 对象可以比较大小】  
        //6.String是一个final，不能被其他类继承  
        //7.String有属性 private final char value[];用于存在字符串内容  
        //8.一定要注意：value是一个final类型，赋值后就不可修改(地址)：  
        //  即value不能指向新地址，但是单个字符内容是可以改变的  
        String name = "jack";  
        name = "tom";  
        final char value[] = {'a', 'b', 'c'};  
        char[] v2 = {'t', 'o', 'w'};  
        value[0] = 'H';  
        //value = v2;  
        //无法将值赋给 final 变量 'value'    }  
}
```

### 8.2.1 创建String对象的两种方式

#### 8.2.1.1方式一

**直接赋值String s = "cwz";**

- 先从常量池查看是否有"cwz"数据空间，如果有，直接指向
- 如果没有则重新创建，然后指向
- s最终指向的是常量池的空间地址

#### 8.2.1.2方式二

**调用构造器String s = new String("cwz");**

- 先在堆中创建空间，里面维护了value属性，指向常量池的"cwz"空间。
- 如果常量没有”cwz“，重新创建
- 如果有，直接通过value指向
- 最终指向的是堆中的空间地址

```
String a = "cwz";
```

解析：`a 指向 常量池的 "cwz"`

```
String b = mew String("cwz");
```

解析：`b指向堆中的对象`

```
System.out.println(a.equals(b));
```

解析：`T`

```
System.out.println(a==b);
```

解析:`F`

### 8.2.2 字符串的特性

1. String是一个final类，代表不可变的字符序列
2. 字符串是不可变的，一个字符串对象一旦被分配，其内容是不可变的

小结：底层是 StringBuilder sb = new StringBuilder();  sb.append(a);  sb.append(b);  sb是在堆中，并且append是在原来字符串的基础上追加的。  
**重要规则：String c1 = "ab" + "cd";常量相加，看到是池。 String c1 = a + b；变量相加，在堆中**

```
String s1 = "hello";
s1 = "haha";
```

问：该语句创建了几个对象?

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712026944103-00e7ff2b-29fb-4744-9fb7-a6075457c018.png)  
答：创建了两个对象

```
String a = "hello" + "abc";
//String a = "hello" + "abc";==>优化等价于String a = "helloabc"
```

问：创建了几个对象？  
答：只有一个对象

```
String a = "hello";
String b = "abc";
String c = a + b;
```

问：创建了几个对象  
答：3个

第一行：创建a对象  
第二行：创建b对象  
第三行：

- 先创建一个 StringBuilder sb = StringBuilder()
- 执行   sb.append("hello")；
- 执行   sb.append("abc");
- 再调用 sb.toString 方法
- 最后其实是 c 指向堆中的对象(String) value[ ] -> 池中"helloabc"

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712026955142-be706a0b-2277-41c5-8ae4-1799fee90bb6.png)

### 8.2.3 String的常见方法

String类是保存字符串常量的。每次更新都需要重新开辟空间，效率极低，因此java设计者还提供了StringBuilder和StringBuffer来增强String的功能，并提高效率

|   |   |
|---|---|
|方法|作用|
|equals|区分大小写，判断内容是否相等|
|equalslgnoreCase|忽略大小写的判断内容是否相等|
|length|获取字符的个数，字符串的长度|
|indexOf|获取字符在字符串中第1次出现的索引，索引从0开始，如果找不到，返回-1|
|lastIndexOf|获取字符在字符串中最后1次出现的索引，索引从0开始，如果找不到，返回-1|
|substring|截取指定范围的子串|
|trim|去前后空格|
|charAt|获取某索引处的字符，注意不能使用Str[index]这种方法|
|toUpperCase|转换成大写|
|toLowerCase|转化成小写|
|concat|拼接字符串|
|replace|替换字符串中的字符|
|split|分割字符串|
|toCharArray|转换成字符数组|
|compareTo|比较两个字符串的大小|
|format|格式化字符串|

```
package com.cwz.string;  
  
import java.util.Locale;  
  
/**  
 * @author 陈文臻  
 */  
public class StringMethod01 {  
    public static void main(String[] args) {  
        //1.equals,比较内容是否相同，区分大小写  
        String str1 = "hello";  
        String str2 = "HELLO";  
        System.out.println(str1.equals(str2));  
  
        //2.equalsIgnoreCase 忽略大小写的判断内容是否相等  
        String username = "JOSN";  
        if ("john".equalsIgnoreCase(username)){  
            System.out.println("Success");  
        }else {  
            System.out.println("Failure");  
        }  
  
        //3.length 获取字符串的个数，字符串的长度  
        System.out.println("cwz".length());  
  
        //4.indexOf 获取字符在字符串对象中第一次出现的索引，所以从0开始，如果找不到，返回-1  
        String s1 = "wer@terwe@g";  
        int index = s1.indexOf('@');  
        System.out.println(index);  
        System.out.println(s1.indexOf("we"));  
  
        //5.lastIndexOf 获取字符在字符串中最后1次出现的索引，索引从0开始，如果找不到，返回-1  
        String s2 = "wer@terwe@g";  
        int index1 = s2.indexOf('@');  
        System.out.println(index);  
        System.out.println(s1.lastIndexOf("we"));  
  
        //6.substring 截取指定范围的子串  
        String name = "hello,张三";  
        //下面name.substring(6) 从索引6开始截取后面所有的内容  
        System.out.println(name.substring(6));//截取后面的字符  
        //name.substring(0,5)表示从索引0开始截取，截取到索引 (5-1)的位置  
        System.out.println(name.substring(0,5));  
  
        //7.toUpperCase 转换成大写  
        String s = "hello";  
        System.out.println(s.toUpperCase());//Hello  
  
        //8.toLowerCase 转换成小写  
        String s3 = "HELLO";  
        System.out.println(s3.toLowerCase());  
  
        //9.concat 拼接字符串  
        String s4= "宝玉";  
        s4 = s4.concat("林黛玉").concat("薛宝钗").concat("together");  
        //输出结果：宝玉林黛玉薛宝钗together  
        System.out.println(s4);  
  
        //10.replace 替换字符串中的字符  
        String s5 = "宝玉 and 薛宝钗 薛宝钗 薛宝钗";  
        //在s5中将 所有的薛宝钗内容替换成林黛玉  
        //s5.replace() 方法执行后，返回的结果才是替换过的  
        //注意本身对s5没有影响  
        s5 = s5.replace("薛宝钗", "林黛玉");  
        System.out.println(s5);  
  
        //11.split 分割字符串，对于某些分割字符串，我们需要 转义 比如 | \\等  
        String poem = "锄禾日当午，汗滴禾下土，谁知盘中餐，粒粒皆辛苦";  
        //解读：  
        //1.以逗号为标准，对poem进行分割，返回一个数组  
        //2.在对字符串进行分割时，如果有特殊字符，需要加入转义符  
        String[] split = poem.split(",");  
        poem = "E:\\aaa\\bbb";  
        split = poem.split("\\\\");  
        System.out.println("==分割后内容==");  
        for (int i = 0; i < split.length; i++) {  
            System.out.println(split[i]);  
        }  
  
        //12.toCharArray 转换成字符数组  
        s = "happy";  
        char[] chs = s.toCharArray();  
        for (int i = 0; i < chs.length; i++) {  
            System.out.println(chs[i]);  
        }  
  
        //13.compareTo  比较两个字符串的大小  
        //  如果前者大，就返回正数  
        //  如果后者大，就返回负数  
        //  如果相等，就返回零  
        //1.如果长度相同，并且每个字符也相同，就返回0  
        //2.如果长度相同/不相同，但进行比较时，可以区分大小  
        //      就返回 if(c1 != c2){        //                  return c1 - c2;        //                }        //3.如果前面的部分都相同，就返回第一个字符串的长度 - 第二个字符串的长度  
        String a = "john";  
        String b = "jack";  
        System.out.println(a.compareTo(b));//返回值是'c'-'a'=2的值  
  
        //14，format 格式化字符串  
        //占位符有：  
        //%s 字符串 %c 字符 %d 整型 %.2f 浮点型  
        String name1 = "john";  
        int age = 10;  
        double score = 98.3/3;  
        char gender = '男';  
        //将所有的信息都拼接在一个字符串  
        String info =  
                "我的姓名是" + name + "年龄是" + age + "成绩是" + score + "性别是" + gender;  
        System.out.println(info);  
  
        //1. %s %d %c %f称为占位符  
        //2.这些占位符由后面的变量来替换  
        //3.%s 字符串 %c 字符 %d 整型 %.2f 浮点型(保留两位小数)  
        String info2 = String.format("我的性别是%s 年龄是%d 成绩是%.2f 性别是%c", name, age, score, gender);  
  
        System.out.println("info2=" + info2);  
        }  
}
```

## 8.3 StringBuffer类

- java.lang.StringBuffer 代表可变的字符序列，可以对字符串内容进行增删
- 很多方法与String相同，但是StringBuffer是可变长度的
- StringBuffer是一个容器

### 8.3.1 String vs StringBuffer

- String保存的是字符串常量，里面的值不能更改，每次String类的更新实际上就是更改地址，效率极低  根本原因==>private final char value[];
- StringBuffer保存的是字符串变量，里面的值可以更改，每次StringBuffer的更新实际上可以更新内容，不用每次更新地址(空间内存不够)，效率极高//char[] value 这个放在堆

### 8.3.2 StringBuffer的构造器

|   |   |
|---|---|
|方法|作用|
|StringBuffer|构造一个其中不带字符的字符串缓冲区，其初始容量为16个字符|
|StringBuffer(CharSequence seq)|构造一个字符串缓冲区，它包含与指定的CharSequence相同的字符|
|StringBuffer(int capacity)|构造一个不带字符，但是指定初始容量的字符串缓冲区，即对char[]大小进行指定|
|StringBuffer(String str)|构造一个字符串缓冲区，并将其内容初始化为指定的字符串内容|

```
public class StringBuffer02 {  
    public static void main(String[] args) {  
  
        //构造器使用  
        //1.创建一个大小为16的char[],用于存放字符序列  
        StringBuffer stringBuffer = new StringBuffer();  
        //2.通过构造器指定char数组的大小  
        StringBuffer stringBuffer1 = new StringBuffer(100);  
        //3.通过给给一个String创建StringBuffer  
        //char数组的大小就是字符串的大小+16  
        StringBuffer stringBuffer3 = new StringBuffer("hello");  
    }  
}
```

### 8.3.3 StringBuffer和String之间的相互转换

#### 8.3.3.1 String ---> StringBuffer

- 使用构造器  
    `StringBuffer stringBuffer = new StringBuffer(str);`
- 使用append方法  
    `stringBuffer = stringBuffer.append(str);`

#### 8.3.3.2 StringBuffer ---> String

- 使用StringBuffer提供的toString方法  
    `String s = stringBuffer.toString();`
- 使用构造器来搞定  
    `String s1 = new String(stringBuffer);`

```
public class StringAndStringBuffer {  
    public static void main(String[] args) {  
        //String--->StringBuffer  
        String str = "hello tom";  
        //方式1：使用构造器  
        //注意：返回的才是StringBuffer对象，对str没有影响  
        StringBuffer stringBuffer = new StringBuffer(str);  
        //方式2 使用append方法  
        StringBuffer stringBuffer1 = new StringBuffer();  
        stringBuffer1 = stringBuffer.append(str);  
        //StringBuffer--->String  
        StringBuffer stringBuffer3 = new StringBuffer("cwz");  
        //方法1；使用StringBuffer提供的toString方法  
        String s = stringBuffer3.toString();  
        //方法2：使用构造器来搞定  
        String s1 = new String(stringBuffer3);  
    }  
}
```

### 8.3.4 StringBuffer类常见方法

1. 增 append
2. 删 delete(start,end)
3. 改 replace(start,end,string)//将start---end间的内容替换掉，不含end
4. 查 indexOf //查找子串在字符串第一次出现的索引，如果找不到返回-1
5. 插 insert
6. 获取长度 length

```
public class StringBufferMethod {  
    public static void main(String[] args) {  
  
        StringBuffer s = new StringBuffer("hello");  
        //增  
        s.append(',');  
        s.append("张三丰");  
        s.append("赵敏").append(100).append(true).append(10.5);  
        System.out.println(s);  
        //hello,张三丰赵敏100true10.5  
  
        //删  
        /**  
         * 删除索引 >=start && <end 处的字符  
         * 解读:删除 11~14的字符 [11,14)  
         */        s.delete(11,14);  
        System.out.println(s);  
        //hello,张三丰赵敏true10.5  
  
        //改  
        //替换 使用 大傻逼 替换9-11的字符 [9,11)        s.replace(9,11,"大傻逼");  
        System.out.println(s);  
        //hello,张三丰大傻逼true10.5  
  
        //查找指定的子串第一次出现的索引，如果找不到返回-1  
        int indexOf = s.indexOf("张三丰");  
        System.out.println(indexOf);//6  
  
        //插  
        //在索引为9的位置插入"赵敏",原来索引为9的内容自动后移  
        s.insert(9,"赵敏");  
        System.out.println(s);  
        //hello,张三丰赵敏大傻逼true10.5  
    }  
}
```

## 8.4 StringBuilder

### 8.4.1 基本介绍

- 一个可变的字符序列。(此类提供一个与StringBuffer兼容的API,但不保证同步(StringBuffer不是线程安全的 存在多线程问题)。该类被设计用作StringBuffer的一个简单易替，==用在字符串缓冲区被单个线程使用的时候==。如果可能，建议优先采用该类，因为大多数实现中，它比StringBuffer要快)
- 在StringBuilder上的主要操作是append和insert方法，可重载这些方法，来接受任意类型的数据

```
public class StringBuilder01 {  
    public static void main(String[] args) {  
        //1.StringBuilder 继承 AbstractStringBuilder 类  
        //2.实现了 Serializable ，说明StringBuilder对象是可以串行化(对象可以网络传输，可以保存到文件)  
        //3.StringBuilder是final类，不能被继承  
        //4.StringBuilder 对象字符序列仍然是存在在其父类 AbstractStringBuilder的char[] value;  
        //  因此，字符序列是堆中  
        //5.StringBuilder的方法，没有做互斥的处理
        //即没有synchronized关键字，因此在单线程的情况下使用 StringBuilder        
        StringBuilder stringBuilder = new StringBuilder();  
    }  
}
```

### 8.4.2 String vs StringBuffer vs StringBuilder

1. StringBuilder 和 StringBuilder 非常类似，均代表可变的字符序列，而且方法也一样
2. String:不可变字符序列，效率低，但是重复率高
3. StringBuffer:可变字符序列，效率较高(增删)、线程安全
4. StringBuilder：可变字符序列，效率最高、线程不安全
5. String使用注意说明：  
    String s = "a"; //创建了一个字符串  
    s += "b";//实际上原来的"a"字符串对象已经丢弃了，现在又产生了一个字符串s + "b"(也就是"ab").如果多次执行这些改变串内容的操作，会导致大量副本字符对象存留在内存当中，降低效率。如果这样的操作放在循环中，会极大影响程序的性能=> ==结论：如果我们对String做大量修改，不要使用String==
6. 效率：StringBuilder > StringBuffer > String

**使用的原则**

1. 如果字符串存在大量的修改操作，一般使用StringBuffer或StringBuilder
2. 如果字符串存在大量的修改操作，并在单线程的情况，使用StringBuilder
3. 如果字符串存在大量的修改操作，并在多线程的情况，使用StringBuffer
4. 如果我们字符串很少修改，被多个对象引用，使用String，比如配置信息等

## 8.5 Math

### 8.5.1 基本介绍

Math类包含执行基本的数学运算方法，如初等数学、对数、平方根和三角函数

### 8.5.2 常用的方法

1. abs 绝对值
2. pow 求幂
3. ceil 向上取整
4. floor 向下取整
5. round 四舍五入
6. sqrt 求开方
7. random 求随机数
8. max 求两个数的最大值
9. min 求两个数的最小值

```
public class MathMethod {  
    public static void main(String[] args) {  
        //1.abs 绝对值  
        int abs = Math.abs(-9);  
        System.out.println(abs);  
        //2,pow 求幂  
        double pow = Math.pow(2,4);//2的4次方  
        System.out.println(pow);  
        //3.ceil 向上取整 返回 >= 该参数的最小整数  
        double ceil = Math.ceil(-3.00001);  
        System.out.println(ceil);//-3.0  
        //4.floor 向下取整 返回 <= 该参数的最大整数  
        double floor = Math.floor(-4.999);  
        System.out.println(floor);//-5.0  
        //5.round 四舍五入 Math.floor(该参数 + 0.5)        long round = Math.round(-5.001);  
        System.out.println(round);  
        //6.sqrt 求开方  
        double sqrt = Math.sqrt(9.0);  
        System.out.println(sqrt);  
        //7.random 求随机数  
        //  random 返回的是0 <= x < 1之间的一个随机小数  
        //  返回一个数 x  2 <= x <= 7        //公式： (int)(a + Math.random() * (b - a +1))        for (int i = 0; i < 10; i++) {  
            System.out.println((int)(2 + Math.random() * (7 -2 + 1)));  
        }  
    }  
}
```

## 8.6 Arrays类

### 8.6.1 常见方法应用案例

- toString 返回数组的字符串形式  
    Arrays.toString(arr)

```
Integer[] integers = {1, 20, 90};  
//遍历数组（以前)  
for (int i = 0; i < integers.length; i++) {  
    System.out.print(integers[i] + " ");  
}  
  
//直接使用Array.toString方法，显示数组  
System.out.println(Arrays.toString(integers));
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712026972500-368c2aa8-ae35-4808-b613-bc4cc0450dbe.png)

- sort 排序(自然排序和定制排序)     Integer arr[] = {1, -1, 7, 0, 89};

```
//演示 sort 方法使用  
  
Integer arr[] = {1, -1, 7, 0, 89};  
//进行排序  
//1.可以直接使用冒泡排序，也可以直接使用Arrays提供的sort方法排序  
//2.因为数组是引用类型，所以通过sort排序后，会直接影响到实参 arr//3.sort重载的，可以通过传入一个接口 Comparator 实现定制排序  
//4.调用定制排序时，传入两个参数(1)排序的数组 arr//  (2)实现了Comparator接口的匿名内部类，要求实现 compare方法  
//5.先演示效果，再解释  
//6.这里体现了接口编程的方式  
  
  
  
Arrays.sort(arr);//默认排序方法  
Arrays.sort(arr, new Comparator() {  
    @Override  
    public int compare(Object o1, Object o2) {  
        Integer i1 = (Integer) o1;  
        Integer i2 = (Integer) o2;  
        return i2 - i1;  
    }  
});  
System.out.println("===排序后===");  
System.out.println(Arrays.toString(arr));
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712026986942-25d9e345-3216-47b0-8694-8a7c28d2f9f3.png)

- binarySearch 通过二分搜索法进行查找，要求必须排好序  
    int index = Arrays.binarySearch(arr, 3);

```
Integer[] arr1 = {1, 2, 90, 123, 567};  
//binarySearch 通过二分搜索法进行查找，要求必须排好  
//1.使用binarySearch 二叉查找  
//2.要求该数组时有序的，如果数组是无序的，不能使用binarySearch  
//3.如果数组中不存在该元素，就返回 -(low+1)int index = Arrays.binarySearch(arr1,568);  
int index2 = Arrays.binarySearch(arr1,2);  
System.out.println("index= " + index);  
System.out.println("index2= " + index2);
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712026995788-20f9ba2f-a563-46ea-93e3-081f9a5a66f5.png)

- copyOf 数组元素的复制  
    Integer[] newArr = Arrays.copyOf(arr, arr.length);

```
//copyOf 数组元素的复制  
//1.从 arr 数组中，拷贝arr.length个元素到 newArr数组中  
//2.如果拷贝的长度 > arr.length 就在新数组的后面 增加 null//3.如果拷贝长度小于0，就发生拷贝异常  
Integer[] newArr = Arrays.copyOf(arr,arr.length);  
Integer[] newArr1 = Arrays.copyOf(arr,arr.length - 1);  
Integer[] newArr2 = Arrays.copyOf(arr,arr.length + 1);  
System.out.println("==拷贝执行完毕后==");  
System.out.println(Arrays.toString(newArr));  
System.out.println(Arrays.toString(newArr1));  
System.out.println(Arrays.toString(newArr2));
```

- fill 数组元素的填充  
    Integer[] num = new Integer[]{9,3,2};  
    Arrays.fill(num, 99);

```
//fill 数组填充的方法  
//1.使用99去填充，可以理解成替换掉所有元素  
Integer[] num = new Integer[]{9,3,2};  
Arrays.fill(num,99);  
System.out.println("==num数组填充后==");  
System.out.println(Arrays.toString(num));
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027004057-2c15e74a-3061-4ff3-9b3f-a83c0bbec5b6.png)

- equals 比较两个数组元素内容是否一致  
    boolean equals = Arrays.equals(arr, arr2);

```
//equals 比较两个数组元素是否完全一致  
Integer[] arr2 = {1,2,90,123};  
//1.如果arr3和arr4数组的元素一样，则返回true  
//2.如果不是完全一样就返回false  
boolean equals = Arrays.equals(arr,arr2);  
System.out.println("equals= " + equals);
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027027162-e37893ec-66a8-480f-bc7b-07611993f95a.png)

- asList 将一组值，转换成list

```
//asList将一组值，转换成list  
//1.asList方法，会将(2,3,4,5,6,1)数据转成一个List集合  
//2.返回 asList 编译类型 List(接口)  
//3.asList 运行类型 class java.util.Arrays$ArrayList,是Arrayss类的  
List<Integer> asList = Arrays.asList(2,3,4,5,6,1);  
System.out.println("asList=" + asList);  
System.out.println("asList的运行类型" + asList.getClass());
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027021515-9a93230d-b4c0-4765-973b-f2ba57ae42b4.png)

## 8.7 System类

- exit 退出当前程序

```
public class System_ {  
    public static void main(String[] args) {  
  
        //exit 退出当前程序  
  
        System.out.println("hello  world !!");  
        //1.exit(0) 表示程序退出  
        //2.0 表示一个状态，正常状态  
        System.exit(0);  
        System.out.println("ok2");  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027033978-2aef78ed-d9a0-4a51-94fd-990138eeab91.png)

- arraycopy：复制数组元素，比较适合底层调用，一般使用Arrays.copyOf完成复制数组

```
public class System01 {  
    public static void main(String[] args) {  
        int[] src={1,2,3};  
        int[] dest = new int[3];//dest 当前是 {0,0,0}                
        //1.主要是搞清楚这五个参数的含义  
        //  src            源数组  
        //  srcPos         从源数组的哪个索引位置开始拷贝  
        //  dest           目标数组，即把源数组的数据拷贝到哪个数组  
        //  destPos        把源数组的数据拷贝到目标数组的哪个索引  
        //  length         从源数组拷贝多少个数据到目标数组  
        System.arraycopy(src, 0 , dest, 0 , src.length);  
  
        System.out.println("dest= " + Arrays.toString(dest));  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027043566-78440e06-1985-40fc-a117-a215bf426c5e.png)

- currentTimeMillens:返回当前时间距离1970-1-1的毫秒数

```
//currentTimeMillens:返回当前时间距离1970-1-1的毫秒数  
System.out.println(System.currentTimeMillis());
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027050560-1454c9a4-e5af-4cce-985b-71db099a4da8.png)

- gc:运行垃圾回收机制 System.gc();

## 8.8 BigInteger 和 BigDecimal类

### 8.8.1 应用场景

1. BigInteger适合保存比较大的整型
2. BigDecimal适合保存精度更高的浮点型(小数)

### 8.8.2 BigInteger 和 BigDecimal 常见方法

1. add 加
2. subtract 键
3. multiply 乘
4. divide 除

#### 8.8.2.1 BigInteger

```
public class BigInteger {  
    public static void main(String[] args) {  
  
        //当我们编程中，需要处理很大的整数，long就不够用了  
        //可以使用BigInteger的类来搞定  
        long l = 238282223;  
        System.out.println("l=" + l);  
  
        java.math.BigInteger bigInteger = new java.math.BigInteger("213721878137121");  
        java.math.BigInteger bigInteger1 = new java.math.BigInteger("100");  
        System.out.println(bigInteger);  
        //1.在对 BigInteger 进行加减乘除的时候，需要使用对用的方法，不能直接进行 + - * /        //2.可以创建一个要操作的BigInteger 然后进行操作  
        java.math.BigInteger add = bigInteger.add(bigInteger1);  
        System.out.println(add);//加  
        java.math.BigInteger subtract = bigInteger.subtract(bigInteger1);  
        System.out.println(subtract);//减  
        java.math.BigInteger multiply = bigInteger.multiply(bigInteger1);  
        System.out.println(multiply);//乘  
        java.math.BigInteger divide = bigInteger.divide(bigInteger1);  
        System.out.println(divide);//除  
        }  
}
```

#### 8.8.2.2 BigDecimal

```
public class BigDecimal {  
    public static void main(String[] args) {  
        //当我们需要保存一个精度很高的数时，double 不够用  
        //可以是BigDecimal  
        double d = 1999.11111111;  
        System.out.println(d);  
        java.math.BigDecimal bigDecimal = new java.math.BigDecimal("128.8364286464918791841");  
        java.math.BigDecimal bigDecimal1 = new java.math.BigDecimal("1.1");  
        System.out.println(bigDecimal);  
        //1.如果BigDecimal进行运算，比如加减乘除，需要使用对应的方法  
        //2.创建一个需要操作的BigDecimal然后调用方法即可  
        System.out.println(bigDecimal.add(bigDecimal1));  
        System.out.println(bigDecimal.subtract(bigDecimal1));  
        System.out.println(bigDecimal.multiply(bigDecimal1));  
        System.out.println(bigDecimal.divide(bigDecimal1));//可能抛出异常ArithmeticException  
        //在调用divide方法时，指定精度即可 BigDecimal.ROUND_CEILING        //如果有无线循环小数，就会保留分子精度  
        System.out.println(bigDecimal.divide(bigDecimal1, java.math.BigDecimal.ROUND_CEILING));  
        }  
}
```

## 8.9 日期类

### 8.9.1 第一代日期类

1. Date：精确到毫秒，代表特定时间
2. SimpleDateFormat：格式和解析日期的类 SimpleDateFormat格式化和解析日期的具体类。它允许进行格式化 (日期 -> 文本) 、解析(文本->日期) 和 规范化

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027059695-e78a73c8-faaf-40a7-a634-30c079eb7a8a.png)

```
package com.cwz.date;  
  
import java.text.ParseException;  
import java.text.SimpleDateFormat;  
import java.util.Date;  
  
/**  
 * @author 陈文臻  
 */  
public class Date01 {  
    public static void main(String[] args) throws ParseException {  
  
        Date d1 = new Date();//获取当前的系统时间  
        System.out.println("当前日期=" + d1);//默认输出的日期时国外的方式  
        //因此需要对格斯进行转换  
        //1.创建 SimpleDateFormat对象，可以指定相应的格式  
        //2.这里的格式使用的字母是规定好的，不能乱写  
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 hh:mm:ss E");  
        String format = sdf.format(d1); //format：将日期转换成指定格式的字符串  
        System.out.println("当前的日期是：" + format);  
  
        Date d2 = new Date(9234567);//通过指定毫秒数得到时间  
        System.out.println("d2= " + d2);  
        System.out.println(d1.getTime());//获取某个时间对应的毫秒数  
  
        //1.可以把一个格式化的字符串转成对应的date  
        //2.得到的date仍然在输出时，还是按照国外的形式，如果希望指定格式输出，需要转化  
        //3.在把一个 String --》 Date ，使用的 sdf 格式需要和你给的String格式一样，否则会抛出异常  
        String s = "1996年01月01日 10:20:30 星期一";  
        Date parse = sdf.parse(s);  
        System.out.println("parse=" + parse);  
        System.out.println("parse=" + sdf.format(parse));  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027066688-a8cbf80a-aeb3-4b86-b3b1-f3fb90f0651a.png)

### 8.9.2 第二代日期类

1. 第二代日期类，主要就是Calendar类(日历)
2. Calendar类就是一个抽象类，它为特定瞬间与一组诸如YEAR、MONTH、DAY_OF_MONTH、HOUR等日历、字段之间的转换提供了一些方法，并为操作日历字段(例如获得下星期的日期)提供了一些方法

```
package com.cwz.date;  
  
/**  
 * @author 陈文臻  
 */  
public class Calendar {  
    public static void main(String[] args) {  
        //1.Calendar是一个抽象类，并且构造器是private  
        //2.可以通过 getInteger() 来获取实例  
        //3.提供大量的方法和字段提供给程序员  
        //4.没有提供对应的格式化的类，需要程序员自己组合  
        //5.如果我们需要按照24小时进制来获取时间
        //Calendar.HOUR ==> 改成 Calendar.HOUR_OF_DATE
        java.util.Calendar c = java.util.Calendar.getInstance();  
        //创建日历类对象  
        System.out.println(c);  
  
        //获取日历对象的某个字段  
        System.out.println("年：" + c.get(java.util.Calendar.YEAR));  
        //这里为什么要 + 1，因为Calendar返回月时候，是按照 0 开始编号  
        System.out.println("月：" + (c.get(java.util.Calendar.MONTH) + 1));  
        System.out.println("日：" + c.get(java.util.Calendar.DAY_OF_MONTH));  
        System.out.println("小时：" + c.get(java.util.Calendar.HOUR));  
        System.out.println("分钟：" + c.get(java.util.Calendar.MINUTE));  
        System.out.println("秒：" + c.get(java.util.Calendar.SECOND));  
        //Calendar 没有专门的格式化方法，所以需要程序员自己来组合显示  
        System.out.println(c.get(java.util.Calendar.YEAR) + "年" 
        + (c.get(java.util.Calendar.MONTH) + 1) + "月" 
        + c.get(java.util.Calendar.DAY_OF_MONTH) + "日" 
        + c.get(java.util.Calendar.HOUR) + "小时" 
        + c.get(java.util.Calendar.MINUTE) + "分钟" 
		+ c.get(java.util.Calendar.SECOND) + "秒");  
  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027077230-a96dfb50-05d5-4682-bb8a-04333cfe3b4b.png)

Calendar不足分析：

- 可变性：像日期和时间这样的类应该时不可变的
- 偏移性：Date中的年份是从1900开始的，而月份是从0开始的
- 格式化：格式化只对Date有用，Calendar不行
- 此外，他们也不是线程安全的；不能处理闰秒(每隔2天，多出1s)

### 8.9.3 第三代日期类

1. LocalDate(日期/年月日)
2. LocalTime(时间/时分秒)
3. LoaclDateTime(日期时间/年月日时分秒)  
    ==jdk8加入==

```
package com.cwz.date;  
  
import java.time.Instant;  
import java.time.LocalDateTime;  
import java.time.format.DateTimeFormatter;  
import java.util.Date;  
  
/**  
 * @author 陈文臻  
 */  
public class LocalDate {  
    public static void main(String[] args) {  
        //第三代日期  
        //1，使用now()返回当前日期时间的对象  
        LocalDateTime ldt = LocalDateTime.now();  
        System.out.println(ldt);  
        System.out.println("年=" + ldt.getYear());  
        System.out.println("月=" + ldt.getMonthValue());  
        System.out.println("月=" + ldt.getMonth());  
        System.out.println("日=" + ldt.getDayOfMonth());  
        System.out.println("时=" + ldt.getHour());  
        System.out.println("分=" + ldt.getMinute());  
        System.out.println("秒=" + ldt.getSecond());  
  
        //2.使用DateTimeFormat对象来进行格式化  
        //创建 DateTimeFormat对象  
        DateTimeFormatter dtf = DateTimeFormatter.ofPattern("yyyy年MM月dd日 HH小时mm分钟ss秒");  
        String format = dtf.format(ldt);  
        System.out.println("格式化的日期" + format);  
        //3.时间戳  
        //(1)通过静态方法 now() 获取表示当前时间戳的对象  
        Instant now = Instant.now();  
        System.out.println(now);  
        //(2)通过from方法可以把Instant转成Date  
        Date date = Date.from(now);  
        //(3)通过date的toInstance()可以把date转成Instance方法  
        Instant instant = date.toInstant();  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027084568-61d59aa4-87b2-4ab9-8553-26f8b0f168bb.png)

# 9. 集合

## 9.1 基本介绍

1. 可以==动态保存==任意多个对象，使用比较方便
2. 提供了一系列方便的操作对象的方法: add、remove、set、get等
3. 使用集合添加，删除新元素的示意代码-简介了

## 9.2 集合框架体系

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027091190-00ad241a-2d87-48c4-8187-0ad8ac0c8ca9.png)

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027099462-cf081f9b-21aa-4267-98c0-7c77a13de98b.png)

```
package com.cwz.collection;  
  
import java.util.ArrayList;  
import java.util.HashMap;  
  
/**  
 * @author 陈文臻  
 */  
@SuppressWarnings({"all"})  
public class Collection {  
    public static void main(String[] args) {  
        //1.集合主要是两组(单列集合，双列集合)  
        //2.Collection 接口有两个重要的子接口 List Set, 他们的实现子类都是单列集合  
        //3.Map 接口的实现子类 是双列集合，存放的是kv  
        //把老师梳理的两张图记住  
        //Collection  
        //Map  
        //单列集合  
        ArrayList arrayList = new ArrayList();  
        arrayList.add("jack");  
        arrayList.add("tom");  
  
        //双列集合  
        HashMap hashMap = new HashMap();  
        hashMap.put("NO1","北京");  
        hashMap.put("NO2","北京");  
  
    }  
}
```

## 9.3 Collection接口

### 9.3.1 Collection接口实现类的特点

1. collection实现子类可以存放多个元素，每个元素可以是Object
2. 有些Collection的实现类，可以存放重复的元素，有些不可以
3. 有些Collection的实现类，有些是有序的(List)，有些不是有序的(Set)
4. Collection接口没有直接的实现子类，是通过它的子接口Set和List来实现的

### 9.3.2 Collection接口的常用方法

|   |   |
|---|---|
|方法|作用|
|add|添加单个元素|
|remove|删除指定元素|
|contains|查找元素是否存在|
|size|获取元素个数|
|isEmpty|判断是否为空|
|clear|清空|
|addAll|添加多个元素|
|containsAll|查找多个元素是否都存在|
|removeAll|删除多个元素|

```
package com.cwz.collection;  
  
import java.util.ArrayList;  
import java.util.List;  
  
/**  
 * @author 陈文臻  
 */  
public class CollectionMethod {  
    @SuppressWarnings("all")  
    public static void main(String[] args) {  
  
        List list = new ArrayList();  
  
        //1. add:添加单个元素  
        list.add("jack");  
        list.add(100);//list.add(new Integer(10))  
        list.add(true);  
        System.out.println("list=" + list);  
  
        //2. remove:删除指定元素  
        list.remove(0);//删除第一个元素  
        list.remove("jack");//指定删除某个元素  
        System.out.println("list=" + list);  
  
        //3. contains:查找元素是否存在  
        System.out.println(list.contains("jack"));//T  
                //4. size:获取元素个数  
        System.out.println(list.size());  
        //5. isEmpty:判断是否为空  
        System.out.println(list.isEmpty());  
  
        //6. clear:清空  
        list.clear();  
        //7. addAll:添加多个元素  
        List list2 = new ArrayList();  
        list2.add("红楼梦");  
        list2.add("三国演义");  
        list.addAll(list2);  
        System.out.println("list=" + list);  
  
        //8. containsAll:查找多个元素是否都存在  
        System.out.println(list.contains(list2));  
        //9. removeAll:删除多个元素  
        list.removeAll(list2);  
        }  
}
```

### 9.3.3 Collection 接口遍历元素方式

#### 9.3.3.1 方式一：使用Iterator(迭代器)

1. Iterator对象称为迭代器，主要用于遍历Collection集合中的元素
2. 所以实现了Collection接口的集合类都有一个iterator()方法，用以返回一个实现了Iterator接口的对象，即可以返回一个迭代器
3. Iterator的结构
4. Iterator仅用于遍历集合，Iterator本身不存放对象

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027117261-a194edbd-573a-48ea-a01a-4dbba833e9e0.png)

```
package com.cwz.collection;  
  
  
import java.util.ArrayList;  
import java.util.Collection;  
import java.util.Iterator;  
  
/**  
 * @author 陈文臻  
 */  
public class CollectionIterator {  
    @SuppressWarnings("all")  
    public static void main(String[] args) {  
  
        Collection col = new ArrayList();  
  
        col.add(new Book("三国演义","罗贯中",10.1));  
        col.add(new Book("小李飞刀","古龙",5.1));  
        col.add(new Book("红楼梦","曹雪芹",34.6));  
  
        System.out.println("col=" + col);  
        //现在希望能够遍历集合  
        //1.先得到 col 对应的迭代器  
        Iterator iterator = col.iterator();  
        //2.使用while循环遍历  
        while(iterator.hasNext()){//判断是否还有数据  
            //返回下一个元素，类型是Object  
            Object obj = iterator.next();  
            System.out.println("obj= " + obj);  
        }  
        //快捷键itit  
        //显示所有快捷键 ctrl + j  
        //3.当退出while循环后，这时iterator迭代器，指向最后的元素  
        //iterator.next();//NoSuchElmentException  
        //如果需要再次遍历，需要重置迭代器  
        iterator = col.iterator();  
        System.out.println("第二次遍历");  
        while (iterator.hasNext()) {  
            Object obj = iterator.next();  
            System.out.println("obj=" + obj);  
        }  
    }  
}  
  
class Book{  
    private String name;  
    private String author;  
    private double price;  
  
    public Book(String name, String author, double price) {  
        this.name = name;  
        this.author = author;  
        this.price = price;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public String getAuthor() {  
        return author;  
    }  
  
    public void setAuthor(String author) {  
        this.author = author;  
    }  
  
    public double getPrice() {  
        return price;  
    }  
  
    public void setPrice(double price) {  
        this.price = price;  
    }  
  
    @Override  
    public String toString() {  
        return "Book{" +  
                "name='" + name + '\'' +  
                ", author='" + author + '\'' +  
                ", price=" + price +  
                '}';  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027174283-7010a5a6-3ccc-4cb2-91bc-1d6cf6874210.png)

#### 9.3.3.2 方式二：增强for循环

增强for循环，可以代替iterator迭代器  
**特点**：增强for就是简化版的iterator，本质一样。只能用于遍历集合或数组

**基本语法**

```
for(元素类型 元素名：集合名或数组名){
		访问元素
}
```

```
package com.cwz.collection;  
  
import java.util.ArrayList;  
import java.util.Collection;  
  
/**  
 * @author 陈文臻  
 */  
public class CollectionFor {  
    @SuppressWarnings("all")  
    public static void main(String[] args) {  
        Collection col = new ArrayList();  
  
        col.add(new Book("三国演义", "罗贯中", 10.1));  
        col.add(new Book("小李飞刀", "古龙", 5.1));  
        col.add(new Book("红楼梦", "曹雪芹", 34.6));  
  
        //使用增强for循环  
        //for循环的底层仍然是iterator迭代器  
        //增强for可以理解为简化版的迭代器  
        //快捷方式 I        
        for (Object book : col) {  
            System.out.println("book= " + book);  
        }  
//        //增强for也可以直接在数组上使用  
//        int[] nums = {1, 8, 10, 90};  
//        for(int i : nums){  
//            System.out.println("nums= " + nums);  
//        }  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027186657-d58e268d-fc67-4a65-8e2a-0f6bf462a945.png)

### 9.3.4 List接口和常用方法

#### 9.3.4.1 基本介绍

List接口是Collection接口的子接口

1. List集合类中元素有序(即添加顺序和取出顺序一致)、且可重复
2. List集合类中的每个元素都有其对应的顺序索引，即支持索引
3. List容器中的元素都对应一个整数型的序号记载其在容器中的位置，可以根据序号存取容器中的元素
4. JDK API中List接口的实现类常用的有

- ArrayList
- LinkedList
- Vector

```
public class List {  
    @SuppressWarnings("all")  
    public static void main(String[] args) {  
        //1.List集合类中元素有序(即添加顺序和取出顺序一致)、且可重复  
        java.util.List list = new ArrayList();  
        list.add("jack");  
        list.add("tom");  
        list.add("marry");  
        list.add("tom");  
        System.out.println("list=" + list);  
        //2. List集合类中的每个元素都有其对应的顺序索引，即支持索引  
        //   索引是从0开始的  
        System.out.println(list.get(3));  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027194641-88ae848b-5cf9-408c-b977-4544a6f0a3f6.png)

### 9.3.5 List接口的常用方法

List集合里添加了一些根据索引来操作集合元素的方法

|   |   |
|---|---|
|方法|作用|
|void add(int index, Object ele)|在index位置插入ele元素|
|boolean addAll(int index, Collection eles)|从index位置开始将eles中的所有元素添加进来|
|Object get(int index)|获取指定index位置的元素|
|int indexOf(Object obj)|返回obj在当前集合中首次出现的位置|
|int lastIndexOf(Object ob)|返回obj在当前集合末次出现的位置|
|Object remove(int index)|移除指定index位置的元素为ele,相当于是替换|
|Object set(int index, Object ele)|设置指定index位置的元素为ele, 相当于是替换|
|List subList(int fromIndex, int toIndex)|返回从fromIndex到toIndex位置的子集合|

```
package com.cwz.List;  
  
import com.sun.org.apache.xpath.internal.operations.Lt;  
  
import java.util.ArrayList;  
import java.util.List;  
  
/**  
 * @author 陈文臻  
 */  
public class ListMethod {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
  
        List list = new ArrayList();  
        list.add("张三丰");  
        list.add("贾宝玉");  
        //1. void add(int index, Object ele): 在index位置插入ele元素  
        //在索引等于1的位置加入一个对象  
        list.add(1,"张飞");  
        //2. boolean addAll(int index, Collection eles): 从index位置开始将eles中的所有元素添加进来  
        List list2 = new ArrayList();  
        list2.add("jack");  
        list2.add("tom");  
        list.addAll(1,list2);  
        //3. Object get(int index): 获取指定index位置的元素  
        //4. int indexOf(Object obj): 返回obj在当前集合中首次出现的位置  
        System.out.println(list.indexOf("tom"));  
        //5. int lastIndexOf(Object ob): 返回obj在当前集合末次出现的位置  
        System.out.println(list.indexOf("tom"));  
        //6. Object remove(int index): 移除指定index位置的元素为ele,相当于是替换  
        list.remove(0);  
        //7. Object set(int index, Object ele): 设置指定index位置的元素为ele, 相当于是替换  
        list.set(1,"marry");  
        //8. List subList(int fromIndex, int toIndex): 返回从fromIndex到toIndex位置的子集合  
        //注意返回的子集合 fromIndex <= index < toIndex        List returnlist = list.subList(0,2);  
        System.out.println("returnlit= " + returnlist);  
    }  
}
```

#### 9.3.5.1 List的三种遍历方式

[ArrayList  LinkedList  Vector]

```
package com.cwz.List;  
  
import java.util.ArrayList;  
import java.util.Iterator;  
import java.util.List;  
  
/**  
 * @author 陈文臻  
 */  
public class ListFor {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
  
        //List 接口的实现子类 Vector LinkedList        List list = new ArrayList();  
        //List list = new Vector();  
        //List list = new LinkedList();        list.add("jack");  
        list.add("tom");  
        list.add("鱼香肉丝");  
        list.add("北京烤鸭");  
  
        //遍历  
        //1.迭代器  
        Iterator iterator = list.iterator();  
        while (iterator.hasNext()) {  
            Object obj = iterator.next();  
            System.out.println(obj);  
        }  
  
        System.out.println("===增强for===");  
        //2.增强for  
        for (Object o : list) {  
            System.out.println("o" + o);  
        }  
  
        System.out.println("===普通类===");  
        //3.使用普通for循环  
        for (int i = 0; i < list.size(); i++) {  
            System.out.println("对象=" + list.get(i));  
        }  
  
    }  
}
```

#### 9.3.5.2 ArrayList

##### 9.3.5.2.1 ArrayList的注意事项

1. Permits all elements,including null,ArrayList 可以加入null，并且多个
2. ArrayList是由数组来实现数据存储的
3. ArrayList基本等同与Vector，除了ArrayList是线程不安全(执行效率高)看源码，在多线程情况下不建议使用ArrayList

##### 9.3.5.2.2 ArrayList的底层操作机制源码分析

1. ArrayList中维护了一个Object类型的数组elementData
2. 当创建ArrayList对象时，如果使用的是无参构造器，则初始elementData容量为0，第1次添加，则扩容elementData为10，如需再次扩容，则扩容elementData为1.5倍
3. 如果使用的是指定大小的构造器，则初始elementData容量为指定大小，如果需要扩容，则直接扩容elementData为1.5倍

#### 9.3.5.3 Vector

##### 9.3.5.3.1 基本介绍

- Vector类的定义说明

```
public class Vector<E>
extends AbstractList<E>
implements List<E>, RandomAccess, Cloneable, Serializable
```

- Vector底层也是一个对象数组，protected Object[] elementData;
- Vector是线程同步的，即线程安全，Vector类的操作方法由synchronized

```
public synchronized E get(get index)
	if(inedx >= elementCount)
		throw new ArrayIndexOutOfBoundException(index);
	return elementData(index);
```

- 在开发中，需要同步安全时，考虑使用Vector

##### 9.3.5.3.2 Vector和ArrayList比较

|   |   |   |   |   |
|---|---|---|---|---|
||底层结构|版本|线程安全(同步)效率|扩容倍数|
|ArrayList|可变数组|jkd1.2|不安全，效率高|如果有参数构造1.5倍   如果是无参构造，第一次是10，第二次开始时按1.5倍扩|
|Vector|可变数组|jdk1.0|安全，效率不高|如果是无参，默认10，满后，就按2倍扩容。如果指定大小，则每次直接按2倍扩|

```
package com.cwz.List;  
  
/**  
 * @author 陈文臻  
 */  
  
@SuppressWarnings({"all"})  
public class Vector {  
    public static void main(String[] args) {  
        //无参构造器  
        //1.new Vector() 底层  
        /*  
            public vector() {            
	            this(10);            
            }            
            补充:如果是  vector vector = new Vector(8);                
	            走的方法:  
                public Vector(int initialCapacity){ 
                    this(initalCapacity, 0);                
                }  
                
        2. //vector.add(i)        
        2.1 //下面这个方法就添加数据到vector集合  
  
            public synchronized boolean add(E e) {                
	            modCount++;                
	            ensureCapacityHelper(elementCount + 1);  
	            elementData[elementCount++] = e;                
	            return true;            
	            }
	              
        2.2 //确定是否需要扩容 条件 ： minCapacity - elementData.length > 0   
	        private void ensureCapacityHelper(int minCapacity){              
		          //overflow - conscious code                
		          if(minCapacity - elementData.length > 0)       
			          grow(minCapacity);            
		    }
	              
        2.3 //如果 需要的数组大小 不能用，就扩容， 扩容的算法  
            //newCapacity = oldCapacity + ((capacityIncrement > 0)?     
            //                              capacityIncrement : oldCapacity);            
            //就是扩容的两边  
            private void grow(int minCapacity) {                
            // overflow - conscious code                
            int oldCapacity = elementData.lenth;                
            int newCapacity = oldCapacity + ((capacityIncrement > 0) ?       
                                         capacityIncrement : oldCapacity); 
            if (newCapacity - minCapacity < 0)                    
            newCapacity = minCapacity;                
            if (newCapacity - Max_ARRAY_SIZE > 0)                    
            newCapacity = hugeCapacity(minCapacity);                 
            elementData = Arrays.copyOf(elementData, newCapacity);           
            }        */        
            
        java.util.Vector vector = new java.util.Vector();  
         for (int i = 0; i < 10; i++) {  
            vector.add(i);  
        }  
    }  
}
```

#### 9.3.5.4 LinkedList

##### 9.3.5.4.1 LinkedList的全面说明

1. LinkedList实现了双向链表和双端队列特点
2. 可以添加任意元素(元素可以重复)，包括null
3. 线程不安全，没有实现同步

##### 9.3.5.4.2 LinkedList的底层操作机制

1. LinkedList底层维护了一个双向链表
2. LinkedList中维护了两个属性first和last分别指向首节和尾节点
3. 每个节点(Node对象), 里面又维护了prev、next、ltem三个属性，其中通过prev指向前一个，通过next指向后一个节点。最终实现双向链表
4. 所有LinkedList的元素的==添加和删除==，不是通过数组完成的，相对来说效率较高(改变对象的指向)
5. 模拟一个简单的双向链表

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027244347-0540f945-c95b-43d2-af42-eb0e571f407b.png)

```
package com.cwz.List;  
  
/**  
 * @author 陈文臻  
 */  
public class LinkList01 {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
        //模拟一个简答的双向链表  
  
        Node jack = new Node("jack");  
        Node tom = new Node("tom");  
        Node cwz = new Node("cwz");  
  
        //连接三个结点，形成双向链表  
        //jack -> tom -> cwz  
        jack.next = tom;  
        tom.next = cwz;  
        //cwz -> tom -> jack  
        cwz.pre = tom;  
        tom.pre = jack;  
  
        Node first = jack;//让first引用指向jack，就是双向链表的头结点  
        Node last = cwz;//让last引用指向cwz，就是双向链表的尾结点  
  
        //演示从头到尾进行遍历  
        System.out.println("==从头到尾遍历==");  
        while(true){  
            if(first == null){  
                break;  
            }  
            //输出first信息  
            System.out.println(first);  
            first = first.next;  
        }  
        //演示从尾到头的遍历  
        System.out.println("==从尾到头遍历==");  
        while(true){  
            if(last == null){  
                break;  
            }  
            //输出last信息  
            System.out.println(last);  
            last = last.pre;  
        }  
        //演示链表添加对象/数据  
        //要求在tom和cwz之间插入一个对象 smith                //1.先创建一个Node结点，名字就是smith  
        Node smith = new Node("smith");  
        //下面就把 smith 加入到双向链表了  
        smith.next = cwz;  
        smith.pre = tom;  
        cwz.pre = smith;  
        tom.next = smith;  
        //让first再次指向第一个人：jack  
        first = jack;//让first引用指向jack，就是双向链表的头结点  
        //演示从头到尾进行遍历  
        System.out.println("==从头到尾遍历==");  
        while(true){  
            if(first == null){  
                break;  
            }  
            //输出first信息  
            System.out.println(first);  
            first = first.next;  
        }  
  
    }  
}  
  
//定义一个Node类，Node 对象 表示双向链表的一个结点  
class Node{  
    public Object item;//真正存放数据的地方  
    public Node next;//指向后一个结点  
    public Node pre;//指向前一个结点  
    public Node(Object name){  
        this.item = name;  
    }  
    public String toString(){  
        return "Node name=" + item;  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027262627-8c583294-1bff-419e-8fef-169b389adff7.png)

##### 9.3.5.4.3 LinkedList底层结构

```
package com.cwz.List;  
  
import java.util.Iterator;  
import java.util.LinkedList;  
  
/**  
 * @author 陈文臻  
 */  
@SuppressWarnings({"all"})  
public class LinkedListCRUD {  
    public static void main(String[] args) {  
  
        LinkedList linkedList = new LinkedList();  
        linkedList.add(1);  
        linkedList.add(2);  
        linkedList.add(3);  
  
        System.out.println("LinkedList= " + linkedList);  
  
        //演示删除结点的源码  
        linkedList.remove(); //这里默认删除第一个结点  
        //LinkedList.remove(2);  
  
        System.out.println("LinkedList= " + linkedList);  
        //修改某个结点对象  
        linkedList.set(1,999);  
        System.out.println("LinkedList= " + linkedList);  
        //得到某个结点对象  
        Object o = linkedList.get(1);  
        System.out.println("o= " + o);  
        //因为LinkedList是实现了List接口，遍历方式  
        System.out.println("==LinkedList遍历迭代器==");  
        Iterator iterator = linkedList.iterator();  
        while (iterator.hasNext()) {  
            Object next = iterator.next();  
            System.out.println("next=" + next);  
        }  
  
        System.out.println("==LinkedList遍历增强for==");  
        for (Object o1 :linkedList) {  
            System.out.println("o1= " + o1);  
        }  
  
        System.out.println("==LinkedList遍历普通for==");  
        for (int i = 0; i < linkedList.size(); i++) {  
            System.out.println(linkedList.get(i));  
        }  
  
  
        //这里是添加的源码  
        /*  
            1.LinkedList linkedList = new LinkedList();  
            public LinkedList(){}          
            2.这时 linkedList的属性 first = null   last = null          
            3.执行  
              public boolean add(E e){                    
	              linkLast(e);                    
	              return true;              
              }          
            4.将新的结点，加入到双向链表的最后  
              void linkedLast(E e){                    
	              final Node<E> l = last;                    
	              final Node<E> newnode = newNode<>(l, e, null);              
                  last = newNode;                    
                  if(l = null)                        
					first = newNode;                    
				  else                        
					l.next = newNode;                    
				  size++;                    
				  modCount++;               
				}  
         */                
         
         //这里是删除的源码  
        /*  
            linkedList.remove(); //这里默认删除第一个结点  
            1. 执行 removeFirst       
            public E remove(){                 
	            return removeFirst();               
            }  
            2. 执行  
               public E removeFirst(){                   
	               final Node<E> f = first;                   
	               if (f = null)                       
		               throw new NoSuchElementException();                   
	               return unlinkFirst(f);                
               }             
            3. 执行 unlinkFirst,将f指向的双向链表的第一个结点拿掉  
                private = E unlinkFirst(Node<E> f){                    
	                // assert f = first && f != null;                    
	                final E element = f.item;                    
	                final Node<E> next = f.next;                    
	                f.item = null;                    
	                f.next = null; // help GC                    
	                first = next;                    
	                if (next == null)                        
		                last = null;                    
	                else                        
		                next.prev = null;                    
	                size--;                    
	                modCount++;                    
	                return element;                
                }         
                */    }  
}
```

##### 9.3.5.4.4 ArrayList 和 LinkedList比较

|   |   |   |   |
|---|---|---|---|
||底层结构|增删的效率|改查的效率|
|ArrayList|可变数组|较低  数组扩容|较高|
|LinkedList|双向链表|较高  通过链表追加|较低|

如何选择ArrayList和LinkedList：

1. 如果我们改查的操作多，选择ArrayList
2. 如果我们增删的操作多，选择LinkedList
3. 一般来说，在程序中，80%-90%都是查询，因此大部分情况下会选择ArrayList
4. 在一个项目中，根据业务灵活选择，也可能这样，一个模块使用的ArrayList，另外一个模块是LinkedList

### 9.3.6 Set接口

#### 9.3.6.1 基本介绍

1. 无序(添加和取出的顺序不一致)，没有索引
2. 不允许重复元素，索引最多包含一个null

#### 9.3.6.2 Set接口的常用方法

和List接口一样，Set接口也是Collection的子接口，因此，常用方法和Collection接口一样

#### 9.3.6.3 Set接口遍历方式

同Collection的遍历方式一样，因为Set接口是Collection接口的子接口

1. 可以使用迭代器
2. 增强for
3. ==不能使用==索引的方式来获取

```
package com.cwz.Set;  
  
import java.util.HashSet;  
import java.util.Iterator;  
import java.util.Set;  
  
/**  
 * @author 陈文臻  
 */  
public class SetMethod {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
        //1.以Set接口的实现类 HashSet来讲解Set接口  
        //2.set接口的实现类的对象(Set接口对象),不能存放重复的元素，可以添加一个null  
        //3.sert接口对象存放数据是无序的(即添加顺序和取出顺序不一致)  
        //4.注意:取出的顺序虽然不是添加的顺序，但是他是固定的  
  
        Set set = new HashSet();  
        set.add("john");  
        set.add("lucy");  
        set.add("jack");  
        set.add(null);  
  
        System.out.println("set=" + set);  
        //遍历方式1：使用迭代器  
        System.out.println("==使用迭代器==");  
        Iterator iterator = set.iterator();  
        while (iterator.hasNext()) {  
            Object obj = iterator.next();  
            System.out.println("obj=" + obj);  
        }  
        //遍历方式2：增强for循环  
        System.out.println("==增强for循环==");  
        for (Object o : set) {  
            System.out.println("o" + o);  
        }  
    }  
}
```

#### 9.3.6.4 HashSet

##### 9.3.6.4.1 HashSet的全面说明

1. HashSet实现了Set接口
2. HashSet实际上是HashMap

```
public HashSet(){
	map = new HashMap<>();
}
```

3. 可以存放null值，但是只能由一个null
4. HashSet不保证元素是有序的，取决于hash后，在确定索引的结果(即不保证元素存放的顺序和取出顺序一致)
5. 不能由重复元素/对象，在前面Set接口使用已经讲过

```
package com.cwz.set;  
  
import java.util.Set;  
  
/**  
 * @author 陈文臻  
 */  
@SuppressWarnings({"all"})  
public class HashSet {  
    public static void main(String[] args) {  
        //1.构造器走的源码  
        /*  
            public HashSet(){                map = new HashMap<>();            }          2.HashSet 可以存放空，但最多只能放一个空  
         */        Set hashSet = new java.util.HashSet();  
        hashSet.add(null);  
        System.out.println("hashSet" + hashSet);  
    }  
}
```

##### 9.3.6.4.2 HashSet底层机制说明

```
package com.cwz.set;  
  
/**  
 * @author 陈文臻  
 */  
public class HashSetStruct {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
        //模拟一个HashSet的底层(HashMap的底层结构）  
  
        //1.创建一个数组，数组的类型是 Node[]        //2.有些人，直接把 Node[] 数组称为表  
        Node[] table = new Node[16];  
        System.out.println("table= " + table);  
        //3.创建结点  
        Node john = new Node("john", null);  
  
        table[2] = john;  
        Node jack = new Node("jack", null);  
        john.next = jack;// 将jack挂在到john  
        Node rose = new Node("Rose", null);  
        jack.next = rose;// 将rose结点挂在到jack  
        System.out.println("table= " + table);  
        //在索引为2的位置形成链表  
  
        Node luck = new Node("luck", null);  
        table[3] = luck;//把luck放在table表索引为3的位置  
    }  
}  
  
class Node{//结点，存储数据，可以指向下一个结点，从而形成链表  
    Object item; //存放数据  
    Node next; //指向下一个结点  
  
    public Node(Object item, Node next) {  
        this.item = item;  
        this.next = next;  
    }  
}
```

1. HashSet底层是HashMap
2. 添加一个元素时，先得到hash值 -> 会转成 -> 索引值
3. 找到存储数据表table，看这个索引位置是否已经存放的元素
4. 如果没有，直接加入
5. 如果有，调用equals比较，如果相同，就放弃添加，如果不相同，则添加到最后
6. 在Java8中，如果一条链表的元素个数到达TREEIFY_THRESHOLD(默认是8)，并且table的大小 >= MIN_TREEIFY_CAPACITY(默认64),就会进行树化(红黑树)

```
package com.cwz.set;  
  
import java.util.HashSet;  
import java.util.Objects;  
  
/**  
 * @author 陈文臻  
 */  
public class HashSetExercise {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
        /**  
         * 定义一个Employee类，该类包含private成员属性name,age 要求:  
         * 创建3个Employee 对象放入 HashSet  
         * 当 name和age的值相同时，认为是相同员工，不能添加到HashSet集合中  
  
         */  
        HashSet hashSet = new HashSet();  
        hashSet.add(new Employee("milan",18));//ok  
        hashSet.add(new Employee("smith",28));//ok  
        hashSet.add(new Employee("milan",18));//加入不成功  
  
        //加入几个？3个  
        System.out.println("hashSet= " + hashSet );  
    }  
}  
  
//创建Employee对象  
class Employee{  
    private String name;  
    private int age;  
  
    public Employee(String name, int age) {  
        this.name = name;  
        this.age = age;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public int getAge() {  
        return age;  
    }  
  
    public void setAge(int age) {  
        this.age = age;  
    }  
  
    //如果name和age值相同，则返回相同的hash值  
    @Override  
    public boolean equals(Object o) {  
        if (this == o) return true;  
        if (o == null || getClass() != o.getClass()) return false;  
        Employee employee = (Employee) o;  
        return age == employee.age && Objects.equals(name, employee.name);  
    }  
  
    @Override  
    public int hashCode() {  
        return Objects.hash(name, age);  
    }  
}
```

##### 9.3.6.3 LinkedHashSet

###### 9.3.6.1 LinkedHashSet的全面说明

1. LinkedHashSet是HashSet的子类
2. LinkedHashSet底层是一个LinkedHashMap，底层维护了一个数组 + 双向链表
3. LinkedHashSet根据元素的hashCode值来决定元素的存储位置，同时使用链表维护元素的==次序==，这使得元素看起来是以插入顺序保存的
4. LinkedHashSet不允许重复添加元素  
    ![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027279657-46bc4569-b714-471d-9998-858ef64349b3.png)

说明：

- 在LinkedHashSet中维护了一个hash表和双向链表( LinkedHashSet 有 head 和 tail)
- 每一个结点有 before 和 after属性，这样可以形成双向链表
- 在添加一个元素时，先求hash值，在求索引，确定该元素在table的位置，然后将添加的元素加入到双向链表(如果已经存在，不添加[原则和hashset一样])

```
tail.next = newElement;
newElement.pre = tail;
tail = newElement;
```

- 这样的话，我们遍历LinkedHashSet 也能确保插入顺序和遍历顺序一致

```
package com.cwz.set;  
  
import java.util.LinkedHashMap;  
import java.util.LinkedHashSet;  
import java.util.Set;  
  
/**  
 * @author 陈文臻  
 */  
@SuppressWarnings({"all"})  
public class LinkedHashSetSource {  
    public static void main(String[] args) {  
        //分析一下LinkedHashSet的底层机制  
       Set set = new LinkedHashSet();  
       set.add(new String("AA"));  
       set.add(456);  
       set.add(456);  
       set.add(new Customer("刘",1001));  
       set.add(123);  
       set.add("HSP");  
  
        System.out.println("set= " + set);  
        //1.LinkedHashSet 加入顺序和取出元素/数组的顺序一致  
        //2.LinkedHashSet 底层维护的是一个LinkedHashMap(是HashMap的子类）  
        //3.LinkedHashSet 底层结构(数组 + 双向链表）  
        //4.添加第一次时，直接将table扩容到16, 存放的结点类型是 LinkedHashMap$Entry        //5.数组和是 HashMap$Node[] 存放的数据/元素是 LinkedHashMap$Entry类型  
        /*  
                //继承关系是在内部类完成的  
                static class Entry<k,v> extends HashMap.Node<k,v>{                    Entry<k,V> before, after;                    Entry(int hash, K key, V value, Node<k,v> next){                        super(hash, key, value, next);                    }                }         */  
    }  
}  
  
class Customer{  
    private String name;  
    private int no;  
  
    public Customer(String name, int no) {  
        this.name = name;  
        this.no = no;  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027290681-44358b5e-293f-4140-ab55-65dae85a13e0.png)

```
package com.cwz.set;  
  
import java.util.LinkedHashSet;  
import java.util.Objects;  
  
/**  
 * @author 陈文臻  
 */  
@SuppressWarnings({"all"})  
public class LInkedHashMapExercise {  
    public static void main(String[] args) {  
        LinkedHashSet linkedHashSet = new LinkedHashSet();  
        linkedHashSet.add(new Car("奥拓",1000));  
        linkedHashSet.add(new Car("奥迪",300000));  
        linkedHashSet.add(new Car("法拉利",1000000));  
        linkedHashSet.add(new Car("奥迪",300000));  
        linkedHashSet.add(new Car("保时捷",700000));  
        linkedHashSet.add(new Car("奥迪",300000));  
  
        System.out.println("linkedHashSet= " + linkedHashSet );  
    }  
}  
  
  
/**  
 * Car 类(属性:name,price),  如果 name 和 price一样  
 * 则认为是相同元素，就不能添加  
 */  
class Car{  
    private String name;  
    private double price;  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public double getPrice() {  
        return price;  
    }  
  
    public void setPrice(double price) {  
        this.price = price;  
    }  
  
    public Car(String name, double price) {  
        this.name = name;  
        this.price = price;  
    }  
  
    @Override  
    public String toString() {  
        return "\nCar{" +  
                "name='" + name + '\'' +  
                ", price=" + price +  
                '}';  
    }  
  
    @Override  
    public boolean equals(Object o) {  
        if (this == o) return true;  
        if (o == null || getClass() != o.getClass()) return false;  
        Car car = (Car) o;  
        return Double.compare(car.price, price) == 0 && Objects.equals(name, car.name);  
    }  
  
    @Override  
    public int hashCode() {  
        return Objects.hash(name, price);  
    }  
  
    //重写equals方法和hashCode  
    //当那name和price相同时，就返回相同的hashCode值equals返回t  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027306622-20dcfc66-07bb-458b-a2e8-ae5a2713217d.png)

#### 9.3.6.5 TreeSet

```
package com.cwz.set;  
  
import sun.reflect.generics.tree.Tree;  
  
import java.util.Comparator;  
  
/**  
 * @author 陈文臻  
 */  
public class TreeSet {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
  
        //1.当我们使用无参构造器，创建TreeSet时，仍然是无序的  
        //2.老师希望添加的元素，按照字符串大小排序  
        //3.使用TreeSet 提供的一个构造器，可以传入一个比较器(匿名内部类)  
        //  并指定排序规则  
  
  
        //java.util.TreeSet treeSet = new java.util.TreeSet();  
        java.util.TreeSet treeSet = new java.util.TreeSet(new Comparator() {  
            @Override  
            public int compare(Object o1, Object o2) {  
                //下面调用String的comparaTo方法进行大小比较  
                //return ((String) o1).length - compareTo((String) o2).length;  
                //该规则：长度相等就是相同字符串 所有会缺少元素  
                return ((String) o1).compareTo((String) o2);  
            }  
        });  
  
        treeSet.add("jack");  
        treeSet.add("a");  
        treeSet.add("b");  
        treeSet.add("c");  
  
        /*  
            1.构造器把传入的比较器对象，赋给了 TreeSet的底层的 TreeMap的属性this.comparator  
  
            public TreeMap(Comparator<? super K> comparator){                    this.comparator = comparator;            }  
            2.在调用treeSet.add("tom"), 在底层会执行到  
  
            if(cpr != null){//cpr 就是我们的匿名内部类(对象)  
                do {                    parent = t;                    cmp = cpr.compare(key, t.key);                    //动态绑定到我们的匿名内部类(对象)compare  
                    if (cmp < 0)                        t = t.left;                    else if(cmp > 0)                        t = t.right;                    else //如果相等，即返回0，这个Key就没有加入  
                        return t.setValue(value);                 } while(t != null);             }         */    }  
}
```

## 9.4 Map接口

### 9.4.1 Map接口实现的特点[实用]

注意：这里讲的是JDK8的Map接口特点

1. Map用于保存具有映射关系的数据:Key-Value
2. Map中的Key和Value可以是任何引用类型的数据，会封装到HashMap$Node对象中
3. Map中的key不允许重复，原因和HashMap一样
4. Map中的value可以重复
5. Map的key可以为null，value也可以为null，注意key为null，只能有一个，value为null，可以多个
6. 常用String类作为Map的Key
7. Key和value之间存在单向一对一关系，即通过指定的key总能找到对应的value
8. 接口存放数据的key-value示意图，一对k-v是存放在一个Node中的，又因为Node(HashMap的内部类)实现了Entry接口，有些书也说一对k-v就是一个Entry

```
package com.cwz.Map;  
  
import java.util.HashMap;  
  
/**  
 * @author 陈文臻  
 */  
public class Map {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
        //Map接口实现类的特点  
        //1. Map用于保存具有映射关系的数据:Key-Value(双列元素)  
        //2.Map中的Key和Value可以是任何引用类型的数据，会封装到HashMap$Node对象中  
        //3.Map中的key不允许重复，原因和HashMap一样  
        //4.Map中的value可以重复  
        //5.Map的key可以为null，value也可以为null，注意key为null，只能有一个，value为null，可以多个  
        //6.Key和value之间存在单向一对一关系，即通过指定的key总能找到对应的value  
  
        java.util.Map map = new HashMap();  
        map.put("No1", "cwz");//k-v  
        map.put("No2", "张无忌");//k-v  
        //map.put("No2","张三丰"); 用新的值替换原来的值  
        map.put("No3", "cwz");  
        map.put(null, null);  
        map.put(null, "abc");//等价替换  
  
        System.out.println("map=" + map);  
        //通过get方法传入一个key会返回对应的value  
        System.out.println(map.get("No1"));  
  
    }  
}
```

### 9.3.2 Map体系的继承图

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027135754-1ba216a4-c398-4266-b0cc-366f90628708.png)

### 9.3.3 Map接口常用方法

1. put: 添加
2. remove: 根据键删除映射关系
3. get: 根据键获取值
4. size: 获取元素个数
5. isEmpty: 判断个数是否为0
6. clear: 清除
7. containsKey:查找键是否存在

```
package com.cwz.Map;  
  
  
import java.util.HashMap;  
import java.util.Map;  
  
/**  
 * @author 陈文臻  
 */  
@SuppressWarnings({"all"})  
public class MapMethod {  
    public static void main(String[] args) {  
        //演示Map接口常用方法  
        Map map = new HashMap();  
        map.put("邓超", new Book("", 100));  
        map.put("邓超", "孙俪");//替换  
        map.put("王宝强", "马蓉");  
        map.put("宋喆", "马蓉");  
        map.put("刘令博", null);  
        map.put(null, "刘亦菲");  
        map.put("鹿晗", "关晓彤");  
  
        System.out.println("map=" + map);  
  
        //remove: 根据键删除映射关系  
        map.remove(null);  
        System.out.println("map=" + map);  
  
        //get: 根据键获取值  
        Object val = map.get("鹿晗");  
        System.out.println("val=" + val);  
  
        //size: 获取元素个数  
        System.out.println("k-v=" + map.size());  
  
        //isEmpty: 判断个数是否为0  
        System.out.println(map.isEmpty());  
  
        //clear: 清除  
        map.clear();  
  
        //containsKey:查找键是否存在  
        System.out.println(map.containsKey("hsp"));  
    }  
}  
  
class Book {  
    private String name;  
    private int num;  
  
    public Book(String name, int num) {  
        this.name = name;  
        this.num = num;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public int getNum() {  
        return num;  
    }  
  
    public void setNum(int num) {  
        this.num = num;  
    }  
}
```

### 9.3.4 Map接口遍历方法

1. containsKey： 查找键是否存在
2. keySet： 获取所有的键
3. entrySet： 获取所有关系
4. values：获取所有的值

```
package com.cwz.Map;  
  
import java.util.*;  
import java.util.Map;  
  
/**  
 * @author 陈文臻  
 */  
public class MapFor {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
  
        Map map = new HashMap();  
        map.put("邓超", new Book("", 100));  
        map.put("邓超", "孙俪");//替换  
        map.put("王宝强", "马蓉");  
        map.put("宋喆", "马蓉");  
        map.put("刘令博", null);  
        map.put(null, "刘亦菲");  
        map.put("鹿晗", "关晓彤");  
  
        //第一组:先取出 所有的Key， 通过Key 取出对应的Value  
        Set keyset = map.keySet();  
        //(1)增强for  
        System.out.println("----第一种方式----");  
        for (Object key : keyset) {  
            System.out.println(key + "-" + map.get(key));  
        }  
        //(2)迭代器  
        System.out.println("----第二种方式----");  
        Iterator iterator = keyset.iterator();  
        while (iterator.hasNext()) {  
            Object key = iterator.next();  
            System.out.println(key + "-" + map.get(key));  
        }  
  
        //第二组：把所有value取出  
        Collection values = map.values();  
        //这里可以使用所有的Collections使用的遍历方法  
        System.out.println("---取出所有的value---");  
        //(1)增强for  
        for (Object value : values) {  
            System.out.println(value);  
        }  
  
        //(2)迭代器  
        Iterator iterator1 = values.iterator();  
        while (iterator1.hasNext()) {  
            Object value = iterator1.next();  
            System.out.println(value);  
        }  
  
        //第三组：通过EntrySet 来获取 k-v        Set entrySet = map.entrySet();  
        //(1)增强for  
        for (Object entry : entrySet) {  
            //将entry转成Map.Entry  
            Map.Entry m = (Map.Entry) entry;  
            System.out.println(m.getKey() + "-" + m.getValue());  
        }  
        //(2)迭代器  
        Iterator iterator2 = entrySet.iterator();  
        while (iterator2.hasNext()) {  
            Object entry = iterator2.next();  
            System.out.println(next.getClass());  
            //HashMap$Node -实现-> Map.Entry (getKey,getValue)  
            //向下转型 Map.Enrty            Map.Entry m = (Map.Entry) entry;  
            System.out.println(m.getKey() + "-" + m.getValue());  
        }  
  
  
    }  
}
```

### 9.3.5 HashMap

#### 9.3.5.1 基本介绍

1. Map接口的常用实现类：HashMap、HashTable、Properties
2. HashMap是Map接口使用频率最高的实现类
3. HashMap是以key-val对的方式来储存数据(HashMap$Node)
4. key不能重复，但是值可以重复，允许使用null键和null
5. 如果添加相同的key，则会覆盖原来的key-val，等同于修改(key不会替换，val会替换)
6. 与HashSet一样，不保证映射的顺序，因为底层是以hash表的方式来存储的(jdk8的hashMap底层 数组+链表+红黑数)
7. HashMap没有实现同步，因此是线程不安全的

#### 9.3.5.2 HashMap底层机制及源码剖析

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027229283-32748512-a631-4379-8f7d-38f920d7646a.png)

**扩容机制**

1. HashMap维护了Node类型的数组table，默认为null
2. 当创建对象时，将加载因子初始化为0.75
3. 当添加 key-val 时，通过key的哈希值得到在table的索引。然后判断该索引处是否有元素，如果没有元素直接添加。如果该索引处有元素，继续判断该元素(Node)的key是否和准备加入的key相等，如果相等，则直接替换val；如果不相等需要判断是树状还是链表结构，做出相应处理。如果添加时，发现容量不够，则需要扩容
4. 第1次添加，则需要库容table容量为16，临界值为12
5. 以后再扩容，则需要扩容table容量为原来的2倍，临界值为原来的2倍，即24依此类推
6. 在Java8中，如果需要一条链的元素个数超过 TREEIFY_THRESHOLD(默认是8)，并且table的大小 >= MIN_TREEIFY_CAPACITY(默认64)，就会进行树化(红黑树)

### 9.3.6 HashTable

#### 9.3.6.1 基本介绍

1. 存放的是键值对：即k-v
2. hashtable的键和值都不能为null，否则会抛出NullPointerException
3. hashTable使用方法基本和HashMap一样
4. hashTable是线程安全的，hashMap是线程不安全的

#### 9.3.6.2 Hashtable的扩容

```
//简单说明一下Hashtable的底层
1. 底层有数组 Hashtable$Entry[] 初始化大侠为 11
2. threshold 8 = 11 x 0.75
3. 扩容：按照自己的扩容机制来扩容
4. 执行 方法 addEntry(hash, key, value, index); 添加 K-V 封装到Entry
5. 当 if (count >= threshold) 满足时， 就进行扩容
6. 按照 int newCapacity = (oldCapacity << 1) + 1; 的大小扩容
```

#### 9.3.6.3 Hashtable和HashMap的对比

|   |   |   |   |   |
|---|---|---|---|---|
||版本|线程安全(同步)|效率|允许null键和null值|
|HashMap|1.2|不安全|高|可以|
|Hashtable|1.0|安全|较低|不可以|

#### 9.3.6.4 Properties

##### 9.3.6.4.1 基本介绍

1. Properties类继承自Hashtable类并且实现了Map接口，也是使用一种键值对的形式来保存数据
2. 他的使用特点和Hashtable类似
3. Properties==还可以用==从xxx.properties文件中，加载数据到Properties类对象，并进行读取和修改
4. 说明：工作后 xxx.properties 文件通常作为配置文件，这个知识点在IO流举例

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027329682-a5312b5e-9048-49b6-bca8-550efbfe8b04.png)

```
package com.cwz.Map;  
  
/**  
 * @author 陈文臻  
 */  
public class Properties {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
  
        //1.Properties 继承Hashtable  
        //2.可以通过 k-v 存放数据，当然key和value不能为null  
  
        //增加  
        java.util.Properties properties = new java.util.Properties();  
        //properties.put(null,100);//抛出 空指针异常  
        //properties.put("john",null);//抛出 空指针异常  
        properties.put("john",100);  
        properties.put("lucy",100);  
        properties.put("lic",100);  
        properties.put("lic",88);//如果有相同的key，value被替换  
  
        System.out.println("properties= " + properties);  
  
        //通过k 获取对应值  
        System.out.println(properties.get("lic"));//88  
  
        //删除  
        properties.remove("lic");  
        System.out.println("properties= " + properties);  
  
        //修改  
        properties.put("john","约翰");  
  
    }  
}
```

### 9.3.7 TreeMap

```
package com.cwz.Map;  
  
import java.util.Comparator;  
  
/**  
 * @author 陈文臻  
 */  
public class TreeMap {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
  
        //使用默认的构造器，创建TreeMap, 是无序的(也没有顺序)  
        /*            要求：按照传入的key(String)的大小进行排序  
         */        //java.util.TreeMap treeMap = new java.util.TreeMap();        java.util.TreeMap treeMap = new java.util.TreeMap(new Comparator() {  
            @Override  
            public int compare(Object o1, Object o2) {  
                //按照传入的key(String)的大小进行排序  
                //return ((String) o1).compareTo((String) o2);  
                //按照长度大小排序  
                return ((String) o1).length() - ((String) o2).length();  
            }  
        });  
        treeMap.put("jack", "杰克");  
        treeMap.put("tom", "汤姆");  
        treeMap.put("kristina", "克里斯提诺");  
        treeMap.put("smith", "斯密斯");  
  
        System.out.println("treeMap=" + treeMap);  
  
        /*  
            1. 构造器 把传入的实现了 Comparator 接口的匿名内部类(对象),传给TreeMap的comparator  
            public TreeMap(Comparator<? super K> comparator){                this.comparator = comparator;            }            2. 调用put方法  
            2.1 第一次添加,把k-v封装到Entry对象，放入root  
            Entry<K,V> t = root;            if(t == null){                compare(key,key);// type(and possibly null) check  
                root = new Entry<>(key, value, null);                size = 1;                modCount++;                return null;             2.2 以后添加  
             Comparator<? super K>> cpr = comparator;             if (cpr != null){                do{//遍历所有的key，给当前key找到适当位置  
                    parent = t;                    cmp = cpr.compare(key, t.key);                    //动态绑定到我们的匿名内部类的compara  
                    if(cmp < 0)                        t = t.left;                    else if                        t = t.right;                    else //如果遍历过程中，发现准备添加Key 和当前已有的 Key相等，就不添加  
                        return t.setValue(value);                 } while (t != null);             }         */    }  
}
```

## 总结

### 开发中如何选择集合实现类

`先判断存储的类型(一组对象[单列]或一组键值对[双列])`

**一组对象[单列]：Collection接口**  
允许重复:list  
增删多：LinkedList[底层维护了一个双向链表]  
改查多：ArrayList[底层维护了 Object类型的可变数组]  
不允许重复:Set  
无序：HashSet [底层是HashMap, 维护了一个哈希表 即(数组+链表+红黑树)]  
排序：TreeSet  
插入和取出顺序一致:LinkedHashSet, 维护数组 + 双向链表

**一组键值对[双列]：Map**  
键无序：HashMap[底层是：哈希表 jdk7：数组+链表， jdk8：数组+链表+红黑数]  
键排序：TreeMap  
键插入和取出顺序一致：LinkedHashMap  
读取文件 Properti

## 9.5 Collection工具类

### 9.5.1 基本介绍

1. Collections 是一个操作Set、List和Map等集合的工具类
2. Collections 中提供了一系列静态的方法对集合元素进行排序、查询和修改等操作

### 9.5.2 排序操作(均为static方法)

1. reverse(List): 反转 List 中元素的顺序
2. shuffle(List): 对List集合元素进行随机排序
3. sort(List): 根据元素的自然顺序对指定List集合元素按升序排序
4. sort(List, Comparator): 根据指定的Comparator产生的顺序对List顺序
5. swap(List, int, int): 将指定list集合中的i处和j处元素进行交换

```
package com.cwz.collections;  
  
  
import java.util.ArrayList;  
import java.util.Comparator;  
import java.util.List;  
  
/**  
 * @author 陈文臻  
 */  
public class Collections {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
        //创建ArrayList 集合，用于测试  
        List list = new ArrayList();  
        list.add("tom");  
        list.add("smith");  
        list.add("king");  
        list.add("milan");  
  
        //1. reverse(List): 反转 List 中元素的顺序  
        java.util.Collections.reverse(list);  
        System.out.println("list=" + list);  
  
        //2. shuffle(List): 对List集合元素进行随机排序  
        java.util.Collections.shuffle(list);  
        System.out.println("list=" + list);  
  
        //3. sort(List): 根据元素的自然顺序对指定List集合元素按升序排序  
        java.util.Collections.sort(list);  
        System.out.println("自然排序后");  
        System.out.println("list=" + list);//按字符串大小来排序的  
  
        //4. sort(List, Comparator): 根据指定的Comparator产生的顺序对List顺序  
        java.util.Collections.sort(list, new Comparator<Object>() {  
            @Override  
            public int compare(Object o1, Object o2) {  
                return ((String)o1).length() - ((String)o2).length();  
            }  
        });  
        System.out.println("list=" + list);  
  
        //5. swap(List, int, int): 将指定list集合中的i处和j处元素进行交换  
        java.util.Collections.swap(list,0,1);  
    }  
}
```

### 9.5.3 查找、替换

1. Object max(Collection): 根据元素的自然顺序，返回给定集合中最大的元素
2. Object max(Collection, Comparator): 根据Comparator指定的顺序，返回给定集合中的最大元素
3. Object min(Collection)
4. Object min(Collection, Comparator)
5. int frequency(Collection, Object): 返回指定集合中指定元素的出现次数
6. void copy(List dest, List src): 将src中的内容复制到dest中
7. boolean replaceAll(List list, Object oldVal, Object newVal): 使用新值替换List对象的所有旧值

```
package com.cwz.collections;  
  
import sun.plugin2.gluegen.runtime.CPU;  
  
import java.util.*;  
import java.util.Collections;  
  
/**  
 * @author 陈文臻  
 */  
public class Collections_ {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
        //创建ArrayList 集合，用于测试  
        List list = new ArrayList();  
        list.add("tom");  
        list.add("smith");  
        list.add("king");  
        list.add("milan");  
  
        //1. Object max(Collection): 根据元素的自然顺序，返回给定集合中最大的元素  
        System.out.println("自然顺序的最大元素=" + Collections.max(list));  
  
        //2. Object max(Collection, Comparator): 根据Comparator指定的顺序，返回给定集合中的最大元素  
        //比如要返回长度最大的元素  
        Object maxObject = Collections.max(list, new Comparator<Object>() {  
            @Override  
            public int compare(Object o1, Object o2) {  
                return ((String)o1).length() - ((String)o2).length();  
            }  
        });  
        System.out.println("长度最大的元素=" + maxObject);  
  
        //3. Object min(Collection)  
  
        //4. Object min(Collection, Comparator)  
        //5. int frequency(Collection, Object): 返回指定集合中指定元素的出现次数  
        System.out.println("tom出现的次数=" + Collections.frequency(list,"tom"));  
  
        //6. void copy(List dest, List src): 将src中的内容复制到dest中  
        //为了完成一个完整拷贝，我们需要先给arrayList赋值，大小和list.size()一样  
        ArrayList arrayList = new ArrayList();  
        for (int i = 0; i < list.size(); i++) {  
            arrayList.add("")  
        }  
        Collections.copy(arrayList, list);  
        System.out.println(arrayList);  
  
        //7. boolean replaceAll(List list, Object oldVal, Object newVal): 使用新值替换List对象的所有旧值  
        //如果list有tom就替换成汤姆  
        Collections.replaceAll(list,"tom","汤姆");  
        System.out.println(list);  
    }  
}
```

# 10. 泛型

## 10.1 泛型的引入

### 10.1.1 使用传统方法问题的引入

1. 不能对加入到集合ArrayList中的数据类型进行约束(不安全)
2. 遍历的时候，需要进行类型转换，如果集合中的数据量较大，对效率有影响

```
package com.cwz.generic;  
  
import java.util.ArrayList;  
  
/**  
 * @author 陈文臻  
 */  
public class Generic01 {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
  
        //使用传统的方法来解决  
        ArrayList arrayList = new ArrayList();  
        arrayList.add(new Dog("旺财", 10));  
        arrayList.add(new Dog("发财", 1));  
        arrayList.add(new Dog("小黄", 5));  
  
        //假如我们的程序员不小心加入了一只猫  
        arrayList.add(new Cat("招财猫", 8));  
  
        for (Object o :arrayList) {  
            //向下转型 Object -> Dog            Dog dog = (Dog) o;  
            System.out.println(dog.getName() + "- " + dog.getAge());  
        }  
    }  
}  
  
class Dog{//狗类  
    private String name;  
    private int age;  
  
    public Dog(String name, int age) {  
        this.name = name;  
        this.age = age;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public int getAge() {  
        return age;  
    }  
  
    public void setAge(int age) {  
        this.age = age;  
    }  
}  
  
class Cat{//猫类  
    private String name;  
    private int age;  
  
    public Cat(String name, int age) {  
        this.name = name;  
        this.age = age;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public int getAge() {  
        return age;  
    }  
  
    public void setAge(int age) {  
        this.age = age;  
    }  
}
```

### 10.1.2 泛型好处

1. 编译时，检查添加的元素类型，提高了安全性
2. 减少了类型转换的次数，提高了效率
3. 不再提示编译警告

```
package com.cwz.generic;  
  
import java.util.ArrayList;  
  
/**  
 * @author 陈文臻  
 */  
public class Generic02 {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
  
        //使用传统的方法来解决 ==> 使用泛型  
        //1.当我们 Arraylist<Dog>表示放入ArrayList集合的元素是Dog类型  
        //2.如果编译器发现添加的类型不满足需求，就会报错  
        //3.在遍历的时候，可以直接取出Dog类型 而不是Object类型  
        ArrayList<Dog> arrayList = new ArrayList<Dog>();  
        arrayList.add(new Dog("旺财", 10));  
        arrayList.add(new Dog("发财", 1));  
        arrayList.add(new Dog("小黄", 5));  
        //arrayList.add(new Cat("招财猫", 8 ));  
  
        for (Dog dog : arrayList) {  
            System.out.println(dog.getName() + "-" + dog.getAge());  
        }  
  
    }  
}  
  
  
class Dog {//狗类  
    private String name;  
    private int age;  
  
    public Dog(String name, int age) {  
        this.name = name;  
        this.age = age;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public int getAge() {  
        return age;  
    }  
  
    public void setAge(int age) {  
        this.age = age;  
    }  
}  
  
class Cat {//猫类  
    private String name;  
    private int age;  
  
    public Cat(String name, int age) {  
        this.name = name;  
        this.age = age;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public int getAge() {  
        return age;  
    }  
  
    public void setAge(int age) {  
        this.age = age;  
    }  
}
```

## 10.2 基本介绍

1. 泛型又称参数化类型，是jdk5.0出现的新特性，解决数据类型的安全性问题
2. 再类声明或实例化时只要指定好需要的具体的类型即可
3. Java泛型可以保证如果程序再编译时没有发出警告，运行时就不会产生ClassCastException异常。同时，代码更加简洁、健壮
4. 泛型的作用是：可以在类声明时通过一个标识表示类中某个属性的类型，或者是某个方法的返回值的类型，或者是参数类型。

`泛型是一种可以表示数据类型的数据类型`

```
class Person<E>{
	E s;
	//E表示 s的数据类型，该数据表示在定义Person对象的时候指定,即在编译期间确定E的类型

	public Person(E s){//E也可以是参数类型
		this.s = s;
	}

	public E f(){//返回类型使用E
		return s;
	}
}
```

`PerSon<String> person = new Person<String>("cwz")`  
上面的Person类可以理解为将E -> String

## 10.3 泛型的语法

**泛型的声明  
`interface 接口<T> {}`  
`class 类<K,V>{}`

说明：

- 其中，T，K，V不代表值，而是表示类型
- 任意字母都可以。常用T表示，是Type的缩写

**泛型的实例化:  
要在类名后面指定类型参数的值**

- List<String> strList = new ArrayList<String>();
- Iterator<Customer> iterator = customers.iterator();

```
package com.cwz.generic;  
  
import java.util.*;  
  
/**  
 * @author 陈文臻  
 */  
public class GenericExercise {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
        //使用泛型方式给HashSet放入3个学生对象  
  
        HashSet<Student> students = new HashSet<>();  
        students.add(new Student("jack", 18));  
        students.add(new Student("tom", 19));  
        students.add(new Student("marry", 28));  
  
        //遍历  
        for (Student student : students) {  
            System.out.println(student);  
        }  
        //使用泛型方式给HashMap放入3个学生对象  
        HashMap<String, Student> hm = new HashMap<String, Student>();  
        hm.put("milan", new Student("milan", 18));  
        hm.put("smith", new Student("smith", 19));  
        hm.put("hsp", new Student("hsp", 48));  
  
        //迭代器 EntrySet        
        Set<Map.Entry<String, Student>> entries = hm.entrySet();  
        Iterator<Map.Entry<String, Student>> iterator = entries.iterator();  
        while (iterator.hasNext()) {  
            Map.Entry<String, Student> stu = iterator.next();  
            System.out.println(stu.getKey() + "-" + stu.getValue());  
        }  
    }  
}  
  
/**  
 * 创建 3个学生对象  
 * 放入到HashSet中学生对象使用  
 * 放入到 HashMap中，要求Key是String name, Value 就是学生对象  
 * 使用两种方式遍历  
 */  
  
class Student {  
    private String name;  
    private int age;  
  
    public Student(String name, int age) {  
        this.name = name;  
        this.age = age;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public int getAge() {  
        return age;  
    }  
  
    public void setAge(int age) {  
        this.age = age;  
    }  
  
    @Override  
    public String toString() {  
        return "Student{" +  
                "name='" + name + '\'' +  
                ", age=" + age +  
                '}';  
    }  
}
```

## 10.4 泛型使用的注意事项

1. `interface List<T>{} , public class HashSet<E>{}`..等  
    说明：T E 只能是引用类型
2. 在指定泛型具体类型后，可以传入该类型或其子类类型
3. 泛型使用形式  
    `List<Integer> list1 = new ArrayList<Integer>();`List list2 = new ArrayList<>();`
4. 如果我们这样写 `List list3 = new ArrayList();`默认给它的泛型是[<E> E就是Object]

**课堂练习**

1. 该类包含: private成员变量name, sal, birthday, 其中birthday 为 MyDate类的对象
2. 为每一个属性定义 getter,setter方法
3. 重写toString方法输出name, sal, birthday
4. MyDate类包含:private成员变量month, day, year; 并为每一个属性定义getter, setter方法
5. 创建该类的3个对象，并把这些对象放入ArrayList 集合中(ArrayList需要使用泛型来定义)，对集合中的元素进行排序，并遍历输出:  
    排序方式：调用ArrayList的sort方法，传入Comparator对象[使用泛型]，先按照name排序，如果name相同，则按生日日期的先后排序【即：定制排序】

```
package com.cwz.generic;  
  
import java.util.ArrayList;  
import java.util.Comparator;  
  
/**  
 * @author 陈文臻  
 */  
public class GenericExercise02 {  
    @SuppressWarnings({"all"})  
    public static void main(String[] args) {  
        /**  
         * 1. 该类包含: private成员变量name, sal, birthday, 其中birthday 为 MyDate类的对象  
         * 2. 为每一个属性定义 getter,setter方法  
         * 3. 重写toString方法输出name, sal, birthday  
         * 4. MyDate类包含:private成员变量month, day, year; 并为每一个属性定义getter, setter方法  
         * 5. 创建该类的3个对象，并把这些对象放入ArrayList 集合中(ArrayList需要使用泛型来定义)，对集合中的元素进行排序，并遍历输出:  
         *     排序方式：调用ArrayList的sort方法，传入Comparator对象\[使用泛型]，先按照name排序，如果name相同，则按生日日期的先后排序【即：定制排序】  
         */  
  
        ArrayList<Employee> employees = new ArrayList<>();  
        employees.add(new Employee("tom", 20000, new MyDate(11, 11, 2000)));  
        employees.add(new Employee("jack", 12000, new MyDate(12, 12, 2001)));  
        employees.add(new Employee("cwz", 50000, new MyDate(11, 11, 2002)));  
  
        System.out.println("employees=" + employees);  
        System.out.println("==对员工进行排序==");  
        employees.sort(new Comparator<Employee>() {  
            @Override  
            public int compare(Employee emp1, Employee emp2) {  
                //先按照name排序，如果name相同，则按生日日期的先后排序【定制排序】  
                //先对传入的参数进行验证  
                if(!(emp1 instanceof Employee && emp2 instanceof Employee)){  
                    System.out.println("类型不正确...");  
                    return 0;  
                }  
                //比较name  
                int i = emp1.getName().compareTo(emp2.getName());  
                if (i != 0) {  
                    return i;  
                }  
                //下面对birthday的比较，因此，我们最好把这个比较，放在MyDate类完成  
                return emp1.getBirthday().compareTo(emp2.getBirthday());  
            }  
        });  
  
        System.out.println("==对雇员进行排序==");  
        System.out.println(employees);  
    }  
}  
  
class Employee {  
    private String name;  
    private double sal;  
    private MyDate birthday;  
  
    public Employee(String name, double sal, MyDate birthday) {  
        this.name = name;  
        this.sal = sal;  
        this.birthday = birthday;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public double getSal() {  
        return sal;  
    }  
  
    public void setSal(double sal) {  
        this.sal = sal;  
    }  
  
    public MyDate getBirthday() {  
        return birthday;  
    }  
  
    public void setBirthday(MyDate birthday) {  
        this.birthday = birthday;  
    }  
  
    @Override  
    public String toString() {  
        return "\nEmployee{" +  
                "name='" + name + '\'' +  
                ", sal=" + sal +  
                ", birthday=" + birthday +  
                '}';  
    }  
}  
  
  
class MyDate implements Comparable<MyDate>{  
    private int month;  
    private int day;  
    private int year;  
  
    public MyDate(int month, int day, int year) {  
        this.month = month;  
        this.day = day;  
        this.year = year;  
    }  
  
    public int getMonth() {  
        return month;  
    }  
  
    public void setMonth(int month) {  
        this.month = month;  
    }  
  
    public int getDay() {  
        return day;  
    }  
  
    public void setDay(int day) {  
        this.day = day;  
    }  
  
    public int getYear() {  
        return year;  
    }  
  
    public void setYear(int year) {  
        this.year = year;  
    }  
  
    @Override  
    public String toString() {  
        return "MyDate{" +  
                "month=" + month +  
                ", day=" + day +  
                ", year=" + year +  
                '}';  
    }  
  
    @Override  
    public int compareTo(MyDate o) { //把对year-month-day放在这里  
        //如果name相同，就比较 birthday - year        
        int yearMinus = year - o.getYear();  
        if(yearMinus != 0){  
            return yearMinus;  
        }  
        //如果year相同，就比较month  
        int monthMinus = month - o.getMonth();  
        if(monthMinus != 0){  
            return monthMinus;  
        }  
        //如果month和year都相同  
        return day - o.getDay();  
    }  
}
```

## 10.5 自定义泛型

### 10.5.1 基本语法

```
class 类名<T,R...>{//表示可以有多个泛型
	成员
}
```

```
package com.cwz.customgeneric;  
  
/**  
 * @author 陈文臻  
 */  
public class CustomGeneric {  
    public static void main(String[] args) {  
  
    }}  
  
//1.Tiger 后面泛型，所有我们把 Tiger 就称为自定义泛型类  
//2.T, R, M泛型的标识符，一般是单个大写字母  
//3.泛型标识符可以有多个  
class Tiger<T, R, M>{  
    String name;  
    R r;  
    M m;  
    T t;  
}
```

### 10.5.2 注意细节

1. 普通成员可以使用泛型(属性、方法)
2. 使用泛型的数组，不能初始化`因为数组在new不能确定T的类型，就无法在内存开空间`
3. 静态方法中不能使用类的泛型`因为静态是和类相关的，在类加载时，对象还没有创建,JVM就无法完成初始化`
4. 泛型类的类型，是在创建对象时确定的`因为创建对象时，需要指定确定类型`
5. 如果在创建对象时，没有指定类型，默认为Object

### 10.5.3 自定义泛型接口

#### 10.5.3.1 基本语法

```
inetrface 接口名<T,R...>{

}
```

#### 10.5.3.2 注意细节

1. 接口中，静态成员也不能使用泛型(这个和泛型类规定的一样)
2. 泛型接口的类型，在==继承接口==或者==实现接口==时确定
3. 没有指定类型，默认为Object

```
package com.cwz.generic;  
  
/**  
 * @author 陈文臻  
 */  
public class CustomInterfaceGeneric {  
    public static void main(String[] args) {  
  
    }}  
  
/**  
 *  泛型接口使用的说明  
 *  1. 接口中，静态成员也不能使用泛型(这个和泛型类规定的一样)  
 * 2. 泛型接口的类型，在继承接口或者实现接口时确定  
 * 3. 没有指定类型，默认为Object  
 */  
  
//在继承接口 指定泛型接口的类型  
interface IA extends IUsb<String, Double>{  
  
}  
//当我们去实现IA接口时，因为IA在继承IUsu接口时，指定了U为String R为Double  
//因此，在实现IUsb接口的方法时，使用String替换U，都变了替换R  
class AA implements IA{  
  
    @Override  
    public Double get(String s) {  
        return null;  
    }  
  
    @Override  
    public void hi(Double aDouble) {//自动填充到相应位置  
  
    }  
  
    @Override  
    public void run(Double r1, Double r2, String u1, String u2) {  
  
    }}  
  
//实现接口时，直接指定泛型接口的类型  
//给U指定Integer 给R指定了Float  
//所以，当我们实现IUsb方法时，会用Integer替换U，使用Float替换R  
class BB implements IUsb<Integer, Float>{  
  
    @Override  
    public Float get(Integer integer) {  
        return null;  
    }  
  
    @Override  
    public void hi(Float aFloat) {  
  
    }  
    @Override  
    public void run(Float r1, Float r2, Integer u1, Integer u2) {  
  
    }}  
  
//没有指定类型，默认Object  
//建议直接写成class CC implements IUsb<Object,Object>  
class CC implements IUsb{//等价于class CC implements IUsb<Object,Object>  
    @Override  
    public Object get(Object o) {  
        return null;  
    }  
  
    @Override  
    public void hi(Object o) {  
  
    }  
    @Override  
    public void run(Object r1, Object r2, Object u1, Object u2) {  
  
    }      
}  
interface IUsb<U, R>{  
  
    int n = 10;  
    //U name = "cwz"; 不能这样使用  
  
    //普通方法中，可以使用接口泛型  
    R get(U u);  
  
    void hi(R r);  
  
    void run(R r1, R r2, U u1, U u2);  
  
    //在jdk8中,可以在接口中，使用默认方法  
    default R method(U u){  
        return null;  
    }  
}
```

### 10.5.4 自定义泛型方法

#### 10.5.4.1 基本语法

```
修饰符<T,R...> 返回类型 方法名(参数列表){

}
```

#### 10.5.4.2 注意细节

1. 泛型方法，可以定义在普通类中，也可以定义在泛型类中
2. 当泛型方法被调用时，类型会确定
3. public void eat(E e){ }, 修饰符后没有<T,R...>  
    eat方法不是泛型方法，而是使用了泛型

```
package com.cwz.generic;  
  
import com.cwz.super_.A;  
  
import java.util.ArrayList;  
  
/**  
 * @author 陈文臻  
 */  
@SuppressWarnings({"all"})  
public class CustomMethodGeneric {  
    public static void main(String[] args) {  
        //当泛型方法被调用时，类型会确定  
        Car car = new Car();  
        car.fly("宝马",100);//当调用方法时，传入参数，编译器，就会确定类型  
  
        //测试  
        //T->String R->ArrayList  
        Fish<String, ArrayList> fish = new Fish<>();  
        fish.hello(new ArrayList(),11.3f);  
  
    }  
}  
  
//泛型方法，可以定义在普通类中，也可以定义在泛型类中  
class Car{//普通类  
    public void run(){//普通方法  
  
    }  
    //说明 泛型方法  
    //1.<T, R> 就是泛型  
    //2.是提供给 fly使用的  
    public<T, R> void fly(T t,R r){//泛型方法  
        System.out.println(t.getClass());  
        System.out.println(r.getClass());  
  
    }  
  
}  
  
class Fish<T, R>{//泛型类  
    public void run(){//普通方法  
  
    }  
  
    public<U, M> void eat(U u, M m){//泛型方法  
  
    }  
  
    //说明  
    //1.下面的hi方法不是泛型方法  
    //2.是hi方法使用了类声明的泛型  
    public void hi(T t){  
  
    }    //泛型方法，可以使用类声明的泛型，也可以使用自己声明的泛型  
    public<K> void hello(R r, K k){  
        System.out.println(r.getClass());  
        System.out.println(k.getClass());  
    }  
  
}
```

## 10.6 泛型的继承和通配符

1. 泛型不具备继承性  
    `List<Object> list = new ArrayList<String>();`   错误
2. <?>:支持任意泛型类型
3. <? extends A>:支持A类以及A类的子类，规定了泛型的上限
4. <? super A>:支持A类以及A类的子类，不限于直接父类，规定了泛型的下限

`约束作用`

```
package com.cwz.generic.generic_;  
  
import java.util.ArrayList;  
import java.util.List;  
  
/**  
 * @author 陈文臻  
 */  
public class GenericExtends {  
    public static void main(String[] args) {  
  
        Object o = new String("xx");  
  
        //泛型没有继承性  
        //List<Object> list = new ArrayList<String>();  
  
        //举例说明下面三个方法的使用  
        List<Object> list1 = new ArrayList<>();  
        List<String> list2 = new ArrayList<>();  
        List<AA> list3 = new ArrayList<>();  
        List<BB> list4 = new ArrayList<>();  
        List<CC> list5 = new ArrayList<>();  
  
        //如果是 List<?> c 可以接受任意的泛型类型  
        printCollection1(list1);  
        printCollection1(list2);  
        printCollection1(list3);  
        printCollection1(list4);  
        printCollection1(list5);  
  
        //<? extends A>:支持A类以及A类的子类，规定了泛型的上限  
        //printCollection2(list1);  
        //printCollection2(list2);        printCollection2(list3);  
        printCollection2(list4);  
        printCollection2(list5);  
  
        //<? super A>:支持A类以及A类的子类，不限于直接父类，规定了泛型的下限  
        printCollection3(list1);  
        //printCollection3(list2);  
        printCollection3(list3);  
        //printCollection3(list4);  
        //printCollection3(list5);    }  
  
    //编写几个方法  
    //说明：List<?> 表示任意的泛型类型都可以接受  
    public static void printCollection1(List<?> c){  
        for (Object object : c) {//通配符，取出时，就是Object  
            System.out.println(object);  
        }  
    }  
    //?extends AA 表示上限，可以接受AA或者AA子类  
    public static void printCollection2(List< ? extends AA> c){  
        for (Object object : c) {  
            System.out.println(object);  
        }  
    }  
    //? super 子类名AA:支持AA类以及AA类的父类，不限于直接父类，规定了泛型的下限  
    public static void printCollection3(List<? super AA> c){  
        for (Object object : c) {  
            System.out.println(object);  
        }  
    }  
}  
  
class AA{  
  
}  
  
class BB extends AA{  
  
}  
  
class CC extends BB{  
  
}
```

# 11 多线程基础

## 11.1 基本介绍

- 程序  
    是为完成特定任务，用某种语言编写的一组指令的集合  
    ==简答来说: 就是我们写的代码==
- 进程  
    ==进程是指运行中的程序==，比如说我们使用qq，就启动了一个进程，操作系统就会为该进程分配内存空间。当我们使用迅雷，又启动了一个进程，操作系统将会为迅雷分配新的内存空间

进程是==程序的一次执行进程，或是正在运行的一个程序==。是**动态过程：有它自身的产生、存在和消亡的过程**

- 线程  
    线程是进程创建的，是==进程的一个实体  一个进程可以拥有多个线程
- 单线程  
    ==同一时刻，只允许执行一个线程==
- 多线程  
    ==同一时刻，可以执行多个线程==，比如: 一个qq进程，可以同时打开多个聊天窗口，一个迅雷进程，可以同时下载多个文件
- 并发  
    ==同一时刻，多个任务交替执行==，造成一种"貌似同时"的错觉，简单的说，单核cpu实现的多任务就是并发  
    ![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027346690-6332cd32-1ca6-4535-b8fd-2ab383fda371.png)
- 并行  
    ==同一时刻，多个任务同时执行==。多核cpu可以实现  
    ![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027352683-74513b99-4393-4a0c-b088-dead511a76b3.png)

## 11.2 线程的基本使用

### 11.2.1 创建线程的两种方法

在java中线程来使用有两种方法

- 继承Thread类，重写run方法
- 实现Runnable接口，重写run方法

#### 11.2.1.1 继承Thread类

1. 请编写程序，开启一个线程，该线程每隔1秒。在控制台输出"喵喵，我是小猫咪"
2. 对上题改进: 当输出80次 喵喵，我是小猫咪 结束该线程
3. 使用JConsole监控线程执行情况，并画出程序示意图

```
package com.cwz.threaduse;  
  
/**  
 * @author 陈文臻  
 * 通过继承thread类创建线程  
 */  
public class Thread01 {  
    public static void main(String[] args) {  
  
        //创建Cat对象，可以当作线程使用  
        Cat cat = new Cat();  
        cat.start();//启动线程  
    }  
}  
  
//1.当一个类继承Thread类，该类就可以当线程使用  
//2.我们会重写run方法，写上自己的业务代码  
//3.run Thread 类 实现了 Runnable 接口的run方法  
/*  
    @Override    public void run(){        if (target != null){            target.run();        } */class Cat extends Thread {  
  
    int times = 0;  
    @Override  
    public void run() {//重写run方法，写上自己的业务逻辑  
  
        while(true){  
            //请编写程序，开启一个线程，该线程每隔1秒。在控制台输出"喵喵，我是小猫咪"  
            System.out.println("喵喵，我是小猫咪" + (++times));  
            //让该线程休眠一秒 ctrl+alt+t            try {  
                Thread.sleep(1000);  
            } catch (InterruptedException e) {  
                throw new RuntimeException(e);  
            }  
            if (times == 80){  
                break;//当times到80，退出while,这时线程也就退出了  
            }  
        }  
    }  
}
```

### 11.2.2 为什么是start

`run.strat(); //启动线程->最终会执行cat的run方法`

```
(1)
public synchronized void start(){
	strat0();
}
(2)
//start0() 是本地方法，是JVM调用，底层是c/c++实现
//真正实现多线程的效果，start0()，而不是run
private native void start0();
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027362018-3c68e606-a92c-425c-873a-c4177fabb41c.png)

**start()方法调用start0()方法后，该线程并不一定会立马执行，只是将线程变成可运行状态。具体什么时候执行，取决于CPU，由CPU同一调度**

#### 11.2.2.1 实现Runnable接口

```
package com.cwz.threaduse;  
  
/**  
 * @author 陈文臻  
 * 通过实现接口Runnable来开发线程  
 */  
public class Thread02 {  
    public static void main(String[] args) {  
  
        Dog dog = new Dog();  
        //dog.start()  这里不能调用用start  
        //创建Thread对象，把dog对象(实现Runnable),放入Thread  
        Thread thread = new Thread(dog);  
        thread.start();  
  
  
    }  
}  
  
class Dog implements Runnable {//通过Runnable接口，开发线程  
  
    int count = 0;  
  
    @Override  
    public void run() {//普通方法  
        while (true) {  
            System.out.println("hi" + (++count) + Thread.currentThread().getName());  
  
            //休眠1s  
            try {  
                Thread.sleep(1000);  
            } catch (InterruptedException e) {  
                throw new RuntimeException(e);  
            }  
  
            if (count == 10) {  
                break;  
            }  
        }  
    }  
}
```

#### 11.2.2.2 代理模式

```
Dog dog = new Dog();   
Thread thread = new Thread(dog);  
thread.start();
```

**这里底层使用了设计模式[代理模式]**

```
//线程代理类，模拟了一个极简的Thread  
class Proxy implements Runnable {//你可以把Proxy类当作Thread  
  
    private Runnable target = null;//属性，类型是Runnable  
  
    public Proxy(Runnable target) {  
        this.target = target;  
    }  
  
    @Override  
    public void run() {  
        if (target != null) {  
            target.run();  //动态绑定
        }  
    }  
  
    public void start() {  
        start0();//这个方法是真正实现多线程的方法  
    }  
  
    public void start0() {  
        run();  
    }  
  
}
```

### 11.2.3 继承Thread  VS  实现Runnable

1. 从java的设计来看，通过继承Thread或者实现Runnable接口来创建线程==本质上没有区别==，从jdk帮助文档我们可以看到Thread类本身就实现了Runnable接口start `start() -> start0()`
2. 实现Runnable接口方式更加适合多个线程共享一个资源，并且避免了单继承的限制，建议使用Runnable

# 12. 多线程基础

## 12.1 多线程执行

```
package com.cwz.threaduse;  
  
/**  
 * @author 陈文臻  
 * main线程启动两个子线程  
 */  
public class Thread03 {  
    public static void main(String[] args) {  
  
        T1 t1 = new T1();  
        T2 t2 = new T2();  
        Thread thread = new Thread(t1);  
        Thread thread1 = new Thread(t2);  
        thread.start();//启动第一个线程  
        thread1.start();//启动第二个线程  
    }  
}  
  
  
class T1 implements Runnable {  
  
    int count = 0;  
  
    @Override  
    public void run() {  
        while(true) {  
            //每隔1s输出"hello world"输出10次  
            System.out.println("hello world " + (count++));  
            try {  
                Thread.sleep(1000);  
            } catch (InterruptedException e) {  
                throw new RuntimeException(e);  
            }  
            if(count == 10){  
                break;  
            }  
        }  
    }  
}  
  
class T2 implements Runnable {  
  
    int count = 0;  
  
    @Override  
    public void run() {  
        while(true) {  
            //每隔1s输出"hello world"输出5次  
            System.out.println("hi " + (count++));  
            try {  
                Thread.sleep(1000);  
            } catch (InterruptedException e) {  
                throw new RuntimeException(e);  
            }  
            if(count == 5){  
                break;  
            }  
        }  
    }  
}
```

### 12.1.1 多线程机制

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027375411-65860828-f998-4799-8973-8518d8e95864.png)

### 12.1.2 线程如何理解

```
package com.cwz.threaduse;  
  
/**  
 * @author 陈文臻  
 * main线程启动两个子线程  
 */  
public class Thread03 {  
    public static void main(String[] args) {  
  
        T1 t1 = new T1();  
        T2 t2 = new T2();  
        Thread thread = new Thread(t1);  
        Thread thread1 = new Thread(t2);  
        thread.start();//启动第一个线程  
        thread1.start();//启动第二个线程  
    }  
}  
  
  
class T1 implements Runnable {  
  
    int count = 0;  
  
    @Override  
    public void run() {  
        while (true) {  
            //每隔1s输出"hello world"输出10次  
            System.out.println("hello world " + (count++));  
            try {  
                Thread.sleep(1000);  
            } catch (InterruptedException e) {  
                throw new RuntimeException(e);  
            }  
            if (count == 10) {  
                break;  
            }  
        }  
    }  
}  
  
class T2 implements Runnable {  
  
    int count = 0;  
  
    @Override  
    public void run() {  
        while (true) {  
            //每隔1s输出"hello world"输出5次  
            System.out.println("hi " + (count++));  
            try {  
                Thread.sleep(1000);  
            } catch (InterruptedException e) {  
                throw new RuntimeException(e);  
            }  
            if (count == 5) {  
                break;  
            }  
        }  
    }  
}
```

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027386478-81bdf7da-23e2-491d-b88c-9018864d4106.png)

## 12.2 线程终止

### 12.2.1 基本说明

- 当线程完成任务后，会自动退出
- 还可以通过==使用变量==来控制run方法退出的方式停止线程，即==通知方式==

```
package com.cwz.exit;  
  
/**  
 * @author 陈文臻  
 */  
public class ThreadExit {  
    public static void main(String[] args) throws InterruptedException {  
  
        T t = new T();  
        t.start();  
  
        //如果希望main线程去控制t1线程的终止必须可以修改loop  
        //让t1退出run方法，从而终止t1线程 -> 通知方式  
  
        //让主线程休眠10s，再通知t1线程退出  
        System.out.println("==主线程休眠10s==");  
        Thread.sleep(10 * 1000);  
        t.setLoop(false);  
    }  
}  
  
  
class T extends Thread{  
  
    int count = 0;  
    //设置一个控制变量  
    private boolean loop = true;  
    @Override  
    public void run() {  
        while (true){  
            try {  
                Thread.sleep(50);  
            } catch (InterruptedException e) {  
                throw new RuntimeException(e);  
            }  
            System.out.println("T 运行中..." + (++count));  
        }  
    }  
  
    public void setLoop(boolean loop) {  
        this.loop = loop;  
    }  
}
```

## 12.3 线程常用方法

### 12.3.1 常用方法第一组

|   |   |
|---|---|
|方法|作用|
|setName|设置线程名称，使之与参数name相同|
|getName|返回该线程的名称|
|start|该线程开始执行; java虚拟机底层调用该线程的start0方法|
|run|调用线程对象run方法|
|setPriority|更改线程的优先级|
|getPriority|获取线程的优先级|
|sleep|再指定的毫秒数内让当前正在执行的线程休眠(暂停执行)|
|interrupt|中断线程|

#### 12.3.1.1 注意事项和细节

- start底层会创建新的线程，调用run，run就是一个简单的方法调用，==不会启动新线程
- 线程优先级的范围
- interrupt：中断线程，但并没有真正的结束线程，所以一般用于中断正在休眠的线程
- sleep：线程的静态方法，使当前线程休眠

```
package com.cwz.Threadmethod;  
  
/**  
 * @author 陈文臻  
 */  
public class ThreadMethod {  
    public static void main(String[] args) throws InterruptedException {  
        //测试相关方法  
        T t = new T();  
        t.setName("cwz");  
        t.setPriority(Thread.MIN_PRIORITY);  
        t.start();//启动子线程  
  
        //主线程打印5 hi，然后我就中断 子线程的休眠  
        for (int i = 0; i < 5; i++) {  
            Thread.sleep(10000);  
            System.out.println("hi" + i);  
        }  
  
        System.out.println(t.getName() + "优先级 " + t.getPriority());  
  
        t.interrupt();//当执行到这里，就会中断 t线程的修i按  
        //中断休眠  
  
    }  
}  
  
class T extends Thread {//自定义的线程类  
  
    @Override  
    public void run() {  
        while (true) {  
            for (int i = 0; i < 100; i++) {  
                //Thread.currentThread().getName() 获取当前线程的名称  
                System.out.println(Thread.currentThread().getName() + "吃包子~~~~" + i);  
            }  
            try {  
                System.out.println(Thread.currentThread().getName() + "休眠中~~~~");  
                Thread.sleep(20000);  
            } catch (InterruptedException e) {  
                //当线程执行到一个interrupt方法时，就会catch一个异常，可以加入自己的业务代码  
                System.out.println(Thread.currentThread().getName() + "被 interrupt了");  
            }  
        }  
    }  
}
```

### 12.3.2 常用方法第二组

- yield: ==线程的礼让==。让出cpu，让其他线程执行，但礼让时间不确定，所以也*不一定礼让成功
- join: ==线程的插队==。插队的线程一旦插队成功，则肯定先执行玩插入的线程所有的任务  
    案例：创建一个子线程，每隔1s输出hello，输出20次，主线程输出5次后，就让子线程运行完毕，主线程再继续

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027400243-4bd1329d-08a6-4c22-8173-6a9d2ea20644.png)

```
package com.cwz.Threadmethod;  
  
/**  
 * @author 陈文臻  
 */  
public class ThreadMethod2 {  
    public static void main(String[] args) throws InterruptedException {  
        T2 t2 = new T2();  
        t2.start();  
  
        for (int i = 0; i <= 20; i++) {  
            Thread.sleep(10000);  
            System.out.println("主线程 吃了" + i + "包子");  
            if (i == 5) {  
                System.out.println("主线程让子线程全部吃完");  
                t2.join();// 这里相当于让t2 线程先执行完毕  
  
                //Thread.yield();//礼让不一定成功  
                System.out.println("子线程吃完了 主线程接着吃");  
            }  
        }  
    }  
}  
  
class T2 extends Thread {  
    @Override  
    public void run() {  
        for (int i = 0; i < 20; i++) {  
            try {  
                Thread.sleep(10000);//休眠1s  
            } catch (InterruptedException e) {  
                e.printStackTrace();  
            }  
            System.out.println("子线程吃了" + i + "个包个");  
        }  
    }  
}
```

### 12.3.3 用户线程和守护线程

- 用户线程：也叫工作线程，当线程的任务执行完或通知方式结束
- 守护线程：一般是为工作线程的，当所有的用户线程结束，守护线程自动结束
- 常见的守护线程：垃圾回收机制

```
package com.cwz.Threadmethod;  
  
/**  
 * @author 陈文臻  
 */  
public class threadMethod03 {  
    public static void main(String[] args) throws InterruptedException {  
        MyDaemonThread myDaemonThread = new MyDaemonThread();  
        //如果我们希望当main线程结束后，子线程自动结束  
        //只需要将子线程设置成守护线程即可  
  
        myDaemonThread.setDaemon(true);  
        myDaemonThread.start();  
  
        for (int i = 0; i <= 10; i++) {  
            System.out.println("嘿嘿嘿");  
            Thread.sleep(1000);  
        }  
    }  
}  
  
class MyDaemonThread extends Thread {  
    @Override  
    public void run() {  
        for (; ; ) {//无序排序  
            try {  
                Thread.sleep(50);  
            } catch (InterruptedException e) {  
                e.printStackTrace();  
            }  
            System.out.println("哈哈哈哈");  
        }  
    }  
}
```

## 12.4 线程的生命周期

线程状态，线程可以处于以下状态之一

|   |   |
|---|---|
|状态|意义|
|NEW|尚未启动的线程处于此状态|
|RUNNABLE|在Java虚拟机中执行的线程处于此状态|
|BLOCKED|被阻塞等待监视器锁定的线程处于此状态|
|WAITING|正在等待另一个线程执行动作的线程处于此状态|
|TIME_WAITING|正在等待另一个线程执行动作到达指定等待时间的线程处于此状态|
|TERMINATED|已退出的线程处于此状态|

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027413236-37194d4c-d98f-4a4a-98a3-6d6879f3bbf0.png)

## 12.5 线程同步机制

### 12.5.1 线程同步

- 在多线程编程，一些不敏感数据不允许被多个线程同时访问，此时就使用同步访问技术，保证数据在任何同一时刻，最多有一个线程访问，以保证数据的完整性
- 也可以这样理解：线程同步，即当==有一个线程在对内存进行操作时，其他线程都不可以对这个内存地址进行操作==，直到该线程完成操作，其他线程才能对该内存地址进行操作

### 12.5.2 同步具体方法

- 同步代码块

```
synchronized(对象){//得到对象的锁，才能操作同步代码
	//需要被同步的代码；
}
```

- synchronzied还可以放在方法声明中，表示整个方法为同步方法

```
public synchronized void m(String name){
	//需要同步的代码
}
```

- 如何理解  
    就好像 某小伙伴上厕所前先把门关上(上锁) 完事后出来(解锁)，那么其它小伙伴就可以使用厕所了

```
package com.cwz.syn;  
  
/**  
 * @author 陈文臻  
 * 使用多线程模拟三个窗口同时售票同时售票100张  
 */  
public class SellTicket {  
    public static void main(String[] args) {  
  
        //Thread方式的创建  
  
//        //测试  
//        SellTicket01 sellTicket01 = new SellTicket01();  
//        SellTicket01 sellTicket02 = new SellTicket01();  
//        SellTicket01 sellTicket03 = new SellTicket01();  
//  
//        //这里会出现票数超卖现象  
//        sellTicket01.start();  
//        sellTicket02.start();  
//        sellTicket03.start();  
  
  
        //Runnable接口的创建  
        System.out.println("==使用接口的方法==");  
        SellTicket02 sellTicket02 = new SellTicket02();  
  
        new Thread(sellTicket02).start();  
        new Thread(sellTicket02).start();  
        new Thread(sellTicket02).start();  
  
    }  
}  
  
//实现接口的方式,使用同步方法synchronized实现线程同步  
class SellTicket03 implements Runnable {  
  
    private static int num = 100;//让多个线程共享  
    private boolean loop = true;//控制run方法的一个变量  
  
    public synchronized void sell() { //同步方法，在同一时刻，只能有一个线程来执行run方法  
        if (num <= 0) {  
            System.out.println("售票结束");  
            loop = false;  
            return;        }  
  
        //休眠  
        try {  
            Thread.sleep(50);  
        } catch (InterruptedException e) {  
            throw new RuntimeException(e);  
        }  
  
        System.out.println("窗口" + Thread.currentThread().getName() + "售出一张票" + "剩余票数: " + (--num));  
    }  
  
    @Override  
    public void run() { //同步方法，在同一时刻，只能有一个线程来执行我们的run方法  
        while (loop) {  
  
            sell();//sell方法是一个同步方法  
        }  
  
    }  
  
}  
  
//使用Thread方式  
  
class SellTicket01 extends Thread {  
  
    private static int num = 100;//让多个线程共享  
  
    @Override  
    public void run() {  
        while (true) {  
            if (num <= 0) {  
                System.out.println("售票结束");  
                break;            }  
  
            //休眠  
            try {  
                Thread.sleep(50);  
            } catch (InterruptedException e) {  
                throw new RuntimeException(e);  
            }  
  
            System.out.println("窗口" + Thread.currentThread().getName() + "售出一张票" + "剩余票数: " + (--num));  
        }  
    }  
}  
  
//实现接口的方式  
class SellTicket02 implements Runnable {  
  
    private static int num = 100;//让多个线程共享  
  
    @Override  
    public void run() {  
        while (true) {  
            if (num <= 0) {  
                System.out.println("售票结束");  
                break;            }  
  
            //休眠  
            try {  
                Thread.sleep(50);  
            } catch (InterruptedException e) {  
                throw new RuntimeException(e);  
            }  
  
            System.out.println("窗口" + Thread.currentThread().getName() + "售出一张票" + "剩余票数: " + (--num));  
        }  
    }  
  
}
```

## 12.6 互斥锁

### 12.6.1 基本介绍

- Java在Java语言中，引入了对象互斥锁的概念，来==保证共享数据操作的完整性
- 每个对象都==对应一个可称为"互斥锁"的标记==，这个标记用来保证在任意时刻，只能有一个线程访问该对象
- 关键字synchronized来与对象的互斥锁联系。当某个对象用synchronized修饰时，==表明该对象在任一时刻只能由一个线程访问
- 同步的局限性：导致线程的执行==效率要降低==
- 同步方法(非静态的)锁可以是this，也可以是其他对象(要求是同一个对象)
- 同步方法(静态的)的锁为当前类本身

### 12.6.2 注意事项和细节

1. 同步方法如果没有使用static修饰，默认锁对象为this
2. 如果方法使用static修饰，默认锁对象:当前类.class
3. 实现的落地步骤:

- 需要线分析上锁的代码
- 选择==同步代码==或同步方法
- 要求多个线程的锁对象为同一个即可

### 12.6.3 分析同步原理

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027445991-20946275-4c8d-44ea-954e-b4914acbc16b.png)

## 12.7 线程死锁

### 12.7.1 基本介绍

多个线程都占用对方的锁资源，但不肯让，导致了死锁，在编程时一定要避免死锁的发生

例如：  
妈妈：你先完成作业，才让你玩手机  
小明：你先让我玩手机，我才完成作业

```
package com.cwz.syn;  
  
/**  
 * @author 陈文臻  
 */  
public class DeadLock {  
    public static void main(String[] args) {  
        //模拟一个死锁现象  
        DeadLockDemo deadLockDemo = new DeadLockDemo(true);  
        DeadLockDemo deadLockDemo1 = new DeadLockDemo(false);  
    }  
}  
  
class DeadLockDemo extends Thread{  
    static Object o1 = new Object();//保证多线程，共享一个对象，这里使用static  
    static Object o2 = new Object();  
    boolean flag;  
    public DeadLockDemo(boolean flag){  
        this.flag = flag;  
    }  
  
    @Override  
    public void run(){  
  
        //下面业务代码的分析  
        //1.如果flag为true为T，线程就会先得到/持有o1对象锁，然后尝试去获取o2对象锁  
        //2.如果线程A得不到o2对象锁，就会Blocked  
        //3.如果flag为F，线程B就会先得到/持有o2对象锁，然后尝试去获取o1对象锁  
        //4.如果线程B得不到o1对象锁，就会Blocked  
        if(flag){  
            synchronized (o1){//对象互斥锁，下面是同步代码  
                System.out.println(Thread.currentThread().getName() + "进入1");  
                synchronized (o2){//这里获得li对象的监视权  
                    System.out.println(Thread.currentThread().getName() + "进入2");  
                }  
            }  
        }else{  
            synchronized (o2){  
                System.out.println(Thread.currentThread() + "进入3");  
                synchronized (o1){//这里获得li对象的监视权  
                    System.out.println(Thread.currentThread().getName() + "进入4");  
                }  
            }  
        }  
    }  
}
```

## 12.8 释放锁

### 12.8.1 下面操作会释放锁

- 当前线程的同步方法、同步代码块执行结束  
    案例：上厕所，完事出来
- 当前线程在同步代码块、同步方法中遇到break，return  
    案例：没有正常的完事，经理叫他修改bug，不得已出来
- 当前线程在同步代码块、同步方法中出现未处理的Error或Exception，导致异常结束  
    案例：没有正常完事，发现忘带纸，不得已出来
- 当前线程在同步代码块、同步方法中执行线程对象的wait()方法，当前线程暂停，并释放锁  
    案例：没有正常完事，觉得需要酝酿下，所以出来等会再进来

### 12.8.2 下面操作不会释放锁

- 线程执行同步代码块或同步方法时，程序调用thread.sleep()、Thread.yield()方法暂停当前线程的执行，不会释放锁  
    案例：上厕所，太困了，在坑位上眯了一会
- 线程执行同步代码块时，其他线程调用了该线程的suspend()方法将该线程挂起，该线程不会释放锁  
    提示：应尽量避免使用suspend()和resume()来控制线程，方法不推荐再使用

# 13. IO流

## 13.1 文件

### 13.1.1 概念

- 文件流  
    文件在程序中是以流的形式来操作的  
    ![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027455902-d528e773-0e55-4588-b5c3-d320fd37b4a5.png)

流：数据在数据源（文件）和程序（内存）之间经历的路径  
输入流：数据从数据源（文件）到程序（内存）的路径  
输出流：数据从程序（内存）到数据源（文件）的路径

### 13.1.2 常用操作

- 创建文件对象相关构造器的方法

```
package com.cwz.file;  
  
import javax.annotation.processing.SupportedAnnotationTypes;  
import java.io.File;  
import java.io.IOException;  
  
public class FileCreate {  
	public static void main(String[] args){  
  
}  
  
  
	//方式1 new File(String pathname)  
	  
	public void create01(){  
		String filePath = "e:\\news1.text";  
		File file = new File(filePath);  
	  
		try {  
			file.createNewFile();  
			System.out.println("文件创建成功");  
		} catch (IOException e) {  
			throw new RuntimeException(e);  
		}  
	}  
	  
	  
	//方式2 new File(File parent,String child) //根据父目录文件+子路径构建  
	//e:\\news2.txt  
	public void create02(){  
		File parentFile = new File("e:\\");  
		String fileName = "news2.txt";  
		//这里的file对象中，在java程序中只是一个对象  
		//只有执行create方法才会执行  
		File file = new File(parentFile,fileName);  
		  
		try {  
			file.createNewFile();  
			System.out.println("创建成功");  
		} catch (IOException e) {  
			throw new RuntimeException(e);  
		}  
	}  
	  
	  
	//方式3 new File(String parent,String child) //根据父目录+子路径构建  
	public void create03(){  
		String parentPath = "e:\\";  
		String fileName = "new3.txt";  
		File file = new File(parentPath,fileName);  
		  
		try {  
			file.createNewFile();  
			System.out.println("创建成功");  
		} catch (IOException e) {  
			throw new RuntimeException(e);  
		}  
	}  
}
```

- 获取文件信息

```
package com.cwz.file;  
  
import java.io.File;  
  
public class Fileformation {  
public static void main(String[] args) {  
  
}  
  
//获取文件的信息  
public void info(){  
//创建文件对象  
File file = new File("e:\\news1.txt");  
  
//调用相应的方法，得到对应信息  
System.out.println("文件名字=" + file.getName());  
System.out.println("文件绝对路径=" + file.getAbsolutePath());  
System.out.println("文件父级目录(字节)" + file.length());  
System.out.println("是否存在" + file.exists());  
System.out.println("是不是一个文件" + file.isFile());  
}  
}
```

- 目录的操作和文件删除

```
package com.cwz.file;  
  
import java.io.File;  
  
public class Directory_ {  
	public static void main(String[] args) {  
	  
	}  
	//判断 d:\\news1.txt是否存在，如果存在就删除  
	public void m1(){  
	  
		String filePath = "d:\\news1.txt";  
		File file = new File(filePath);  
		if ((file.exists())){  
		if(file.delete()){  
			System.out.println(filePath + "删除成功");  
		}else {  
			System.out.println(filePath + "删除失败");  
		}else{  
			System.out.println("该文件不存在....");  
		}  
	}  
}
```

## 13.2 IO流原理及流的分类

- Java IO流原理

1. I/O是Input/Output的缩写，I/O技术是非常实用的技术，用于处理数据传输。如读/写文件，网络通讯等
2. Java程序中，对于数据的输入/输出操作以流(stream)的方式进行
3. java.io包下提供了各种“流”类和接口，用以获取不同种类的数据，并通过方式输入或输出数据
4. 输入input：读取外部数据（磁盘、光盘等存储设备的数据）到程序（内存）中
5. 输出output：将程序（内存）数据输出到磁盘、光盘等存储设备中  
    ![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027465551-fd6d587c-ecb6-4a9a-9437-8f865c26e43d.png)

- 流的分类  
    按操作数据单位不同分为：字节流(8 bit)**二进制文件**,字符流(按字符，**对应几个字节 文本文件**)  
    按数据流的流向不同分为：输入流、输出流  
    按流的角色的不同分为：节点流，处理流/包装流

|   |   |   |
|---|---|---|
|(抽象基类)|字节流|字符流|
|输入流|InputStream|Reader|
|输出流|OutputStream|Writer|
|（1）Java的Io流共涉及40多个类，实际上非常规则，都是从如上4个人抽象基类派生的|||
|（2）由这四个类派生出来的子类名称都是以其父亲作为子类名后缀|||

## 13.3 IO流体系图-常用的类

- InputStream: 字节输入流

InputStream抽象类是所有类字节输入流的超类

InputStream常用的子类

1. FileInputStream: 文件输入流
2. BufferedInputStream: 缓冲字节输入流
3. ObjectInputStream: 对象字节输入流

## 13.4 节点流及流的分类

- 基本介绍

1. 节点流可以从一个特定的数据源**读写数据**，如FileReader、FileWriter  
    ![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027473731-05cc897e-916b-49ee-a647-04a47c327f0c.png)
2. 处理流(也叫**包装流**)是”连接“在已存在的流（节点流或处理流）之上，为程序提供更为强大的读写功能，如BufferedReader、BufferedWriter  
    ![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027478560-897cf6ae-6bf8-44f7-bc58-98f73fae2af3.png)

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1712027485427-6b3589f0-d454-4f5f-a4b0-5c604f82a2c4.png)

# 14. 坦克大战游戏(1.0版)

## 14.1 坦克大战游戏演示

涉及到的技术：

1. java面向对象编程
2. 多线程
3. 文件i/o操作
4. 数据库

## 14.2 java绘图坐标体系

### 14.2.1 基本介绍

![[14.2.1.1.png]]

### 14.2.2 像素

`计算机再屏幕上显示的内容都是由屏幕的每一个像素组成的`  
例如：计算机显示屏的分辨率是800x600，表示计算机屏幕上的每一行由800个点组成，共有600行，整个计算机屏幕共有480000个像素。==像素是一个密度单位，而厘米是一个长度单位，两者无法比较==

## 14.3 java绘图技术

### 14.3.1 绘图原理

- Component类提供了两个和绘图相关最重要的方法：

1. paint(Graphics g)绘制组件的外观
2. repaint()刷新组件的外观

- 当组件第一次在屏幕显示的时候，程序会自动地调用paint()方法来绘制组件
- 以下情况paint()将会被调用:

1. 窗口最小化再最大化
2. 窗口的大小发生变化
3. repaint函数被调用

### 14.3.2 绘图入门

```
package com.tank.draw;  
  
import javax.swing.*;  
import java.awt.*;  
  
/**  
 * @author 陈文臻  
 * 演示如何再面板上画出原型  
 */  
@SuppressWarnings({"all"})  
public class DrawCircle extends JFrame{ //JFrame对应窗口  
    //定义一个面板  
    private MyPanel mp = null;  
    public static void main(String[] args) {  
        new DrawCircle();  
    }  
  
    public DrawCircle(){  
        //初始化面板  
        mp = new MyPanel();  
        //把面板放入窗口(画框)  
        this.add(mp);  
        //设置窗口大小  
        this.setSize(400,300);  
        this.setVisible(true);//可以显示  
    }  
}  
  
//1. 先定义一个面板MyPanel(), 继承JPanel类， 画图形，就在面板上画  
class MyPanel extends JPanel {  
  
    //说明  
    //1.MyPanel 对象就是一个画板  
    //2.Graphics g 把g理解成一支画笔  
    //3，Graphics 提供了很多绘图的方法  
  
    //graphics g  
    @Override  
    public void paint(Graphics g) {//绘图方法  
        super.paint(g);//调用父类的方法，完成初始化  
  
        g.drawOval(10,10,100,100);  
    }  
}
```

![[14.3.2.1.png]]

### 14.3.3 Graphics类

Graphics类你可以理解就是画笔，为我们提供了各种绘制图形的方法:

|   |   |
|---|---|
|功能|方法|
|画直线|drawLine(int x1, int y1, int x2, int y2)|
|画矩形边框|drawRect(int x, int y, int width, int height)|
|画椭圆边框|drawOval(int x, int y, int width, int height)|
|填充矩形|fillRect(int x, int y, int width, int height)|
|填充椭圆|fillOval(int x, int y, int width, int height)|
|画图片|drawImage(Image img, int x ,int y,...)|
|画字符串|drawString(String str, int x, int y)|
|设置画笔的字体|setFont(Font font)|
|设置画笔的颜色|setColor(color c)|

```
package com.tank.draw;  
  
import javax.swing.*;  
import java.awt.*;  
  
/**  
 * @author 陈文臻  
 * 演示如何再面板上画出原型  
 */  
@SuppressWarnings({"all"})  
public class DrawCircle extends JFrame{ //JFrame对应窗口  
    //定义一个面板  
    private MyPanel mp = null;  
    public static void main(String[] args) {  
        new DrawCircle();  
    }  
  
    public DrawCircle(){  
        //初始化面板  
        mp = new MyPanel();  
        //把面板放入窗口(画框)  
        this.add(mp);  
        //设置窗口大小  
        this.setSize(400,300);  
        this.setVisible(true);//可以显示  
    }  
}  
  
//1. 先定义一个面板MyPanel(), 继承JPanel类， 画图形，就在面板上画  
class MyPanel extends JPanel {  
  
    //说明  
    //1.MyPanel 对象就是一个画板  
    //2.Graphics g 把g理解成一支画笔  
    //3，Graphics 提供了很多绘图的方法  
  
    //graphics g  
    @Override  
    public void paint(Graphics g) {//绘图方法  
        super.paint(g);//调用父类的方法，完成初始化  
  
        g.drawOval(10,10,100,100);  
  
  
        //演示绘制不同的图形  
        //画直线 drawLine(int x1, int y1, int x2, int y2)        g.drawLine(10,10,100,100);  
  
        //画矩形边框 drawRect(int x, int y, int width, int height)        g.drawRect(10,10,100,100);  
  
        //画椭圆边框 drawOval(int x, int y, int width, int height)  
        //填充矩形 fillRect(int x, int y, int width, int height)        //设置画笔的颜色  
        g.setColor(Color.blue);  
        g.fillRect(10,10,100,100);  
  
        //填充椭圆 fillOval(int x, int y, int width, int height)        g.fillOval(10,10,50,100);  
  
  
        //画图片 drawImage(Image img, int x ,int y,...)        //1.获取图片资源,/bg.png 表示再项目的根目录去获取 bg.png的图片资源  
        Toolkit.getDefaultToolkit().getImage(Panel.class.getResource("/bg.png"));  
        //g.drawImage(image,10,10,175,221,this);  
  
        //画字符串 drawString(String str, int x, int y)        //给画笔设置颜色字体  
        g.setColor(Color.blue);  
        g.setFont(new Font("隶书", Font.BOLD, 5));  
        g.drawString("北京你好",100,100);  
  
        //设置画笔的字体 setFont(Font font)        //设置画笔的颜色 setColor(color c)    }  
}
```

### 14.3.4 绘出坦克

![[14.3.4.1.png]]

```
//编写方法，画出坦克  
  
/**  
 * @param x      坦克的左上角x坐标  
 * @param y      坦克的左上角y坐标  
 * @param g      画笔  
 * @param direct 坦克方向(上下左右)  
 * @param type   坦克类型  
 */  
public void drawTank(int x, int y, Graphics g, int direct, int type) {  
  
    switch (type) {  
        case 0: //我们的坦克  
            g.setColor(Color.cyan);  
            break;        case 1://敌人的坦克  
            g.setColor(Color.yellow);  
            break;    }  
  
    //根据坦克方向，来绘制坦克  
    switch (direct){  
        case 0://表示向上  
            g.fill3DRect(x, y,10,60,false);//画出坦克左边的轮子  
            g.fill3DRect(x + 30, y,10,60,false);//画出坦克右边的轮子  
            g.fill3DRect(x+10,y+10,20,40,false);//画出坦克的盖子  
            g.fillOval(x+10,y+20,20,20);//画出坦克的圆盖  
            g.drawLine(x+20,y + 30 , x+20 ,y);//画出炮筒  
            break;  
        default:  
            System.out.println("暂时没有处理");  
    }  
}
```

![[14.3.4.2.png]]

## 14.4 java事件处理机制

### 14.4.1 基本说明

java事件处理是采取"委派事件模型"。当事件方式时，产生事件的对象，会把此"信息"传递给"事件的监听者"处理，这里所说的"信息"实际上就是java.awt.event事件类库里某个类所创建的对象，把它称为"事件的对象"

`委派事件模型 = 事件发生和处理不在一个地方`  
![[Java/images/14.4.1.1.png]]

`小球移动`

```
package com.tank.event;  
  
import javax.swing.*;  
import java.awt.*;  
import java.awt.event.KeyEvent;  
import java.awt.event.KeyListener;  
  
/**  
 * @author 陈文臻  
 * 演示小球通过键盘控制上下左右的移动 -》讲解java事件控制  
 */  
public class BallMove extends JFrame { //窗口  
    MyPanel mp = null;  
  
    public static void main(String[] args) {  
        BallMove ballMove = new BallMove();  
  
    }  
  
    //构造器  
    public BallMove() {  
        mp = new MyPanel();  
        this.add(mp);  
        this.setSize(400, 300);  
        //窗口JFrame对象可以监听键盘事件，即可以监听到面板上，键盘事件  
        this.addKeyListener(mp);  
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);  
        this.setVisible(true);  
  
  
    }  
}  
  
//面板，可以画小球  
//KeyListener是监听器，可以监听键盘事件  
class MyPanel extends JPanel implements KeyListener {  
  
    //为了让小球可以移动，把他的左上角的坐标(x,y)设置变量  
    int x = 10;  
    int y = 10;  
    @Override  
    public void paint(Graphics g) {  
        super.paint(g);  
        g.fillOval(x, y, 20, 20);//默认黑色  
    }  
  
    //有字符输出，该方法就会触发  
    @Override  
    public void keyTyped(KeyEvent e) {  
  
    }  
    //当某个键按下，该方法会触发  
    @Override  
    public void keyPressed(KeyEvent e) {  
        //System.out.println((char)e.getKeyCode() + "被按下..");  
  
        //根据用户按下的不同键，来处理小球的移动(上下左右键）  
        //在java中，会给每一个键定义一个值  
        if (e.getKeyCode() == KeyEvent.VK_DOWN) {//KeyEvent.VK_DOWN就是向下的箭头对应的code  
            y++;  
        } else if (e.getKeyCode() == KeyEvent.VK_UP) {  
            y--;  
        } else if (e.getKeyCode() == KeyEvent.VK_LEFT) {  
            x--;  
        } else if (e.getKeyCode() == KeyEvent.VK_RIGHT) {  
            x++;  
        }  
  
        //让面板重绘  
        this.repaint();  
    }  
  
    //当某个键被松开，该方法会出发  
    @Override  
    public void keyReleased(KeyEvent e) {  
  
  
    }}
```

### 14.4.2 事件处理机制

- ==事件源==：事件源是一个产生事件的对象，比如按钮，窗口等
- ==事件==：事件就是承载事件源状态改变时的对象，比如当键盘事件，鼠标事件，窗口事件等等，会生成一个事件对象，该对象保存着当前事件很多信息，比如KeyEvent对象有含有被按下键的Code值。java.awt.event包和javax.swing.event包中定义了各种事件类型
- ==事件类型==

|   |   |
|---|---|
|事件类|说明|
|ActionEvent|通常在按下按钮或双击一个列表选项或选择某个菜单时发生|
|AdjustmetEvent|当操作一个滚条时发生|
|ComponentEvent|当一个组件隐藏，移动，改变大小时发送|
|ContainerEvent|当一个组件从容器中加入或者删除时发生|
|FocusEvent|当一个组件获得或是失去焦点时发生|
|ItemEvent|当一个复选框或是列表项被选中时，当一个选择框或者菜单被选中|
|KeyEvent|当从键盘的按键被按下，松开时发生|
|MouseEvent|当鼠标被拖动，移动，点击，按下..|
|TextEvent|当文本框和文本域的文本发生改变时发生|
|WindowEvent|当一个窗口激活，关闭，失效，恢复，最小化...|

- ==事件监听接口==：

1. 当事件源产生一个事件，可以传送给事件监听者处理
2. 事件监听者实际上就是一个类，该类实现了某个事件监听器接口比如前面我们案例中的MyPanel就是一个类，它实现了Key Listener接口，它就是可以作为一个事件监听者，对接受到的事件进行处理
3. 事件监听器接口有多种，不同的事件监听器接口可以监听不同的事件，一个类可以实现多个监听接口
4. 这些接口在java.awt.event包和javax.swing.event包中定义。

## 14.5 坦克大战游戏(1.0版)

### 14.5.1 坦克(上下左右)

```
/**  
     * @param x      坦克的左上角x坐标  
     * @param y      坦克的左上角y坐标  
     * @param g      画笔  
     * @param direct 坦克方向(上下左右)  
     * @param type   坦克类型  
     */  
  
    public void drawTank(int x, int y, Graphics g, int direct, int type) {  
  
        switch (type) {  
            case 0: //我们的坦克  
                g.setColor(Color.cyan);  
                break;            case 1://敌人的坦克  
                g.setColor(Color.yellow);  
                break;        }  
  
        //根据坦克方向，来绘制对应形状的坦克  
        //direct表示方向(0：上 1：右 2：下 3：左)  
  
        switch (direct) {  
            case 0://表示向上  
                g.fill3DRect(x, y, 10, 60, false);//画出坦克左边的轮子  
                g.fill3DRect(x + 30, y, 10, 60, false);//画出坦克右边的轮子  
                g.fill3DRect(x + 10, y + 10, 20, 40, false);//画出坦克的盖子  
                g.fillOval(x + 10, y + 20, 20, 20);//画出坦克的圆盖  
                g.drawLine(x + 20, y + 30, x + 20, y);//画出炮筒  
                break;  
            case 1://表示向右  
                g.fill3DRect(x, y, 60, 10, false);//画出坦克左边的轮子  
                g.fill3DRect(x, y + 30, 60, 10, false);//画出坦克右边的轮子  
                g.fill3DRect(x + 10, y + 10, 40, 20, false);//画出坦克的盖子  
                g.fillOval(x + 20, y + 10, 20, 20);//画出坦克的圆盖  
                g.drawLine(x + 30, y + 20, x + 60, y + 20);//画出炮筒  
                break;  
            case 2://表示向下  
                g.fill3DRect(x, y, 10, 60, false);//画出坦克左边的轮子  
                g.fill3DRect(x + 30, y, 10, 60, false);//画出坦克右边的轮子  
                g.fill3DRect(x + 10, y + 10, 20, 40, false);//画出坦克的盖子  
                g.fillOval(x + 10, y + 20, 20, 20);//画出坦克的圆盖  
                g.drawLine(x + 20, y + 30, x + 20, y + 60);//画出炮筒  
                break;  
            case 3://表示向左  
                g.fill3DRect(x, y, 60, 10, false);//画出坦克左边的轮子  
                g.fill3DRect(x, y + 30, 60, 10, false);//画出坦克右边的轮子  
                g.fill3DRect(x + 10, y + 10, 40, 20, false);//画出坦克的盖子  
                g.fillOval(x + 20, y + 10, 20, 20);//画出坦克的圆盖  
                g.drawLine(x + 30, y + 20, x, y + 20);//画出炮筒  
                break;  
            default:  
                System.out.println("暂时没有处理");  
        }  
    }  
  
    @Override  
    public void keyTyped(KeyEvent e) {  
  
    }  
    //处理wdsa 键按下的情况  
    @Override  
    public void keyPressed(KeyEvent e) {  
        if (e.getKeyCode() == KeyEvent.VK_W) {//按下W键  
            //改变坦克方向  
            hero.setDirect(0);  
        } else if (e.getKeyCode() == KeyEvent.VK_D) {//按下D键  
            hero.setDirect(1);  
        } else if (e.getKeyCode() == KeyEvent.VK_S) {//按下D键  
            hero.setDirect(2);  
        } else if (e.getKeyCode() == KeyEvent.VK_A) {//按下A键  
            hero.setDirect(3);  
        }  
  
        //让面板重绘  
        this.repaint();  
    }  
  
    @Override  
    public void keyReleased(KeyEvent e) {  
  
    }}
```

### 14.5.2 坦克移动

`在tank.java中编写方法`

```
//上右下左移动方法  
public void moveUp() {  
    y -= 1;  
}  
  
public void moveRight() {  
    x += 1;  
}  
  
public void moveDown() {  
    y += 1;  
}  
  
public void moveLeft() {  
    x -= 1;  
}
```

`添加moveXX方法`

```
@Override  
public void keyPressed(KeyEvent e) {  
    if (e.getKeyCode() == KeyEvent.VK_W) {//按下W键  
        //改变坦克方向  
        hero.setDirect(0);  
        //修改坦克的坐标 y - 1        hero.moveUp();  
    } else if (e.getKeyCode() == KeyEvent.VK_D) {//按下D键  
        hero.setDirect(1);  
        hero.moveRight();  
    } else if (e.getKeyCode() == KeyEvent.VK_S) {//按下D键  
        hero.setDirect(2);  
        hero.moveDown();  
    } else if (e.getKeyCode() == KeyEvent.VK_A) {//按下A键  
        hero.setDirect(3);  
        hero.moveLeft();  
    }  
  
    //让面板重绘  
    this.repaint();  
}
```

### 14.5.3 1.0初步模型

#### 14.5.3.1 EmenyTank.java

```
package com.tank.tankgame2;  
  
/**  
 * @author 陈文臻  
 * 敌人的坦克  
 */  
public class EnemyTank extends Tank{  
    public EnemyTank(int x, int y) {  
        super(x, y);  
    }  
}
```

#### 14.5.3.2 Hero.java

```
package com.tank.tankgame2;  
  
/**  
 * @author 陈文臻  
 * 我们自己的坦克  
 */  
public class Hero extends Tank {  
    public Hero(int x, int y) {  
        super(x, y);  
    }  
}
```

#### 14.5.3.3 MyPanel.java

```
package com.tank.tankgame2;  
  
import javax.swing.*;  
import java.awt.*;  
import java.awt.event.KeyEvent;  
import java.awt.event.KeyListener;  
import java.util.Vector;  
  
/**  
 * @author 陈文臻  
 * 坦克大战绘图区  
 */  
  
//为了监听键盘事件，实现KeyListener  
public class MyPanel extends JPanel implements KeyListener {  
    //定义我的坦克  
    Hero hero = null;  
    //定义敌人坦克，放入Vector  
    Vector<EnemyTank> enemyTanks = new Vector<>();  
    int enemyTankSize = 3;  
  
    public MyPanel() {  
        hero = new Hero(100, 100);//初始化自己的坦克  
        //hero.setSpeed(2);  
        //初始化敌人的坦克  
        for (int i = 0; i < enemyTankSize; i++) {  
            //创建一个敌人的坦克  
            EnemyTank enemyTank = new EnemyTank(100 * (i + 1), 0);  
            //设置方向  
            enemyTank.setDirect(2);  
            //加入  
            enemyTanks.add(enemyTank);  
        }  
    }  
  
    @Override  
    public void paint(Graphics g) {  
        super.paint(g);  
        g.fillRect(0, 0, 1000, 750);//填充矩形，默认黑色  
  
        //画出坦克 - 封装到方法  
        drawTank(hero.getX(), hero.getY(), g, hero.getDirect(), 0);  
  
        //画出敌人的坦克 遍历Vector  
        for (int i = 0; i < enemyTanks.size(); i++) {  
            //取出坦克  
            EnemyTank enemyTank = enemyTanks.get(i);  
            drawTank(enemyTank.getX(),enemyTank.getY(),g,enemyTank.getDirect(),1);  
        }  
    }  
  
    //编写方法，画出坦克  
  
    /**  
     * @param x      坦克的左上角x坐标  
     * @param y      坦克的左上角y坐标  
     * @param g      画笔  
     * @param direct 坦克方向(上下左右)  
     * @param type   坦克类型  
     */  
  
    public void drawTank(int x, int y, Graphics g, int direct, int type) {  
  
        switch (type) {  
            case 0: //我们的坦克  
                g.setColor(Color.cyan);  
                break;            case 1://敌人的坦克  
                g.setColor(Color.yellow);  
                break;        }  
  
        //根据坦克方向，来绘制对应形状的坦克  
        //direct表示方向(0：上 1：右 2：下 3：左)  
  
        switch (direct) {  
            case 0://表示向上  
                g.fill3DRect(x, y, 10, 60, false);//画出坦克左边的轮子  
                g.fill3DRect(x + 30, y, 10, 60, false);//画出坦克右边的轮子  
                g.fill3DRect(x + 10, y + 10, 20, 40, false);//画出坦克的盖子  
                g.fillOval(x + 10, y + 20, 20, 20);//画出坦克的圆盖  
                g.drawLine(x + 20, y + 30, x + 20, y);//画出炮筒  
                break;  
            case 1://表示向右  
                g.fill3DRect(x, y, 60, 10, false);//画出坦克左边的轮子  
                g.fill3DRect(x, y + 30, 60, 10, false);//画出坦克右边的轮子  
                g.fill3DRect(x + 10, y + 10, 40, 20, false);//画出坦克的盖子  
                g.fillOval(x + 20, y + 10, 20, 20);//画出坦克的圆盖  
                g.drawLine(x + 30, y + 20, x + 60, y + 20);//画出炮筒  
                break;  
            case 2://表示向下  
                g.fill3DRect(x, y, 10, 60, false);//画出坦克左边的轮子  
                g.fill3DRect(x + 30, y, 10, 60, false);//画出坦克右边的轮子  
                g.fill3DRect(x + 10, y + 10, 20, 40, false);//画出坦克的盖子  
                g.fillOval(x + 10, y + 20, 20, 20);//画出坦克的圆盖  
                g.drawLine(x + 20, y + 30, x + 20, y + 60);//画出炮筒  
                break;  
            case 3://表示向左  
                g.fill3DRect(x, y, 60, 10, false);//画出坦克左边的轮子  
                g.fill3DRect(x, y + 30, 60, 10, false);//画出坦克右边的轮子  
                g.fill3DRect(x + 10, y + 10, 40, 20, false);//画出坦克的盖子  
                g.fillOval(x + 20, y + 10, 20, 20);//画出坦克的圆盖  
                g.drawLine(x + 30, y + 20, x, y + 20);//画出炮筒  
                break;  
            default:  
                System.out.println("暂时没有处理");  
        }  
    }  
  
    @Override  
    public void keyTyped(KeyEvent e) {  
  
    }  
    //处理wdsa 键按下的情况  
    @Override  
    public void keyPressed(KeyEvent e) {  
        if (e.getKeyCode() == KeyEvent.VK_W) {//按下W键  
            //改变坦克方向  
            hero.setDirect(0);  
            //修改坦克的坐标 y - 1            hero.moveUp();  
        } else if (e.getKeyCode() == KeyEvent.VK_D) {//按下D键  
            hero.setDirect(1);  
            hero.moveRight();  
        } else if (e.getKeyCode() == KeyEvent.VK_S) {//按下D键  
            hero.setDirect(2);  
            hero.moveDown();  
        } else if (e.getKeyCode() == KeyEvent.VK_A) {//按下A键  
            hero.setDirect(3);  
            hero.moveLeft();  
        }  
  
        //让面板重绘  
        this.repaint();  
    }  
  
    @Override  
    public void keyReleased(KeyEvent e) {  
  
    }}
```

#### 14.5.3.4 Tank.java

```
package com.tank.tankgame2;  
  
/**  
 * @author 陈文臻  
 */  
public class Tank {  
    private int x;//坦克的横坐标  
    private int y;//坦克的纵坐标  
    private int direct;//坦克方向 上：0 右1 下2 左3  
    private int speed = 1;  
  
    //上右下左移动方法  
    public void moveUp() {  
        y -= speed;  
    }  
  
    public void moveRight() {  
        x += speed;  
    }  
  
    public void moveDown() {  
        y += speed;  
    }  
  
    public void moveLeft() {  
        x -= speed;  
    }  
  
  
    public Tank(int x, int y) {  
        this.x = x;  
        this.y = y;  
    }  
  
    public int getDirect() {  
        return direct;  
    }  
  
    public void setDirect(int direct) {  
        this.direct = direct;  
    }  
  
    public int getSpeed() {  
        return speed;  
    }  
  
    public void setSpeed(int speed) {  
        this.speed = speed;  
    }  
  
    public int getX() {  
        return x;  
    }  
  
    public void setX(int x) {  
        this.x = x;  
    }  
  
    public int getY() {  
        return y;  
    }  
  
    public void setY(int y) {  
        this.y = y;  
    }  
}
```

#### 14.5.3.5 TankGame02.java

```
package com.tank.tankgame2;  
  
/**  
 * @author 陈文臻  
 */  
public class Tank {  
    private int x;//坦克的横坐标  
    private int y;//坦克的纵坐标  
    private int direct;//坦克方向 上：0 右1 下2 左3  
    private int speed = 1;  
  
    //上右下左移动方法  
    public void moveUp() {  
        y -= speed;  
    }  
  
    public void moveRight() {  
        x += speed;  
    }  
  
    public void moveDown() {  
        y += speed;  
    }  
  
    public void moveLeft() {  
        x -= speed;  
    }  
  
  
    public Tank(int x, int y) {  
        this.x = x;  
        this.y = y;  
    }  
  
    public int getDirect() {  
        return direct;  
    }  
  
    public void setDirect(int direct) {  
        this.direct = direct;  
    }  
  
    public int getSpeed() {  
        return speed;  
    }  
  
    public void setSpeed(int speed) {  
        this.speed = speed;  
    }  
  
    public int getX() {  
        return x;  
    }  
  
    public void setX(int x) {  
        this.x = x;  
    }  
  
    public int getY() {  
        return y;  
    }  
  
    public void setY(int y) {  
        this.y = y;  
    }  
}
```