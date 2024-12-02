# 1. 基础语法

## 1.1 字面量

字面量：在代码中，被写下来的固定的值  
_**常用的六种值（数据）：数字、字符串、列表、远足、集合、字典**_

### 1.1.1 字符串

字符串：又称文本，是由任意数量的字符如中文、英文、各类符号、数字组成的  
例如：  
"黑马程序员"  
"！@#¥%……"  
"股票代码：19837"

**python中，字符串需要用双引号（" "）包围起来，被双引号包围起来的，都是字符串**

```
666    [[整数]]
13.14   [[浮点数]]
"我是字符串"    [[字符串]]

print(666)
print(13.14)
print("我是字符串")
```

## 1.2 注释

- 单行注释：以**#开头**，**#右边**的所有文字当作说明，而不是真正要执行的程序，起辅助说明作用

```
# 我是单行注释
printt("Hello world")
```

**注意，#号和注释内容一般建议以一个空格隔开**

- 多行注释：以 **一对三个双引号** 引起来 （"""注释内容"""）来解释说明一段代码的作用使用方法

```
"""
    我是多行注释
    诗名：悯农
    作者：李绅
"""

print("锄禾日当午")
print("汗滴禾下土")
print("谁知盘中餐")
print("粒粒皆辛苦")
```

## 1.3 变量

变量：程序运行时，能储存计算结果或能表示值的抽象概念  
作用：记录数据（理解为"盒子"）

定义格式：`变量名称=变量的值`  
1.每一个变量都有自己存储的值（内容），成为变量值  
2.赋值，表示将等号右侧的值，赋予左侧的变量  
3.每一个变量都有自己的名称，称之为：变量名，也就是变量本身

```
# 定义一个变量，用来记录钱包余额
money = 50

# 通过print语句，输出变量记录的内容
print("钱包还有：",money)

# 买一个冰淇凌，话费10元
money = money - 10
print("买冰淇淋话费10元，还剩余：",money,"元")

# 假设，每隔一小时，输出钱包的余额
print（"现在是下午1点，钱包余额剩余："，money）
print（"现在是下午2点，钱包余额剩余："，money）
print（"现在是下午3点，钱包余额剩余："，money）
print（"现在是下午4点，钱包余额剩余："，money）
```

## 1.4 数据类型

在字面量时学习到，数据是有类型的  
主要接触一下三种类型：

## 1.5 string  字符串

yes

## 1.6 int    整型（有符号）

yes  
float   浮点型（有符号）

- type（）语句使用方式  
    1.在print语句中，直接输出类型信息

```
print(type("我是字符串"))
print(type(666))
print(type(13,14))
```

2.用变量存储type()的结果(返回值)：

```
string_type = type("我是字符串")
int_type = type(666)
float_tyoe = type(13.14)

print(string_type)
print(int_type)
print(float_type)
```

**上述为type()语句查找字面量类型的语句，type()当然也可以查找变量中的语句**

```
name = "黑马程序员"
name_type = type(name)
print(name_type)
```

**type(变量)查看的是变量存储的数据的类型。因为变量无类型，但他存储的数据有**

## 1.7 数据类型的转换

类型转换，将会是我们以后经常使用的功能：  
1.从文件中读取的数字，默认是字符串，我们需要转换成数字类型  
2.后续学习的input()语句，默认结果是字符串，若需要数字也需要转换  
3.将数字转换成字符串用以写出到外部系统

int(x)    将x转换成一个整数  
float(x)   将x转换成一个浮点数yes  
str(x)    将对象x转换为字符串

```
# 将数字类型转换成字符串
num_str = str(11)
print(type(num_str),num_str)

float_str = str(11.34)
print(type(float_str),float_str)

# 将字符串转换成数字
num = int("11")
print(type(num),num)
```

**万物皆可转字符串，字符串转数字需要字符串内容都是数字**

## 1.8 标识符

在python程序中，我们可以给很多东西起名字，比如：

- 变量的名字
- 方法的名字
- 类的名字  
    这些名字，我们统一把它称为标识符，用来做内容的标识

标识符：是用户在编程的时候所使用的一系列名字，用于给变量、类、方法等命名  
标识符命名的三类规则：

- 内容限定  
    标识符的命名中，只允许出现：  
    1.英文  
    2.中文  
    3.数字  
    4.下划线  
    注：1.不推荐使用中文   2.数字不可以开头
- 大小写敏感
- 不可使用关键字  
    大小写敏感同样适合于关键字

变量的命名规范：  
1.见名知意：明了，简洁  
2.下划线命名法：first_number  
3.英文字母全小写

## 1.9 运算符

### 1.9.1 算数运算符

进行做数学运算的运算符：+ - * / // % **

```
# 算数（数学）运算符

# 加号运算符
print("1 + 1 =", 1 + 1)
# 减号运算符
print("2 - 1 =", 2 - 1)
# 乘号运算符
print("3 * 3 =", 3 * 3)
# 除号运算符
print("4 / 2 =", 4 / 2)
# 取整除运算符
print("11 // 2 =", 11 // 2)
# 取余运算符
print("9 % 2 =", 9 % 2)
# 指数运算符
print("2 ** 2 =", 2 ** 2)
```

### 1.9.2 赋值运算符

进行赋值的运算符：= += -= *= /= %= **= //=

```
# 赋值运算符
num = 1 + 2 * 3

[[符合赋值运算符]]
num = 1
num += 1 [[num]] = num + 1
num -= 1
num *= 4
```

## 1.10 字符串的扩展

### 1.10.1 字符串的三种定义方式

1.单引号定义法：'我是字符串'/可以内含双引号  
2.双引号定义法："我是字符串"/可以内含单引号  
3.三引号定义法："""我是字符串"""/可以用转义字符\将引号的效用解除

三引号定义法和多行注释的写法一样，同样支持换行操作。  
如果变量接受它，他就是字符串，不使用变量接收它，他就可以作为多行注释使用

```
# 单引号定义法
name = '我是字符串'
# 双引号定义法
name = "我是字符串"
# 三引号定义法
name = """我是字符串"""
name = """ 
我是
黑马
程序员
"""
# 在字符串内 包含双引号
name = '"我是字符串"'
# 在字符串内 包含单引号
name = "'我是字符串'"
# 在字符串内 使用转义字符\解除引号的效用
name = "\"我是字符串\""
name = '\'我是字符串\''
```

### 1.10.2字符串拼接

如果有两个字符串（文本）字面量，可以将其拼接成一个字符串，通过加号完成，如

```
# 字符串字面量之间的拼接
print("我是" + "字符串")
# 字符串字面量和字符串变量的拼接
name = "我是"
address = "字符串"
print("我是：" + name + "，我的地址是：" + address)
```

**拼接操作只适合字符串本身，只能进行字符串间的拼接操作**

### 1.10.3 字符串格式化1

拼接字符串也不好用：  
1.变量过多，拼接起来实在是太麻烦  
2.字符串无法和数字或其他类型完成拼接  
解决方法：字符串格式化

```
name = "字符串"
message = "我是 %s" % name
print(message)
```

其中的，%s

- %表示：我要占位
- s表示：将变量变成字符串放入占位的地方  
    所以，综合起来的意思就是：我先占个位置，等一会有个变量过来，我把它变成字符串放到占位的位置

```
class_num = 57
avg_salary = 16781
# 多个变量占位 变量要用括号括起来 并按照占位的顺序填入
message = "Python大数据科学，北京%s期，毕业平均工资：%s" % (class_num,avg_salary)
print(message)
```

python中，支持非常多的类型占位：

- 格式符号：%s    将内容转换成字符串，放入占位位置

---

- 格式符号：%d    将内容转换成整数，放入占位位置

---

- 格式符号：%f    将内容转换成浮点型，放入占位位置

```
name = "传智播客"
setup_year = 2006
stock_price = 19.99
message = "%s,成立于：%d,我今天的股价是：%f" % (name, setup_year, stock_price)
print(message)
```

### 1.10.4 格式化精度控制

我们可以使用辅助符号 **"m.n"** 来控制数据的宽度和精度

- 控制宽度，要求数字（很少使用），**设置的宽度小于数字自身，不生效**
- 控制小数点精度，要求是数字，**会进行小数的四舍五入**  
    示例：
- %5d：表示将整数的宽度控制在五位，如数字11，被设置为5d，就会变成[空格][空格][空格]11，用三个空格补足宽度
- %5.2f：表示将宽度控制为5，将小数点精度设置为2  
    小数点和小数部分也算入宽度计算。如，对11.345设置了%7.2f后，结果是：[空格][空格]11.35。两个空格不足宽度，小数部分限制2位精度后，四舍五入为.35
- %.2f：表示不限制宽度，只设置小数点精度为2，如11.345设置%.2f后，结果是11.35

```
num1 = 11
num2 = 11.345
print("数字11宽度限制5，结果是：%5d" % num1)
print("数字11宽度限制1，结果是：%1d" % num1)
print("数字11.345宽度限制7，结果是：%7.2f" % num2)
print("数字11.345宽度不限制，小数精度2，结果是：%.2f" % num2)
```

### 1.10.5 字符串格式化2

语法:f"内容{变量}"的格式来快速格式化

```
name = "传智博客"
set_up_year = 2006
stock_price = 19.99
print(f"我是{name}，我成立于：{set_up_year},我今天的股票价格是：{stock_price}")
# 该方式不做精度控制，原样输出（适合对精度无要求的快速使用）
```

### 1.10.6 对表达式进行格式化

表达式：一条有明确执行结果的代码语句  
如：  
1+1、5*2  
name = "张三"、age = 11+4

对于字符串格式化，可以直接格式化一个表达式：

```
print("1*1的结果是：%d" % （1*1))
print(f"1*2的结果是：{1*2}")
print("字符串在python中的类型名是：%s" % type("字符串"))
```

如何格式化表达式：

- f"{表达式}"
- "%s%d%f % (表达式、表达式、表达式)

## 1.11 数据输入

input语句(函数)  
在python中，与之对应的还有一个input语句，用来获取键盘输入

- 数据输出：print
- 数据输入：input  
    使用也很简单：
- 使用input()语句可以从键盘获取输入
- 使用一个变量接收(存储)input语句获取的键盘输入数据即可

```
print("请告诉我你是谁")
name = input()
print("我是%s"，name)

num = input("请告诉我你的应行卡密码：")
```

**无论键盘输入什么类型的数据，接收到的数据永远都是字符串类型**

# 2. 判断语句

## 2.1 布尔类型和比较运算符

### 2.1.1 布尔类型

布尔类型的字面量：

- True表示真（是、肯定）
- False表示假(否，否定)

定义变量存储布尔类型数据：  
变量名称 = 布尔类型的字面量：

### 2.1.2 比较运算符

比较运算符：== != > < >= <=

```
# 定义变量存储布尔类型的数据
bool_1 = True
bool_2 = False
print(f"bool_1变量的内容是:{bool_1},类型是:{type(bool_1)}")
# 比较运算符的使用
# == , ！= , < , > , <= , >=
num1 = 10
num2 = 10
print(f"10等==10的结果是:{num1 == num2}")
```

## 2.2 if语句的基本格式

if 要判断的条件：  
条件成立时，要做的事情

```
age = 30

if age >= 18:
    print("我已经成年了")
```

## 2.3 if else语句

程序中的判断：  
if 条件：  
满足条件时要做的事情1  
…………  
else：  
不满足条件时要做的事情1  
…………

```
print("欢迎来到黑马儿童游乐场")
age = input("请输入你的年龄")
if age >= 18:
    print("您已成年，需要买票10元")
else:
    print("您未成年，不需要买票")
```

## 2.4 if elif else语句

作用：完成多个条件的判断  
注意点：  
1.elif可以写多个  
2.判断时互斥且有序，上一个满足后面就不会判断了  
3.可以在条件判断中，直接写input语句，节省代码量

程序中的判断：  
if 条件1:  
……  
elif 条件2:  
……  
elif 条件N：  
……  
else：  
……

```
height = int(input("请输入你的身高(cm)"))
vip_level = int(input("请输入的vip等级"))

# 通过if判断，可以使用多条件判断语法
# 第一个条件就是if
if height < 120:
    print("身高小于120cm,可以免费")
elif vip_level > 3:
    print("vip等级大于3，可以免费")
else：
    print("条件都不满足，需要买票")
```

## 2.5 判断语句的嵌套

基础语法格式如下：  
if 条件1:

```
满足条件1 做的事情1
满足条件2 做的事情2

if条件2:
    满足条件2 做的事情1
    满足条件2 做的事情2
```

```
if int(input("你的身高是多少：")) > 120:
    print("身高超出限制，不可以免费)
    
    if int(input("你的vip级别是多少：")) > 3:
        print("恭喜你，vip级别达标，可以免费")
    else:
        print("sorry，你需要买票")
else：
    print("欢迎小朋友免费游玩")
```

# 3. 循环语句

## 3.1 while循环的基础语法

程序中的循环：  
while 条件：  
条件满足时，做的事情1  
条件满足时，做的事情2  
…………

```
i = 0
while i < 100:
    print("小美，我喜欢你")
    i +=1
```

1.while的条件需要布尔类型，True表示继续循环，False表示结束循环  
2.需要设置循环终止的条件，如i += 1配合i < 100,就能确保100次后停止，否则将无限循环  
3.空格缩进和if判断一样，都需要设置

## 3.2 while循环的嵌套应用

程序中饭的循环：  
while 条件1：  
…………

```
while 条件2:
…………
```

```
# 外层：表白100天的控制
# 内层：每天表白都送10只玫瑰花的控制

i = 1
while i <= 100:
    print(f"今天是第{i}天，准备表白……")

    # 内层循环的控制变量
    j = 1
    while j <= 10
        print(f"送给小美第{j}只玫瑰花")
        j += 1

    print("小美，我喜欢你")
    i += 1

print(f"坚持到第{i-1}天，表白成功")
```

## 3.3 for循环的基础语法

### 3.3.1基础语法

while 和 for 循环功能基本差不多，但仍然有一些区别：

- while循环的循环条件是自定义的，**自行控制循环条件**
- for循环是一种"**轮询**"机制，是对一批内容进行"**逐个处理**"

for循环就是将"待办事项"逐个完成

程序中的for循环  
for 临时变量 in 待处理数据集：  
循环满足条件时的执行语句

```
name = "itheima"

for x in name:
    # 将name的内容，挨个取出赋予x临时变量
    # 就可以在循环体内对x进行处理
    print(x)
```

可以看出，for循环是将字符串的内容：**依次取出**  
所以，for循环也被称之为：**遍历循环**

注意点：  
1.同while循环不同，for循环是无法定义循环条件的。只能从被处理的数据集中，依次取出内容进行处理。所以，for无法进行无限循环

### 3.3.2 range语句

fot 临时变量 in 待处理数据集：  
循环满足条件时的执行语句

语法中的：待处理数据集，严格来说，称之为：**序列类型**  
序列类型指的，其内容可以一个个依次取出的一种类型，包括：

- 字符串
- 列表
- 元组

for循环语句，本质上是遍历：序列类型

语法1:  
range(num)  
获取一个从0开始，到num结束的数字序列(不含num本身)  
如range(5)取得的数据是：[0,1,2,3,4]

语法2:  
range(num1, num2)  
获得一个从num1开始，到num2结束的数字序列(不含num2本身)  
如，range(5, 10)取得的数据是：[5,6,7,8,9]

语法3:  
range(num1, num2, step)  
获得一个从num1开始，到num2结束的数字序列(不含num2本身)  
数字之间的步长，以step为准（step默认为1）  
如，range(5,10,2)获得的数据是：[5,7,9]

```
# range 语法1 range(num)
for x in range(10):
    print(x)

# range 语法2 range(num1, num2)
for x in range(5, 10):
    # 从5开始买到10结束（不包含10本身）的一个数字序列,数字之间的间隔是1
    print(x)

# range 语法3 range(num1, num2, step)
for x in range(5, 10, 2)
    [[从5开始，到10结束（不包含10本身）的一个数字序列，数字之间的间隔是2]]
    print(x)
```

```
i=1
while i <= 10:
    print("送玫瑰花")
    i += 1

for x in range(10)
    print("送玫瑰花")
```

### 3.3.3 变量作用域

for 临时变量 in 待处理数据集：  
循环满足条件时的执行语句

临时变量，在编程规范上，作用范围(作用域)，只限定在for循环内部

如果在for循环外部访问临时变量：

- 实际上是可以访问的
- 在编程规范上，是不允许、不建议这么做的

```
i = 0
for i in range(5)
    print(i)
# 在for外定义变量i就可以进行for外的规范输出
print(i)
```

## 3.4 for循环的嵌套应用

程序中的嵌套for循环：  
for 临时变量 in 待处理数据集(序列)：  
…………  
for 临时变量 in 待处理数据集(序列）：  
…………

```
# 坚持表达100天，每天都送10朵花
# range 

i = 0
for i in range(1,101):
    print(f"今天是向小美表白的第{i}天，加油坚持。")

    # 写内存的循环
    for j in range（1,11):
        print(f"给小美送的第{j}朵玫瑰花")
    
    print("小美我喜欢你")

print(f"第{i}天，表白成功')
```

for循环和while循环可以相互嵌套

## 3.5 循环中断

### 3.5.1 continue

continue关键字用于：中断本次循环，直接进入下一次循环  
continue可以用于：for循环和while循环，效果一致

for i in range(1,100)  
语句1  
continue  
语句2

- 在循环内，遇到continue就结束当次循环，进行下一次
- 所以，**语句二不会执行**

应用场景：在循环中，因某些原因，临时结束本次循环

```
for i in range(1,6)
    print("语句1")
    continue
    print("语句2")
# 输出结果：5次语句1
```

### 3.5.2 continue在嵌套循环中的应用

continue关键字只可以控制：它所在的循环临时中断  
for i in range(1,100):  
语句1  
for j in range(1,100):  
语句2  
continue  
语句3  **语句3不能执行**  
语句4

```
for i in range(1,6):
    print("语句1")
    for j in range(1,6):
        print("语句2")
        continue
        print("语句3")

    print("语句3")

    [[输出结果]] （1个语句1，5个语句2，1个语句4）x5
```

### 3.5.3 break

break关键字用于：直接结束循环  
break可以用于：for循环和while循环，效果一致

for i in range(1,100):  
语句1  
break  
语句2  
语句3

- 在循环内，遇到break就结束循环了
- 所以，执行语句1后，直接执行语句3

```
for i in range(1,101):
    print("语句1")
    break
    print("语句2")

print("语句3")
```

## 3.6 break在嵌套中的应用

break关键字同样只可以控制：它所在的循环结束

for i in range(1,100):  
语句1  
for j in range(1,100):  
语句2  
break  
语句3

```
语句4
```

```
for i in range(1,6):
    print("语句1")
    for j in range(1,6):
        print("语句2")
        break 
        print("语句3")

    print("语句4")
```

# 4. 函数

## 4.1 函数介绍

函数：是组织好的，可重复使用的，用来实现特定功能的代码段

name = "iheimai"  
length = len(name)  
print(length)

因为，len()是python内置的函数：

- 是提前写好的
- 可以重复使用的
- 实现统计长度这一特定功能的代码段

```
# 需求统计字符串的长度，不使用内置函数len()
str1 = "itheima"
str2 = "itcast"
str3 = "python"

# 定义一个计数的变量
count = 0 
for i in str1:
    count += 1
print(f"字符串{str1}的长度是:{count}")

count = 0 
for i in str2:
    count += 1
print(f"字符串{str2}的长度是:{count}")

count = 0 
for i in str3:
    count += 1
print(f"字符串{str3}的长度是:{count}")

# 可以使用函数，来优化这个过程
def my_len(data):
    count = 0
    for i in data:
        count += 1
    print(f"字符串{data}的长度是{count}")

my_len(str1)
my_len(str2)
my_len(str3)
```

函数特性：  
1.已组织好的  
2.可以重复使用的  
3.针对特定功能

## 4.2 函数的定义

函数的定义：  
def 函数名(传入参数):  
函数体  
return 返回值(可省略)

函数的调用：  
函数名(参数)

注意事项：  
1.参数如不需要，可以省略  
2.返回值如不需要，可以省略  
3.函数必须先定义后使用

```
# 定义一个函数，输出相关信息
def say_hi():
    print("hi 我是黑马程序员")

# 调用函数，让定义的函数开始工作
say_hi()
```

## 4.3 函数的参数

传入参数的功能：在函数进行计算的时候，接受外部(调用时)提供的数据

基于函数的定义语法：  
def 函数名(传入参数)：  
函数体  
return 返回值如不需要，可以省略

可以有如下函数定义：  
def add(x, y)  
result = x + y  
print(f"{x} + {y}的结果是：{result}")

```
# 定义2数相加的函数，通过参数接收被计算的2个数字
def add(x, y)
    result = x + y
    print(f"{x} + {y}的计算结果是：{result}")

# 调用函数，传入被计算的2个数字
add(5,6)

[[输出结果：11]]
```

- 函数定义中，提供的x和y，称之为：形式参数(形参)，表示函数声明将要使用2个参数

- 参数之间使用逗号进行分隔

- 函数调用中，提供的5和6，称之为：实际参数（实参），表示函数执行时真正使用的参数值

- 传入的时候，按照顺序传入数据，使用逗号分隔

传入参数的数量是不受限制的

- 可以不使用参数
- 也可以仅使用任意N个参数

## 4.5 函数的返回值

### 4.5.1 函数返回值的定义语法

程序中的返回值：  
def add(a,b):  
result = a + b  
return result

r = add(1, 2)  
print(r)

返回值就是程序中函数完成事情后，最后给调用者的结果

语法格式：  
def 函数（参数...):  
函数体  
return 返回值

变量 = 函数（参数）

语法：通过return关键字，就能向调用者返回数据

```
# 定义一个函数，完成2数相加功能
def add(a, b):
    result = a + b
    return result
    # 通过返回值，将相加的结果返回给调用者
    return result 
    [[return后面的代码不执行]]


# 函数的返回值，可以通过变量去接收
r = add(5, 6)
print(r)

# 输出结果：11
```

### 4.5.2None类型

None作为一个特殊的字面量，用来表示：空、无意义，其有非常多的应用场景

- 用在函数无返回值上
- 用在if判断上

- 在if判断中，None等同于False
- 一般用于在函数中主动返回None，配合if判断做相关处理

- 用于声明无内容的变量上

- 定义变量，但暂时不需要变量有具体的值，可以用None来代替  
    **暂不赋予变量具体值**  
    name = None

```
# 无return语句的函数返回值
def say_hi():
    print("你好鸭")

result = say_hi()
print(f"无返回值函数，返回的内容是：{result}")

# 主动返回None的函数
def say_hi2():
    print("你好鸭")

result = say_hi()
print(f"无返回值函数，返回的内容是：{result}")

# 两者返回效果相同，输出效果相同

# None用于if判断
def check_age(age):
    if age > 18:
        return "Success"
    else:
        return None 

result = check_age(16)
if not result:
    # 进入if表示result时None值，也就是False值
    print("未成年，不可以进入")
```

## 4.6 函数说明文档

函数是纯代码语言，可以给函数添加说明文档，辅助理解函数的作用

语法如下：  
def func(x, y):  
"""  
函数说明  
:param x: 形参x的说明  
:param y: 形参y的说明  
:return : 返回值的说明  
"""  
函数体  
return 返回值

内容写在函数体之前

```
def add(x, y):
    """
    add函数可以接收2个参数，进行2数相加的功能
    :param x: 形参x的说明
    :param y: 形参y的说明
    :return : 返回值是2数相加的结果
    """

    result = x + y 
    print(f"2数相加的结果是:{result}")
    return result
```

## 4.7 函数的嵌套调用

函数的嵌套调用：一个函数里面又调用了另外一个函数

```
# 定义函数func_b
def func_b():
    print("---2---")
# 定义函数func_a,并在内部调用func_b
def func_a():
    print("---1---")

    # 嵌套调用func_b
    func_b()

    print("---3---")
```

### 4.7.1 变量的作用域

变量的作用域指的是变量的作用范围（变量在哪里可用，在哪里不可用）  
主要分为两类：局部变量和全局变量

### 4.7.2 局部变量

所谓局部变量是定义在函数体内部的变量，即只在函数体内部生效

```
def testA():
    num = 100
    print(num)

testA()     # 100
print(num)    # 报错：name'num'is not defined
```

变量a是定义在`testA`函数内部的变量，在函数外访问则立即报错

**局部变量的作用：**在函数体内部，临时保存数据数据，函数调用完成立刻销毁局部变量

### 4.7.3 全局变量

所谓全局变量，指的是在函数体内、外都能生效的变量

```
# 定义全局变量a
num = 100

def testA():
    print(num)  # 访问全局变量num，并打印变量num存储的数据


def testB():
    print(num)  # 访问全局变量num，并打印变量num存储的数据

testA()
testB()
```

### 4.7.4 global关键字

```
# 在函数内修改全局变量
num = 200

def test_a():
    print(f"test_a:{num}")

def test_b():
    global num  # 设置内部定义的变量为全局变量
    num = 500   # 局部变量
    print(f"test_b:{num}")

test_a()
test_b()
print(num)
```

## 4.8 函数多返回值

```
def test_return()
    return 1, 2

x, y = test_return()
print(x)        # 结果1
print(y)        # 结果2
```

按照返回值的顺序，写对应顺序的多个变量接收即可  
变量之间用逗号隔开  
支持不同类型的数据return  
返回数据类型不受限

## 4.9 函数的多种传参方式

### 4.9.1 位置参数

位置参数：调用函数时根据函数定义的参数位置来传递参数  
注意：传递的参数和定义的参数的顺序及个数必须一致

### 4.9.2 关键字参数

关键字参数：函数调用时通过"键=值"形式传递参数  
作用：可以让函数更加清晰、容易使用，同时也清除了参数放入顺序需求  
注意：函数调用时，如果有位置参数时，位置参数必须在关键字参数的前面，但关键字参数之间不存在先后顺序

```
def user_info(name, age, gender)：
    print(f"姓名是：{name}, 年龄是：{age}, 性别是:{gender}")
# 位置参数 - 默认使用形式   
user_info('小明'， 20， '男')
# 关键字参数 
user_info(name="小明", age = 20, gender = "男") # 可以不按照参数的定义顺序传参
```

### 4.9.3 缺省参数

缺省参数：缺省参数也叫默认参数，用于定义函数，为参数提供默认值，调用函数时不传该默认参数的值(注意：所有位置参数必须出现在默认参数前，包括函数定义和调用)  
作用：当调用函数时没有传递参数，就会使用默认是用缺省参数对应的值

```
def user_info(name, age, gender='男')   # 默认参数必须写在最后
    print(f"姓名是：{name}, 年龄是：{age}, 性别是：{gender}")

user_info('小天'， 13)
user_info('小天，13, gender = '女')
```

### 4.9.4 不定长参数

不定长参数：不定长参数也叫可变参数，用于不确定调用的时候会传递多少个参数(不传参也可以)的场景  
作用：当调用函数时不确定参数个数时，可以使用不定长参数

不定长参数的类型：  
1.位置传递  
注意：传进的所有参数都会被args变量收集，它会根据传进参数的位置合并为一个元组(tuple),args是元组类型，这就是位置传递

2.关键字传递  
注意：参数是"键=值"形式的形式的情况下，所有的"键=值"都会被kwargs接收，同时会根据"键=值"组成字典

```
# 不定长 - 位置不定长，*号
# 不定长定义的形式参数作为元组存在，接收不定长数量的参数传入
def user_info(*args):
    print(f"args参数的类型是:{type(args)}, 内容是:{args"})

user_info(1, 2, 3, '小明', '男孩')

# 不定长 - 关键字不定长，**号
def user_info(**kwargs):
    print(f"args参数的类型是：{type(kwarg)}, 内容是：{kwargs}")

user_info(name = '小王', age = 11, gender = '男孩')
```

## 4.10 匿名函数

### 4.10.1 函数作为参数传递

**计算逻辑的传递，而非数据的传递**

```
# 定义一个函数，接收另一个函数作为传入参数
def test_func(computer):
    result = compute(1, 2)  # 确定compute是函数
    print(f"compute参数的类型是:{type(compute)}")
    print(f"计算结果：{result}")

# 定义一个函数，准备作为参数传入另一个函数
def compute(x, y)
    return x + y

# 调用并传入函数
test_func(compute)
```

### 4.10.2 lanbda匿名函数

函数的定义中

- def关键字中，可以定义待遇名称的函数
- lambda关键字，可以定义匿名函数(无名称)  
    有名称的函数，可以基于名称重复使用  
    无名称的匿名函数，只可以临事使用依次

匿名函数定义语法：  
**lambda 传入参数： 函数体(一行代码)**

- lambda是关键字，表示定义匿名函数
- 传入参数表示匿名函数的形式参数，如：x，y表示接收两个形式参数
- 函数体，就是函数的执行逻辑，要注意：只能写一行，无法写多行代码

```
# 定义一个函数，接受其他函数输入
def test_func(compute):
    result = compute(1, 2)
    print(f"结果是:{result}")
# 通过lambda匿名函数的形式，将匿名函数作为参数传入
test_func(lambda x, y:x + y)
```

# 5. 数据容器

## 5.1 数据容器入门

python中的数据容器：  
一种**可以容纳多份数据的数据**类型，容纳的每**一份数据称之为一个元素**。  
每一个元素可以是**任意类型**的数据，如字符串、数字、布尔

数据容器根据特点的不同，如：

- 是否支持重复元素
- 是否可以修改
- 是否有序  
    分为5类，分别是：  
    列表(list)、元组(tuple)、字符串(str)、集合(set)、字典(dict)

## 5.2 数据容器：list列表

### 5.2.1 列表的定义

列表的定义：  
基本语法：

```
# 定义一个列表 list
["ltheima","itcast", "python"]
# 定义一个变量
my_list = ["ltheima", "itcast", "python"]
print(my_list)
print(type(my_list)) # 类型是list
# 每一份元素可以是任意数据类型
my_list = ["itheima", 666, True]

# 定义一个嵌套的列表
my_list = [[1, 2], [3, 4], [5, 6]
```

### 5.2.2 列表的下标索引

```
my_list = ["Ton", "Lily", "Rose']
# 列表[下标索引]，从前向后从0开始，每次+1   从后向前从-1开始，每次-1
print(my_list[0])
# 如果超出范围将会报错
print(my_list[-3])

# 取出嵌套列表的元素
my_list = [[1,2,3],[4,5,6]]
print(my_list[1][2])
```

## 5.3列表的常用操作

列表的功能：

- 定义
- 使用下标索引获取值
- 插入元素
- 删除元素
- 清空列表
- 修改元素
- 统计元素个数  
    这些功能我们都称之为：**列表的方法**  
    方法的使用：student = Student()  
    num = student.add(1,2)
- 查找某元素下标  
    功能：查找指定元素在列表的下标，如果找不到，报错ValueError  
    语法：列表.index(元素)  
    **index就是列表对象(变量)内置的方法(函数)**
- 修改特定位置(索引)的元素值  
    语法：列表[下标]=值  
    可以使用如上语法，直接对指定下标(正向、反向下标均可)的值进行：重新赋值(修改)
- 插入元素  
    语法：列表.insert(下标、元素)，在指定的下标位置，插入指定的元素
- 追加元素(单个)  
    语法：列表.append（元素），将指定元素，追加到列表尾部
- 追加元素（一批）  
    语法：列表.extend（其他数据容器），将其他数据容器的内容取出，依次追加到列表尾部
- 删除元素  
    语法1：del 列表 [下标]  
    语法2:列表.pop（下标）
- 删除某元素在列表中的第一个匹配项  
    语法：列表.remove(元素)
- 清空列表  
    语法：列表.clear()
- 统计某元素在列表内的数量  
    语法：列表.count(元素)
- 统计列表内，有多少元素  
    语法：len(列表)

```
my_list = ["itheima", "itcast", "python"]
# 1.1查找某元素在列表内的下标索引
index = my_list.index("itheima")
print(f"itheima在列表的下标索引值是：{index}")
# 1.2如果被查找的元素不存在，会报错
# 2.修改特定下标索引的值
my_list[0] = "传智教育"
print(f"列表被修改结果后：{my_list}")
# 3.在指定下标位置插入新元素
my_list.insert(1, "best")
print(f"列表插入元素后，结果是：{my_list}")
# 4.在列表的尾部追加单个新元素
my_list.append("黑马程序员")
# 5.在列表的尾部追加一批新的元素
mylist2 = [1, 2, 3]
my_list.extend(mylist2)
# 6.删除指定下标索引的元素（2种方式）
my_list = ["itcast", "itheima", "python"]
# 6.1方式1:del 列表[下标]
del my_list[2]
# 6.2方式2:列表.pop(下标)
element = my_list.pop(2)
# 7.删除某元素在列表中的第一个匹配项
mylist.remove("itheima")
# 8.清空列表
my_list.clear()
# 9.统计列表内某元素的数量
count = my_list.count("itheima")
# 10.统计列表内全部的元素数量
count = len(my_list)
```

## 5.4 list的遍历

将容器内的元素依次取出的进行处理的行为，称之为：遍历，迭代  
在使用场景时：

- while循环适用于任何想要循环的场景
- for循环适用于，遍历数据容器的场景或简单的固定次数循环场景

### 5.4.1 while循环遍历

index = 0  
while index < len(列表)：  
元素 = 列表[index]  
对元素进行处理  
index += 1

```
my_list = ["传智教育"， "黑马程序员"， "python"]
# 循环控制变量通过下标索引来控制，默认0
# 每一次循环将下标索引变量+1
# 循环条件：下标索引变量 < 列表的元素数量

# 定义一个变量用来标记列表的下标
ibdex = 0           # 初始值为0
while index < len(my_list)
    # 通过index变量取出对应下标的元素
    element = my_list[index]
    print("列表的元素：{element}")
    # 至关重要 将循环变量(index)每一次循环都+1
    index += 1
```

### 5.4.2 for循环遍历

```
my_list = [1, 2, 3, 4, 5]
for element in my_len
    print(f"列表的元素有：{element}")
```

## 5.5 数据容器：tuple元组

列表传递信息，可以修改。元祖一旦定义完成，就不可以修改

### 5.5.1 定义元组

元组定义：定义元组使用小括号，且使用逗号隔开各个数据，数据可以是不同数据类型  
注意事项：**如果元组只有一个数据，这个数据后面要添加逗号**  
t1 = ("hello", )  
元组也支持嵌套

```
# 定义元组
t1 = (1, "hello", True)
t2 = ()
t3 = tuple()
# 定义单个元素的元组
t4 = ("Hello", )
# 元组的嵌套
t5 = ((1, 2, 3), (4, 5, 6))
# 下标索引取出内容
t5[1][2]
```

### 5.5.2 元组的操作

- index()
- count()
- len(元组)
- 不可修改元组的内容，否则会直接报错
- 可以修改元组内的list的内容(修改元素、增加、删除、反转)

```
t1 = (1, 2, ["itheima", "itcast"])
t1[2][0] = "黑马程序员"
t1[2][1] = "传智教育"
```

## 5.6 数据容器：str字符串

字符串是字符的容器，一个字符串可以存放任意数量的字符

同元组一样，字符串是一个：**无法修改**的数据容器  
所以：

- 修改指定下标的字符        (如：字符串[0] = "a")
- 移除特定下标的字符        (如：del字符串[0]、字符串.remove、字符串.pop)
- 追加字符                (如：字符串.append())  
    **均无法完成。如果必须要做，只能得到一个新字符串**

```
my_str = "itheima and itcast"
# 通过下标索引取值
value = my_str[2]
value2 = my_str[-16]
```

### 5.6.1 字符串的常用操作

- 查找特定字符串的下标索引值  
    语法：字符串.index(字符串)
- 字符串的替换  
    语法：字符串.replace(字符串1，字符串2)  
    功能：将字符串内的全部：字符串1替换为字符串2  
    注意：不是修改字符串本身，而是得到一个新的字符串
- 字符串的分隔  
    语法：字符串.spilt(分隔符字符串)  
    功能：按照指定的分隔符字符串，将字符串划分为多个字符串，并存入对象中  
    注意：字符串本身不变，而是得到了一个列表对象
- 字符串的规整操作(去前后空格)  
    语法:字符串.strip()
- 字符串的规整操作(去前后指定字符串)  
    语法：字符串.strip(字符串)
- 统计字符串中某字符串出现的次数  
    语法：字符串.count(字符串)
- 统计字符串的长度  
    语法：len(字符串)

```
my_str = "itheima and itcast"
# index方法
value = my_str.index("and")
# replace方法
new_my_str = my_str.replace("it","程序")
# split方法
my_str = "hello python itheima itcast"
my_str_list = my_str.split(" ")
# strip方法
my_str = "  itheima and itcast  "
new_my_str = my_str.strip() # 不传入参数去除首尾空格
my_str = "12itheima and itcast21"
new_my_str = my_str.strip("12") # 输出结果为itheima and itcast
# 统计字符串在某字符串中出现的次数，count
my_str = "itheima and itcast"
count = my_str.count("it")
# 统计字符串的长度，len
num len(my_str)
```

## 5.7 数据容器的切片

### 5.7.1 序列

序列：内容连续、有序，可以使用下标索引的一类数据容器  
列表、元组、字符串均可以视为序列

### 5.7.2 切片

切片：从一个序列中，取出一个子序列  
切片操作不影响原序列，只会得到一个新的序列

语法：序列[起始下标：结束下标：步长]

- 起始下标表示从何开始，可以留空，留空视为从头开始
- 结束下标(不含)表示何处结束，可以留空，留空视为截取到结尾
- 步长表示，依次取元素的间隔  
    *步长N表示，每次跳过N-1个元素  
    *步长为负数，反向取(注意，起始下标和结束下标也要反向标记)

```
my_list = [0, 1, 2, 3, 4, 5, 6]
result1 = my_list[1:4]      # 步长默认是1
```

## 5.8 数据容器：set(集合)

**集合不可以重复**  
**顺序不可以保证**

### 5.8.1 集合的定义格式

集合的定义：  
基本语法：{元素， 元素， 元素}

```
# 定义集合
my_set = {"传智教育", "黑马程序员"， "itheima", "传智教育", "黑马程序员"， "itheima"}
my_set_empty = set      [[定义空集合]]
```

### 5.8.2 集合的常用操作-修改

因为集合是无序的，所以集合不支持：下标索引访问，但集合是允许修改的

- 添加新元素  
    语法：集合.add(元素) 将制定元素添加到集合内  
    结果：集合本身被修改，添加了新元素
- 移除元素  
    语法：集合.remove(元素),将指定元素，从集合内移除  
    结果：集合本身被修改，移除了元素
- 随机取出元素  
    语法：集合.pop()，功能：从集合随机取出一个元素  
    结果：会得到一个元素的结果。同时集合本身被修改，元素被移除
- 清空集合  
    语法：集合.clear(),功能：清空集合  
    结果：集合本身被清空
- 取两个集合的差集  
    语法：集合1.difference(集合2)，功能：取出集合1和集合2的差集(集合1有而集合2没有的)  
    结果：得到一个新集合，集合1和集合2不变
- 消除两个集合的差集  
    语法：集合1.difference_update(集合2)  
    功能：对比集合1和集合2，在集合1内，删除和集合2相同的元素  
    结果：集合1被修改，集合2不变
- 两个集合合并  
    语法：集合1.union(集合)  
    功能：将集合1和集合2组成新集合  
    结果：得到新集合，集合1和集合2不变

```
# 添加新元素
my_set.add("python")
my_set.add("C++")
# 移除元素
my_set.remove("黑马程序员")
# 随机取出集合
my_set = {"传智教育"， "黑马程序员"，"itheima"}
element = my_set.pop()
# 清空集合
my_set.claer()
# 取两个集合的差集
set1 = {1, 2, 3}
set2 = {1, 5, 6}
set3 = set1.difference(set2)
# 删除2个集合的差集
set1 = {1, 2, 3}
set2 = {1, 5, 6}
set3 = set1.difference_update(set)
# 两个集合合并
set1 = {1, 2, 3}
set2 = {1, 5, 6}
set3 = set.union(set2)
# 统计集合元素数量
set1 = {1, 2, 3, 4,5}
num = len(set1)
# 集合的遍历
# 集合不支持下标索引，不能用while循环
# 可以用for循环
set1 = {1, 2, 3, 4, 5}
for element in set1:
    print(f"集合的元素有：{element}")
```

## 5.9 数据容器：dict(字典、映射)

### 5.9.1 字典的定义

字典的定义，同样使用{}，不过存储的元素是一个个的：键值对  
{key: value, key: value, ……}

字典同集合一样，不可用使用下标索引  
但字典可以通过key值来取得对应的value

字典的key和value可以是任意的数据类型(key不可以为字典)

```
# 定义字典
my_dict = {"wlh":99， "zjl"：88， "ljj"：77}
# 定义空字典
my_dict2 = {}
my_dict3 = dict()
# 定义重复key的字典
my_dict = {"wlh":99， "wlh"：88， "ljj"：77}
# 字典不允许key的重复，保留后者内容

# 从字典里基于key获取value
my_dict = {"wlh":99， "zjl"：88， "ljj"：77}
score = my_dict["wlh"]
# 字典也是可以嵌套的
stu_score_dict = {
    "wlh":{
        "语文"：99，
        "数学"：88，
        "英语"：77
        }， "zjl":{
        "语文"：88，
        "数学"：77
        "英语"：66
        }， "ljj"{
        "语文"：66
        "数学"：55
        "英语"：44
        }
}
stu_score_dict["zjl"]["语文"]
```

### 5.9.2 字典的常用操作

**key存在就是更新，不存在就是新增**

- 新增元素  
    语法：字典[key] = value  
    结果：字典被修改，新增了元素
- 更新元素  
    语法：字典[key] = value  
    结果：字典被修改，元素被更新  
    注意：字典key不可用重复，所以对已存在的key执行上述操作，就是更新value值
- 删除元素  
    语法：字典.pop(key)  
    结果：获得指定key的value，同时字典被修改，指定key的数据被删除
- 获取全部的key  
    语法：字典.keys()  
    结果：得到字典中的全部key

```
my_dict = {"zjl"：99， "ljj"：88， "zxy"：77}
# 新增元素
my_dict["zxz"] = 66
# 更新元素
my_dict["zjl"] = 33
# 删除元素
score = my_dict.pop("zjl")
# 清空元素
my_dict.clear()
# 得到字典的全部key
my_dict = {"zxy": 99, "ljj": 88,"zjl": 77}
keys = my_dict.keys()
# 遍历字典
# 方式1:通过获取全部的key来遍历
for key in keys:
    print(f"字典的key是：{key}")
    print(f"字典的value是：{my_dict[key]}")
# 方式2:直接对字典进行for循环，每一次循环都是直接得到key
for key in my_dict:
    print(f"2字典的key是：{key}")
    print(f"2字典的value是：{my_dict[key]}")
# 统计字典内的元素数量
element = len(my_dict)
```

## 5.10 数据容器对比总结

- 是否支持下标索引

- 支持：列表、元组、字符串 - 序列类型
- 不支持：集合、字典 - 非序列类型

- 是否支持重复元素

- 支持：列表、元组、字符串 - 序列类型
- 不支持：集合、字典 - 非序列类型

- 是否可以修改

- 支持：列表、集合、字典
- 不支持：元组、字符串

使用场景：

- 列表：一批数据，可修改、可重复的存储场景
- 元组：一批数据，不可修改、可重复的存储场景
- 字符串：一串字符串的存储场景
- 集合：一批数据，去重存储场景
- 字典：一批数据，可用key检索value的存储场景

## 5.11 数据容器的通用操作

### 5.11.1遍历

首先，在遍历上：

- 5类数据容器都支持for循环遍历
- 列表、元组、字符串支持while循环，集合、字典都不支持（无法下标索引）

### 5.11.2统计

- len(容器) 统计容器的元素个数
- max(容器) 统计容器的最大元素
- min(容器) 统计容器的最小元素

### 5.11.3容器的通用转换功能

- list(容器)    将给定容器转换为列表
- str(容器)     将给定的容器转换为字符串
- tuple(容器)   将给定容器转换为元组
- set(容器)     将给定容器转换为集合

### 5.1.4容器通用排序功能

- sorted(容器 ，[reverse=True])  
    默认是False，如果希望排序反转传入一个True  
    将给定容器进行排序

```
print(f'列表对象的排列顺序:{sorted{my_dict}}")
print(f'列表对象的排列顺序:{sorted{my_dict},[resverse=True]}")
```

## 5.12 字符串大小比较

字符串所用的字符：

- 大小写英文单词
- 数字
- 特殊字符  
    都有对应的ACCII码表值

**字符串比较就是基于ascii进行比较**  
字符串是按位比较，也就是一位位进行对比，只要有一位大，那么整体就大

# 6. 文件操作

## 6.1 文件的编码

计算机中有许多可用的编码：

- UTF-8
- GBK
- Big5  
    不同的编码，将内容翻译成二进制  
    UTF-8是目前全球通用的编码格式

## 6.2 文件的读取

### 6.2.1 什么是文件

一篇文章、一段视频、一个可执行程序、都可以保存为一个文件

### 6.2.2文件操作

- open()打开函数  
    **语法：open(name, mode, encoding)**  
    name:是要打开的目标文件名的字符串(可以包含文件所在的具体路径)  
    mode:设置打开文件的模式(访问模式)：只读、写入、追加  
    encoding:编码格式(推荐使用UTF-8)  
    示例代码：  
    f = open("python.txt", "r", encoding ="UTF-8")

**encoding的顺序不是第三位，所以不能用位置参数，用关键字参数直接指定**  
注意：此时的'f'是'open'函数的文件对象，对象是python中一种特殊的数据类型，拥有属性和方法，可以使用对象.属性或对象.方法对其进行访问

r：只读  
w：写入  
a：追加

读操作相关方法

- read()方法：  
    文件对象.read(num)  
    num表示要从文件中读取的数据的长度（单位是字节），如果没有传入num，那么就表示读取文件中的所有数据
- readlines()方法：  
    readlines可以按照行的方式把整个文件中的内容尽性一次性读取，并且返回的是一个列表，其中每一行的数据为一个元素  
    读取文件的全部行，封装到列表中
- readline()方法：  
    一次读取一行内容
- for循环读取文件行  
    每一个line临时变量，就记录了文件的一行数据
- close()关闭文件对象  
    关闭对文件的占用
- with open语法  
    可以在操作完成后自动自闭close

```
# 打开文件
f = open("D:/测试.txt", "r", encoding = "UTF-8)
# 读取文件 - read()
print(f"读取十个字节的结果:{f.read(10)}")
print(f"读取全部结果是：{f.read()}")    # read会从上次阅读的结尾处接着读取
# 读取文件 - readlines()
lines = f.readlines()   # 读取文件的全部行，封装到列表中
print(f"lines对象的内容是:{lines}")
# 读取文件 - readline()
line1 = f.readline()    # 第一行数据
line2 = f.readline()    # 第二行数据
line3 = f.readline()    # 第三行数据
# for循环读取文件行
for line in f:
    print(f"每一行数据是:{line}")
# 文件的关闭
f.close()
# with open 语法操作文件
with open("D:/测试.txt", "r", encoding="UTF-8"):
    for line in f:
        print(f"每一行数据时：{line}")
```

## 6.3 文件的写入

1.打开文件  
f = open()  
2.文件写入  
f.write()  
3.内容刷新  
f.flush()  
注意：  
1.直接调用write，内容并为真正写入文件，而是会积攒在程序的内存中，称之为缓冲区  
2.当调用flush的时候，内容会真正写入文件  
3.这样做是避免频繁的操作硬盘，倒置效率下降(攒一堆，一次性写磁盘)

```
# 打开文件，不存在的文件
open("D:/test.txt", "w", encoding="UTF-8")
# write写入
f.write("Hello world")      # 内存写入到内存中
# flush刷新
f.flush()                    # 将内存中积攒的内容，写入到硬盘的文件中
# close关闭
f.close()                     # close方法，内置了flush的功能
# 打开一个存在的文件
f = open("D:/test.txt", "w", encoding="UTF-8")
# write写入、flush刷新
f.write("黑马程序员")
# close关闭
f.close()
```

## 6.4 文件的追加

注意：  
1.a模式，不存在会创建文件  
2.a模式，存在会追加文件

```
# 打开文件，不存在的文件
f = open("D:/test.txt", "a", encoding="UTF-8")
# write写入，flush刷新
f.write("\n学python最佳选择")
# close关闭
f.close()
```

# 7. 异常、模块与包

## 7.1 了解异常

当检测到一个错误时，python解释器就无法继续执行了，反而出现一些错误的提起，这就是所谓的"异常"，也就是"BUG"

## 7.2 异常的捕获方法

当我们的程序遇到了BUG，接下来有两种情况：  
1.整个程序因为一个BUG停止运行  
2.对BUG进行提醒，整个程序继续运行  
捕获异常的作用在于：提前假设某处会出现异常，做好提前准备，当真的出现异常的时候，可以有后续手段

基本语法：  
try:  
可能发生错误的代码  
except:  
如果出现异常执行的代码

捕获指定异常：  
try:  
print(name)  
except NameError as e:  
print('name变量名称未定义错误')  
注意：  
1.如果尝试执行的代码的异常类型和要捕获的异常类型不一致，则无法捕获异常  
2.一般try下方只放一行尝试执行的代码

捕获多个异常：  
try:  
print(1/0)  
except(NameError,ZeroDivisionError):  
print('ZeroDivisionError错误啊...')

异常else：  
else表示如果没有异常要执行的代码  
try:  
print(1)  
except Exception as e:  
print(e)  
else:  
print("我是else，是没有异常的时候执行的代码")

异常的finally：  
finally表示的是无论是否异常都要执行文件，例如关闭文件

```
# 基本捕获语法
try:
    f = open("D:/abc.txt', "r", encoding="UTF-8")
except:
    print("出现异常了，因为文件不存在，我将open的模式，改为w模式去打开)
    f = open("D:/abc.txt", "w", encoding="UTF-8")
# 捕获指定异常
try:
    # print(name)
    1/0     # 不是指定的异常，直接报错
except NameError as e:
    print("出现变量未定义的异常")
    print(e)    # e为异常的对象
# 捕获多个异常
try:
    # 1/0
    print(name)
except(NameError,ZeroDivisionError):
    print("出现了变量未定义或者是除0异常)
# 未设置捕获异常类型，将无法捕获异常

# 捕获所有异常
try:
    1/0
except Exception as e:
    print("出现异常了")
else:
    print("好高兴，没有异常")
finally：
    f.close()   # 用于把资源关闭掉
```

## 7.3 异常的传递

异常具有传递性：  
当函数func01中发生异常，并且没有捕获处理这个异常的时候，异常会传递到函数func02，当func02也没有捕获处理这个异常的时候，main函数也会捕获这个异常  
提示：  
当所有函数都没有捕获异常的时候，程序就会报错

```
def func1():
    print("func1 开始执行")
    num = 1/0       # 肯定有异常，处以0的异常
    print("func1 结束执行")

def func2():
    print("func 开始执行")
    func1()
    print("func 结束执行")
# 定义一个方法，调用上面的方法

def main():
    try:
        func2()
    except Exception as e:
        print(f"出现异常了，异常的信息是：{e}")
```

## 7.4 python模块

### 7.4.1 模块的导入

什么是模块  
模块，是一个python文件，以.py结尾，模块能定义函数，类和变量  
**模块作用**：python作用中有很多各种不同的模块，每一个模块都可以帮助我们实现一些功能，比如实现和时间相关的功能就可以使用time模块。我们可以认为一个模块就是一个工具包，每一个工具包都有各种不同的工具供我们使用进而实现各种不同的功能

大白话：模块就是一个python文件，里面有类、函数、变量等，我们可以拿过来用(导入模块去使用)

模块的导入方式：  
模块在使用之前需要先导入 导入的语法如下：  
[for 模块名] import [模块 ｜ 类 ｜ 变量 ｜ 函数 ｜ *][as 别名]  
常用的组合形式如：

- import 模块名
- from 模块名 import 类、变量、方法等
- from 模块名 import *
- from 模块名 as 别名
- from 模块名 import 功能名 as 别名

**import基本语法：**  
import 模块名  
import 模块名1，模块名2

模块名.功能名()

as定义别名：  
模块定义别名：  
import 模块名 as 别名  
功能定义别名：  
from 模块名 import功能 as 别名

```
# 使用import导入time模块使用sleep功能(函数)
improt time     # 导入python内置的time模块(time.py这个代码文件)
time.sleep(5)   # 程序执行到这里暂停5s 通过.就可以使用模块内部的全部功能(类、函数、变量)
```

**from 模块名 import 功能名**  
基本语法：from 模块名 import 功能名  
功能名()

```
# 使用from导入time的sleep功能(函数)
from time import sleep
print(5)
sleep(5)

# 使用 * 导入time模块的全部功能
from time import *      # *表示导入全部的意思 
sleep (5)

# 使用as给特定功能加上别名
import time as t
t.sleep(5)      # 和time.sleep效果等同
from time import sleep as sl
sl(5)           # 和time.sleep效果等同
```

## 7.5 自定义模块

注意：每个python文件都可以作为一个模块，模块名字就是文件的名字，但是定义的模块名要符合标识符的命名规则

```
# 文件名命名为 my_module1
def test(a, b):
    print(a + b)
```

```
import my_module1
my_module1.test(1, 2)
from my_module1 import test
test(1, 2)
```

注意事项：当导入多个模块时，且模块内有同名功能，当调用这个同名功能的时候，调用到的是后面导入的模块的功能

**main**  
只有当程序是直接执行的才会进入if内部，如果是被导入的，则if无法进入

```
def test(a,b):
    print(a+b)
if__main__ == '__main__':
    test(1, 2)
可以在该函数内验证，不会在外面的函数输出
```

```
# __main__变量
from my_module1 import test
```

**all**变量  
如果一个模块文件中有'**all**'变量，当使用'from xxx import *'导入时，只能导入这个列表中的元素

```
__all__ = ['test_A']    # 若引用from my_module1 import * 则只会引用__all__,即test_A

def test_A():
    print('testA')

def test_B():
    print('testB')
```

## 7.6 python包

### 7.6.1 自定义包

从物理上看，包就是一个文件夹，在该文件夹下包含一个**init**.py 文件，该文件夹可用于包含多个模块文件  
从逻辑上看，包的本质依然是模块

导入包：  
方式一：  
import 包名.模块名1，模块名  
包名.模块名.目标

方式二：  
必须在'**init**.py'文件中添加'**all**=[]',控制允许导入的模块列表  
from 包名 import*  
模块名.目标

```
# __init__ 文件
__all__ = ['my_module1]
```

```
# 导入定义的包中的模块
import my_package.my_module1
my_package.my_module1.info_print1()

from my_package import my_module1
info_print1()

# 通过__all__变量，控制import *
from my_package import my_module1
my_module1.info_print1()
# 因为init文件，所以只可以引用module1
```

### 7.6.2 安装第三方包

第三方包：

- 科学计算中常用：numpy包
- 数据分析常用的：pandas包
- 大数据计算常用的：pyspark、apache-flink包
- 图形可视化常用的：matplotlib、pyecharts包  
    人工智能常用的：tensorflow

安装第三方包 - pip  
命令提示符：pip install 包名称  
ctrl c可以停止命令

通过国内提供网站进行安装：pip install -i https://pypi.tuna.tsinghua.edu.cn/simple包名称

# 8. 折线图可视化

## 8.1 json数据格式

**不同语言间的数据发送**  
json

- json是一种轻量级的数据交互格式。可以按照json指定的格式去组织和封装数据
- json本质是一个带有特定格式的字符串

**主要功能：**json就是一种在各个编程语言中流通的数据格式，负责不同编程语言中的数据传递和交互，类似于：  
* 国际通用语言-英语  
* 中国56个民族不同地区的通用语言-普通话

json格式数据转化

- json格式的数据要求很严格  
    示例：  
    **json数据的格式可以是：**  
    {"name":"admin","age":18}

**也可以是:**  
[{"name":"admin","age":18},{"name":"root","age":16},{"name":"张三","age":20}]

**python数据和json数据的相互转化**

```
# 准备列表，列表内每一个元素都是字典将其转换为JSON
data = [{"name":"张大山","age":11},{"name":"王大锤","age":13},{"name":"赵小虎","age"=16}]
json_str = json.dumps(data,ensure_ascii=False)
# 准备字典，将字典转化为JSON
d = {"name":"周杰伦","addr":"台北"}
json_str = json.dumps(d,ensure_ascii=False)
# 将json字符串转换为python数据类型
s = '[{"name":"张大山","age":11},{"name":"王大锤","age":13},{"name":"赵小虎","age"=16}]'
l = json.loads(s)   [[转化为python数据类型]]
# 将json 字符串转换为python数据类型
d = '{"name":"周杰伦","addr":"台北"}'
d = json.load(d)
```

## 8.2 pyecharts模块介绍

- 如果想要做出数据可视化效果图，可以借助pyecharts模块来完成  
    网站：  
    1.gallery.pyecharts.org  
    2.pyecharts.org

## 8.3 pyecharts快速入门

- 基础折线图  
    **导包，导入Line功能构建折线图对象**  
    from pyecharts.charts import Line  
    **得到折线图对象**  
    line = Line()  
    **添加x轴数据**  
    line.add_xaxis(["中国"，"美国"，"英国"])  
    **添加y轴数据**  
    line.add_xaxis("GDP",[30,20,10])  
    **生成图标**  
    line.render()

```
# 导包
from pyecharts.charts import Line
from pyecharts.options import TitleOpts,LegendOpts,ToolboxOpts,VisualMapOpts
# 创建一个折线图对象
line = Line()
# 给折线图对象添加x轴的数据
line.add_xaxis(["中国"，"美国"，"英国"])
# 给折线图对象添加y轴的数据
line.add_yaxis("GDP",[30,20,10])
# 通过render方法，将代码生成为图像
line.render()
# 设置全局配置项set_global_opts来设置
line.set_global_opts(
    title_opts=TitleOpts(title="GDP展示"，pos_left="center",pos_botten="1%"),
    legend_opts=LegendOpts(is_show=True),
    tool_box =ToolboxOpts(is_show=True),
    visualmap_opts=VisualMapOpts(is_show=True),
)
```

- pyecharts配置选项

- 全局配置选项  
    set_global_opts方法
- 系列配置选项

## 8.4 数据处理

```
import json
# 处理数据
open("D:/美国.txt", "r", encoding="UTF-8")
us_data = f_us.read().read()    # 美国的全部内容
# 去掉不合JSON规范的开头
us_data = us_data.replace("jsonp_1629344292311_69436(","")
# 去掉不合JSON规范的结尾
us_data = us_data[:-2]
# JSON转Python字典
us_dict = json.loads(us_data)
# 获取trend key
us_trend_data = us_dict['data'][0]['trend']
# 获取日期数据，用于x轴，取2020年（到314下标结束）
us_x_data = us_trend_data['updateDate'][:314]
# 获取确认数据，用于y轴，取2020年（到314下标结束）
us_y_data = us_trend_data['list'][0]['data'][:314]
```

## 8.5 完成折线图

```
import json
from peycharts.charts import Line
[[生成图标]]
lie = Line()        # 构建折线图表对象
# 添加x轴数据
line.add_xaxis(us_x_data)   # x轴是公用的，所以使用一个国家数据即可
# 添加y轴数据
line.add_yaxis("美国确诊人数"，us_y_data)
line.add_yaxis("日本确诊人数"，jp_y_data)
line.add_yaxis("印度确诊人数", in_y_data)
# 调用render方法，生成图表
line.render
# 关闭文件对象
f_us.close()
f_jp.close()
f.in_close()
```

# 9. 动态柱状图

## 9.1 基础柱状图

```
from pyecharts.charts import Bar
from pyecharts.options import LabelOpts
# 使用Bar构建基础柱状图
bar = Bar
# 添加x轴的数据
bar.add_xaxis(["中国","美国","英国"])
# 添加y轴的数据
bar.add_yaxis("GDP",[30,20,10], labal_opts=LabelOpts(position="right"))
# 绘图
bar.render("基础柱状图.html")
# 反转x轴和y轴
bar.reversal.axis()
```

## 9.2 基础时间线柱状图

```
from pyecharts.charts import Bar
from pyecharts.options import LabelOpts
form peycharts.globals import ThemeType

bar1 = Bar()
bar1.add_xaxis(["中国", "美国", "英国"])
bar1.add_yaxis("GDP", [30,30,20],label_opts=LabelOpts(position="right'))
bar1.reversal.axis()

bar2 = Bar()
bar2.add_xaxis(["中国", "美国", "英国"])
bar2.add_yaxis("GDP", [50,50,50],label_opts=LabelOpts(position="right'))
bar2.reversal.axis()

bar3 = Bar()
bar3.add_xaxis(["中国", "美国", "英国"])
bar3.add_yaxis("GDP", [70,60,60],label_opts=LabelOpts(position="right'))
bar3.reversal.axis()

# 构建时间线对象
timeline = Timeline({"theme": ThemeType.LIGHT})
timeline.add(bar1,"点1")
timeline.add(bar2,"点2")
timeline.add(bar3,"点3")
# 自动播放设置
timeline.add_schema(
    play_interval=1000,             # 自动播放的时间间隔，单位毫秒
    is_timeline_show=True,          # 是否在自动播放的时候显示时间线
    is_auto_play=True,              # 是否自动播放
    is_loop_play=True               # 是否循环自动播放
)
# 绘图是用时间线对象绘图
timeline,render("基础时间线柱状图.html")
```

## 9.3 GDP动态柱状图的绘制

- 列表的排序方法  
    使用方法：  
    列表.sort(key=选择排序依据的函数，reverse=True|False)

- 参数key，是要求传入一个函数，表示将列表的每一个元素都传入函数中，返回排序的依据
- 参数reverse，是否反转排序结果，True表示降序，False表示升序

```
# 准备列表
my_list = [["a", 33],["b", 55],["c", 11]]

# 排序，基于带名函数
def choose_sort_key(element):
    return element[1]

my_list.sort(key=choose_sort_key,reverse=True)
# 排序，基于lambda匿名函数
my_list.sort(key=lambda element:element[1], reserse=True)

from pyecharts.charts import Bar, Timeline
from peycharts.options import *
from peycharts.globals import ThemeType


# 读取数据
open("D:/1960-2019全球GDP数据.csv", "r", encoding="GB2312")
data_line = f.readlines()
# 关闭文件
f.close()
# 删除第一行对象
data_lines.pop(0)
# 将数据转换为字典存储，格式为：
# { 年份： [[国家, gdp], [国家,gdp],......]}
# {1960: [[美国, 123], [中国, 321],....], 1961:[[美国, 123],[中国, 321],...]}
# 先定义一个字典对象
data_dict = {}
for line in data_lines:
    int(line.split(",")[0])     # 年份
    country = line.split(",")[1]    # 国家
    gdp = float(line.split(","))[2]     # gdp数据
    # 如何判断字典里面有没有指定的key
    try: 
        data_dict[year].append([country,gdp])
    except KeyError:
        data_dict[year].append([country, gdp])
# 创建时间线对象
timeline = Timeline({"theme":LIGHT})
# 排序年份
sorted_year_list = sorted(data_dict.keys())
for year in sorted_year_list:
    data_dict[year].sort(key=lambda element: element[1],reverse=True)
    # 取出本年份前8名的国家
    year_data = data_dict[year][0:8]
    x_data = []
    y_data = []
    for country_gdp in year_data:
        x_data.append(country_gdp[0])   # x轴添加国家
        y_data.append(country_gdp[1] / 10000000)   # y轴添加gdp数据
    # 构建柱状图
    bar = Bar()
    x_data.reversal()
    y_data.reversal()
    bar.add_xaxis(x_data)
    bar.add_yaxis("GDP(亿)",y_data),label_opts=LabelOpts(position="right"))
    # 反转x轴和y轴
    bar.reversal_axis()
    # 设置每一年图表的标题
    bar.set_global_opts(
        title_opts=TitleOpts(title=f"{year}年全球前八GDP数据")
    )
    timeline.add(bar,str(year))

# 设置时间线自动播放
timeline.add_schema(
    play_interval=1000,
    is_timeline_show=True,
    is_auto_play=True,
    is_loop_play=False
)
# 绘图
timeline.render("1960-2019全球GDP前八国家.html")
```

# 10. 地图可视化

## 10.1 基础地图使用

```
fron pyecharts.charts import my_package
from pyecharts.options import VisualMapOpts
# 准备地图对象
map = Map()
# 准备数据
data = [
    ("北京",99),
    ("上海",199),
    ("湖南",299),
    ("台湾",399),
    ("广东",499)
]
# 添加数据
map.add("测试地图",data,"china")
# 设置全局选项
map.set_global_opts(
    visualmap_opts=VisualMapOpts(
        is_show=True,
        is_piecewise=True,
        pieces=[
            {"min": 1, "max": 9, "label: "1-9", "color": "#CCFFFF"},
            {"min": 10, "max": 99, "label: "10-99", "color": "#CC6666"},
            {"min": 100, "max": 500, "label: "100-500","color": "#990033"},
        ]
    )
)
# 绘图
map.render()
```

## 10.2 疫情地图-国内疫情地图

```
import 
from pyecharts.charts import Map
from pyecharts.options import *
# 读取数据文件
f = open("D:/疫情.txt, "r", enconding="UTF-8")
data = f.read         [[全部数据]]
# 关闭文件
f.close
# 取得各省数据
# 将字符串json转换也python的字典
data_dict = json.loads(data)        # 基础数据字典
# 字典中取出省份的数据
province_data_list = data_dict["areaTree"][0]["children"]
# 组装每个省份和确诊人数为元组，并各个省的数据都封装入列表内
data_list = []      [[绘图需要用的数据列表]]
for province_data in province_data_list:
    provice_name = provice_data["name"]         # 省份名称
    provice_confirm = provice_data["total"]["confirm"]      # 确诊人数
    data_list.append((provice_name,provice_confirm))
# 创建地图对象
map = Map()
# 添加数据
map.add("各省份确诊人数", data_list, "china")
# 设置全局配置，订制分段的视觉映射
map.set_global_opts(
    title_opts=TitleOpts(title="全国疫情地图")
    visualmap_opts=VisualMapOpts(
        is_show=True,           # 是否显示
        is_piecewise=True,      # 是否分段
        pieces=[
            {"min" 1, "max" :99, "lable": "1~99", "color": "#CCFFFF"},
            {"min" 100, "max" :999, "lable": "100~999", "color": "#FFFF99"},
            {"min" 1000, "max" :4999, "lable": "1000~4999", "color": "#FF9966"},
            {"min" 5000, "max" :9999, "lable": "5000~9999", "color": "#FF6666"},
            {"min" 10000, "max" :99999, "lable": "10000~99999", "color": "#CC3333"},
            {"min" 100000, "lable": "100000~", "color": "#990033"},
        ]
    )
)
# 绘图
map.render("全国疫情地图.html")
```

## 10.3 疫情地图-省级地图绘制

```
import 
from pyecharts.charts import Map
from pyecharts.options import *
# 读取数据文件
f = open("D:/疫情.txt, "r", enconding="UTF-8")
data = f.read         [[全部数据]]
# 关闭文件
f.close
# 取得河南省数据
# 将字符串json转换也python的字典
data_dict = json.loads(data)        # 基础数据字典
# 字典中取出河南省的数据
cities_data = data_dict["areaTree"][0]["children"][3]["children"]
# 组装每个省份和确诊人数为元组，并各个省的数据都封装入列表内
data_list = []
for city_data in cities_data:
    city_name = city_data["name"] + "市"        # 城市名称
    city_confirm = city_data["total"]["confirm"]      # 确诊人数
    data_list.append((city_name,city_confirm))
# 手动添加济源市的数据
data_list.append(("济源市"，5)
# 创建地图对象
map = Map()
# 添加数据
map.add("各城市确诊人数", data_list, "河南")
# 设置全局配置，订制分段的视觉映射
map.set_global_opts(
    title_opts=TitleOpts(title="河南疫情地图")
    visualmap_opts=VisualMapOpts(
        is_show=True,           # 是否显示
        is_piecewise=True,      # 是否分段
        pieces=[
            {"min" 1, "max" :99, "lable": "1~99", "color": "#CCFFFF"},
            {"min" 100, "max" :999, "lable": "100~999", "color": "#FFFF99"},
            {"min" 1000, "max" :4999, "lable": "1000~4999", "color": "#FF9966"},
            {"min" 5000, "max" :9999, "lable": "5000~9999", "color": "#FF6666"},
            {"min" 10000, "max" :99999, "lable": "10000~99999", "color": "#CC3333"},
            {"min" 100000, "lable": "100000~", "color": "#990033"},
        ]
    )
)
# 绘图
map.render("全国疫情地图.html")
```

# 11. 高性能HTML内容解析

## 11.1 学习目标

（1）HTML基础结构  
（2）使用XPath从HTML源代码中提取有用信息  
（3）使用Beaut Soup4从HTML源代码中提取有用信息

## 11.2 HTML基础

HTML也就是前面章节提到的网页源代码，是一种结构化的标记语言。HTML可以描述一个网页的结构信息。HTML与CSS（层叠样式表）、JavaScript一起构成了现代互联网的基石。  
先以地名为例，来看HTML代码的结构关系：  
<中国>  
<北京>  
<海淀区>  
<五道口>  
<xx面馆>  
</五道口>  
</海淀区>  
<东城区></东城区>  
</北京>  
<山东>  
<青岛></青岛>  
<烟台></烟台>  
</山东>  
</中国>  
有很多用尖括号括起来的地名，而且这些地名都是成对出现的。有<北京>就有</北京>，有<山东>就有</山东>。在HTML中，这叫做标签。一个标签可以表示为：  
<标签名>  
文本  
<标签名>  
不加斜杠，表示标签开始；加上斜杠，表示标签结束。它们中间的部分，就是标签里面的元素。标签里面可以是另一个标签，也可以是一段文本。标签可以并列，也可以嵌套。例如<北京>与<山东>就属于并列关系。而<北京>与<海淀区>就是属于嵌套关系。并且，一个标签可以有0个、1个或者多个属性，所以一个真正的HTML标签应该是下面这样的：  
<标签名 属性1="属性1的值" 属性2="属性2的值">显示在网页上的文本</标签名>

**XPath**  
_**1.XPath的介绍**_  
XPath是一种查询语言，它能在XML（可扩展标记语言）和HTML的树状结构中寻找结点。简单来说，XPath就是一种根据'地址"来"找人"的语言。

_**2.XPath语法讲解**_  
我需要的信息1  
我需要的信息2  
我需要的信息3  
在看XPath的用法之前，请各位读者思考，如果使用正则表达式应该要写几行代码才能实现。  
如果使用Xpath，代码只有一行

```
info selector.xpath('//div[@class="useful"]/ul/text()')
```

使用XPath的代码如下：

```
import lxml html
selector = lxml.fromstring('网页代码')
info = selector.xpath('一段XPath语句')
```

其中"网页源代码"可以使用requess来获取。"一段XPath语句"可以按照一定的规则来构造  
1.XPath语句格式  
核心思想：写XPath就是写地址  
获取文本：  
//标签1[@属性1="属性值1"]/标签2[@属性2="属性值2"]/.../text()  
获取属性值：  
//标签1[@属性1="属性值1"]/标签2[@属性2="属性值2"]/.../@属性n

其中，[@属性="属性值"]不是必须的。它的作用是帮助过滤相同的标签。在不需要过滤相同标签的情况下可以省略

2.标签1的选取  
标签1可以直接从html这个最外层的标签开始，一层一层往下找，这个时候，XPath语句是这样的：  
/html/body/div[@class="useful"]/ul/li/text()

当以html开头的时候，它前面是单斜线。这样写虽然也可以达到目的，但是却多此一举。正如淘宝收货地址没必要写成："地球，亚洲，中国，xxx"。XPath也是同样的道理。在XPath里面找到一个标志性的"地标"，然后从这个标志性的地标开始往下找就可以找到了。标志性的"地标"前面的标签可以省略。  
所以，需要确定应该从哪个标签开头就需要"倒着找地标"，也就是，从需要提取的内容往上找标签，找到一个拥有"标志性属性值"的标签为止。  
需要找一个独一无二的属性，例如"useful"  
//div[@class='useful"]/ul/li/text()

3.哪些属性可以省略  
< div class="useful" >  
< ul >  
< li class="info" >我需要的信息1< li >

# 12. SQL入门和实战

## 12.1 SQL

不管是何种开发语言，亦或是何种开发方向，SQL都是开发者无法绕开的话题。  
除了一门趁手的编程语言外，SQL语言也是开发者人人必备的开发技能。

## 12.2 数据库介绍

我们通过数据库管理系统(数据库软件)实现数据库形式的数据管理  
数据库是用来存储数据的：

- 数据的新增
- 数据的删除
- 数据的修改
- 数据的查询
- 数据库、数据表的管理

**而SQL语言，这是一种对数据库，数据进行操作、管理、查询的工具**  
**使用数据库软件去获得库->表->数据，这种数据组织、存储的能力并借助SQL语言，完成对数据的增删改查等操作**

## 12.3 MySQL数据库的安装

MySQl是一个中小型的数据库，是开发人员必须会使用的一款数据库软件

## 12.4 MySQL软件的入门化使用

在MySQL的命令环境下，可以通过：

- show databases;   查看有哪些数据库
- use 数据库名  使用某个数据库
- show tables   查看数据库内有哪些表
- exit退出MySQl的命令行环境

## 12.5 SQL基础与DDL

SQL，结果化查询语言，用于访问和处理数据库的标准的计算机语言  
**操作数据库的一款专用软件**  
操作数据库的SQL语言，根据功能划分为四类：

- 数据定义：DDL

- 库的创建删除，表的创建删除等

- 数据操纵：DML

- 新增数据、删除数据、修改数据等

- 数据控制：DCL

- 新增用户、删除用户、密码修改、权限管理等

- 数据查询：DQL

- 基于需求查询和计算数据

- SQl语言，大小写不敏感
- SQl可以单行或多行书写，最后以；号结束
- SQL支持注释：

- 单行注释： --注释内容(--后面一定要有一个空格)
- 当行注释： # 注释内容(# 后面可以不加空格，推荐加上)
- 多行注释：/ _注释内容_ /

**DDL-库管理**

- 查看数据库：show databases;
- 使用数据库：use 数据库名称;
- 创建数据库：create database 数据库名称 [charset utf8];
- 删除数据库：drop database 数据库名称;
- 查看当前使用的数据库：selecet database()

**DDL-表管理**

- 查看有哪些表：show tables;   注意⚠️：要先选择数据库
- 删除表：drop table 表名称;    drop table if exists 表名称;
- 创建表：create table 表名称(  
    列名称  列类型，  
    列名称  列类型，  
    ...  
    )；  
    -- 列类型有  
    int                 -- 整数  
    float                -- 浮点数  
    varchar(长度)        -- 文本，长度为数字，做最大长度限制  
    data                -- 日期类型  
    timestamp           -- 时间戳类型

## 12.6 SQL-DML

DML是指数据操作语言，用来对数据库中表的数据进行更新

- 数据插入：  
    insert into 表[(列1，列2，...，列N)]values(值1，值2，...，值N)[，(值1，值2，...，值N),...,(值1，值2，...，值N)]

```
create table student(
    id int,
    name varchar(10),
    age int
);

insert into student(id) valuse(1),(2),(3);

insert into student(id,name,age) values(4,'周杰伦',31),(5,'林俊杰',33)
```

- 数据删除  
    基础语法：delete from 表名称 [where 条件判断]  
    条件判断：列 操作符 值  操作符：= < > <= >= !=
- 数据更新  
    基础语法：update 表名 set 列=值 [where 条件判断]

## 12.7 SQL-DQL

### 12.7.1 基础查询

基础语法：select 字段列表｜* form 表

```
select id name from student;
```

基础查询-过滤  
基础语法：select 字符列表｜* from 表 where 条件判断

### 12.7.2 分组聚合

需求：

- 按性别分组
- 统计每个人的人数  
    基础语法：select 字段｜聚合函数 from 表 [where 条件] group by 列  
    聚合函数：

- sum（列） 求和
- avg（列） 求平均值
- min（列） 求最小值
- max（列） 求最大值
- count（列｜*）    求数量  
    注意事项：**group by出现了哪个列，哪个列才能出现在select中的非聚合中**

### 12.7.3 排序和分页查询

可以对查询的结果，使用order by关键字，指定某个列进行排序，语法：  
select 列｜聚合函数｜* from 表  
where ...  
group by ...  
order by ...[asc | desc]  
limit n[,m]

```
select * from student where age > 20 order by age asc;
-- 升序排序
select * from student limit 10,5;
-- 从第十条开始往后选五条
```

## 12.8 Python&MySQL

### 12.8.1 基础使用

创建到MySQL的数据库链接

```
from pymysql import Connection
# 构建到MySQL数据库的链接
conn = Connection(
    host = "localhost"              # 主机名(ip)
    port = 3306                     # 端口
    user = "root"                   # 账户
    password = "cwz20031028"        # 密码
)

# print(conn.get_server_info())
# 执行非查询性质SQL
cursor = conn.cursor()       # 获取到游标对象
# 选择数据库
coon.select_db("test")
# 执行sql
cursor.execute("create table test_pymysql(id int);")
# 执行查询性质SQL

# 关闭链接
conn.close()
```