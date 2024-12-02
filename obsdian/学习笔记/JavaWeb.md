# JavaWeb

## 网络

### 计算机网络基础

利用通信线路和通信设备，将地理不同的、功能独立的多台计算机互连起来，以功能完善的网络软件来实现资源共享和信息传递，就构成了计算机网络系统

例如：**设备（手机、平板、电脑）连接路由器来实现对互联网的访问**

**区别计算机的方法：IP地址**（要求连接在同一网络下）

**区别程序的方法：端口号**（0-65535）

IP地址分为IPv4和IPv6

- IPv4 32bit
- IPv6 128bit

**传输协议**：

- TCP：当一台计算机想要与另一台计算机通讯时，两台计算机之间的通信需要畅通且可靠（会进行三次握手，断开也会进行四次挥手），这样才能保证正确收发数据，因此**TCP更适合一些可靠的数据传输场景**
- UDP：是一种**无连接协议**，数据想发就发，而且不会建立可靠传输，也就是说传输过程中有可能导致部分数据丢失，但是他比TCP传输更加简洁高效，适合做视频直播

三次握手：

四次挥手：

### 了解Socket技术

Socket（套接字）是计算机之间进行**通信**的**一种约定**和方式（ => 实现两台计算机之间的通信 ），是操作系统底层提供的一项通信技术，支持TCP和UDP。

要实现Socket通信，必须创建一个数据发送者（客户端）和数据接收者（服务端）

```
import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;

public class Server {
    public static void main(String[] args) {
        try (ServerSocket server = new ServerSocket(8080)){
            System.out.println("等待客户端连接...");
            //暂时阻塞线程，等待客户端连接，一旦获得请求，停止阻塞
            Socket socket = server.accept();
            System.out.println("客户端已连接" + socket.getInetAddress().getHostAddress());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

```
import java.io.IOException;
import java.net.Socket;

public class Clinet {
    public static void main(String[] args) {
        try(Socket socket = new Socket("localhost",8080)) {
            System.out.println("已连接到服务器");
        } catch (IOException e) {
            System.out.println("服务器连接失败");
            e.printStackTrace();
        }

    }
}
```

一旦TCP连接建立，服务端和客户端之间就可以相互发送数据，知道客户端主动关闭连接。当然，服务端不仅仅只可以让一个客户端连接，只要服务器不关闭，可以不断接收客户端的连接。

### 使用Socket进行数据传输

通过Socket对象，我们就可以获取对应的I/O流进行网络数据传输：

```
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.ServerSocket;
import java.net.Socket;

public class Server {
    public static void main(String[] args) {
        try (ServerSocket server = new ServerSocket(8080)){
            System.out.println("等待客户端连接...");
            //暂时阻塞线程，等待客户端连接，一旦获得请求，停止阻塞
            Socket socket = server.accept();
            System.out.println("客户端已连接" + socket.getInetAddress().getHostAddress());
            System.out.println("读取客户端数据：");
            BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            System.out.println(reader.readLine());
            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

```
import java.io.IOException;
import java.io.OutputStream;
import java.io.OutputStreamWriter;
import java.net.Socket;
import java.util.Scanner;

public class Clinet {
    public static void main(String[] args) {
        try(Socket socket = new Socket("localhost",8080);
            Scanner scanner = new Scanner(System.in)) {
            System.out.println("已连接到服务器");
            OutputStreamWriter writer = new OutputStreamWriter(socket.getOutputStream());
            writer.write(scanner.nextLine()+"\n");
            //将数据刷新一下，才会将数据发送到服务端去
            writer.flush();
            System.out.println("数据已发送！");
        } catch (IOException e) {
            System.out.println("服务器连接失败");
            e.printStackTrace();
        }

    }
}
```

同理，既然服务端可以读取客户端的内容，客户端也可以在发送后等待服务端给予响应：

```
import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;

public class Server {
    public static void main(String[] args) {
        try (ServerSocket server = new ServerSocket(8080)){
            System.out.println("等待客户端连接...");
            //暂时阻塞线程，等待客户端连接，一旦获得请求，停止阻塞
            Socket socket = server.accept();
            System.out.println("客户端已连接" + socket.getInetAddress().getHostAddress());
            System.out.println("读取客户端数据：");
            BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            System.out.println(reader.readLine());

            OutputStreamWriter writer = new OutputStreamWriter(socket.getOutputStream());
            writer.write("收到\n");
            writer.flush();
            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

```
import java.io.*;
import java.net.Socket;
import java.util.Scanner;

public class Clinet {
    public static void main(String[] args) {
        try(Socket socket = new Socket("localhost",8080);
            Scanner scanner = new Scanner(System.in)) {
            System.out.println("已连接到服务器");
            OutputStreamWriter writer = new OutputStreamWriter(socket.getOutputStream());
            writer.write(scanner.nextLine()+"\n");
            //将数据刷新一下，才会将数据发送到服务端去
            writer.flush();
            System.out.println("数据已发送！等待服务端确认....");

            BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            System.out.println("收到服务端的响应："+reader.readLine());
        } catch (IOException e) {
            System.out.println("服务器连接失败");
            e.printStackTrace();
        }

    }
}
```

我们可以手动关闭一些单向的流

```
socket.shutdownOutput();  //关闭输出方向的流
socket.shutdownInput();   //关闭输入方向的流
```

如果我们不希望服务器等待太长的时间，我们还可以调用setSoTimeout()方法来设定IO超时时间：

socket.setSoTimeout(3000);

当超过设定时间依然没有收到客户端或服务端的数据时间，会抛出异常：

```
等待客户端连接...
客户端已连接127.0.0.1
读取客户端数据：
java.net.SocketTimeoutException: Read timed out
	at java.net.SocketInputStream.socketRead0(Native Method)
	at java.net.SocketInputStream.socketRead(SocketInputStream.java:116)
	at java.net.SocketInputStream.read(SocketInputStream.java:171)
	at java.net.SocketInputStream.read(SocketInputStream.java:141)
	at sun.nio.cs.StreamDecoder.readBytes(StreamDecoder.java:284)
	at sun.nio.cs.StreamDecoder.implRead(StreamDecoder.java:326)
	at sun.nio.cs.StreamDecoder.read(StreamDecoder.java:178)
	at java.io.InputStreamReader.read(InputStreamReader.java:184)
	at java.io.BufferedReader.fill(BufferedReader.java:161)
	at java.io.BufferedReader.readLine(BufferedReader.java:324)
	at java.io.BufferedReader.readLine(BufferedReader.java:389)
	at Server.main(Server.java:15)

进程已结束，退出代码为 0
```

如果连接的双方发生意外而通知不到对象，导致一方还持有连接，这样会占用资源，因此我们可以使用setKeepAlive()方法来防止此类情况的发生：

socket.setKeepAlive(true);

当客户端连接后，如果设置了keepAlive为true，当对方没有发送任何数据过来，超过一个时间（看系统内核参数配置），那么我们这边会发送一个ack探测包发到对象，探测双方的TCP/IP连接是否有效。

### 使用Socket传输文件

```
import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;

public class Server {
    public static void main(String[] args) {
        try (ServerSocket server = new ServerSocket(8080)) {
            Socket socket = server.accept();
            InputStream stream = socket.getInputStream();
            FileOutputStream fileOutputStream = new FileOutputStream("net/data.txt");
            byte[] bytes = new byte[1024];
            int i;
            while ((i = stream.read(bytes)) != -1) {
                fileOutputStream.write(bytes, 0, i);
            }
            fileOutputStream.flush();
            fileOutputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

```
import java.io.*;
import java.net.Socket;
import java.util.Scanner;

public class Clinet {
    public static void main(String[] args) {
        try (Socket socket = new Socket("localhost", 8080)) {
            FileInputStream fileInputStream = new FileInputStream("src/text.txt");
            OutputStream stream = socket.getOutputStream();
            byte[] bytes = new byte[1024];
            int i;
            while ((i = fileInputStream.read(bytes)) != -1) {
                stream.write(bytes, 0, i);
            }
            fileInputStream.close();
            stream.flush();
        } catch (IOException e) {
            System.out.println("服务器连接失败");
            e.printStackTrace();
        }

    }
}
```

### 使用浏览器访问Socket服务器

```
import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;

public class Server {
    public static void main(String[] args) {
        try (ServerSocket server = new ServerSocket(8080)) {
            System.out.println("正在等待客户端连接...");
            Socket socket = server.accept();
            System.out.println("客户端已连接，IP地址为：" + socket.getInetAddress().getHostAddress());
            InputStream in = socket.getInputStream();
            System.out.println("接收到客户端数据");
            while(true){
                int i = in.read();
                if(i == -1) break;
                System.out.print((char) i);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

用浏览器访问获得的请求：

```
正在等待客户端连接...
客户端已连接，IP地址为：0:0:0:0:0:0:0:1
接收到客户端数据
GET / HTTP/1.1
Host: localhost:8080
Connection: keep-alive
Cache-Control: max-age=0
sec-ch-ua: "Not_A Brand";v="8", "Chromium";v="120", "Google Chrome";v="120"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: Webstorm-4be55202=0268bcd1-421b-4598-a5d0-3faa81e4fc11
```

这些内容都是HTTP协议规定的请求头内容。HTTP是一种应用层协议，全程超文本传输协议，它本质也是基于ICP协议进行数据传输，因此我们的服务器能够读取HTTP请求。但是HTTP协议并不会保持长连接，在得到我们响应的数据后会立即关闭TCP连接。

## 数据库

### 什么是数据库

数据库是数据管理的有效技术，是由一批数据构成的有序集合，这些书数据被存放在结构化的数据表里，。数据表之间相互关联，反映客观事务间的本质联系。

#### 常见的数据库

- MySQL - 免费，用的最多，开源数据库，适合中小型
- Microsoft SQL Server - 收费，但提供技术支持，使用于Windows Server
- Oracle - 收费 大型数据库系统

#### 数据模型

数据模型与现实中的模型一样，是对现实世界数据特征的一种抽象。比如一个学生的特征包括：姓名、学号、年纪、专业等这些成为一种属性，属性具有以下特点：

- 属性不可再分
- 一个实体的属性可以有很多个
- 用于唯一区分不同实体的属性，称为Key，比如每个同学的学号都是不一样的
- 属性取值可以有一定约束，比如性别只能是男或女

### 数据库的规范化

#### 第一范式(1NF)

第一范式是指数据库的每一列都是不可分割的基本数据项，而下面这样的就存在可分割的情况：

- 学生（姓名，电话号码）电话号码包括 家用座机电话 和 移动电话，因此可以拆分为：
- 学生（姓名，座机号码，手机号码）

满足第一范式是关系型数据库最基本的要求！

#### 第二范式(2NF)

第二范式要求表中必须存在主键，且其他的属性必须完全依赖于主键，比如：

- 学生（学号，姓名，性别）

学号是每个学生的唯一标识，每个学生都有着不同的学号，因此此表中存在一个主键，并且每个学生的所有属于都依赖于学号，学号发生改变就代表学生发生改变，姓名和性别都会因此发生改变，所有满足第二范式

#### 第三范式（3NF）

在满足第二范式的情况下，所以的属性都不传递依赖于主键，满足第三范式

- 学生借书情况（借阅编号，学生学号，书籍编号，书籍名称，书籍作者）

实际上书籍编号依赖于借阅编号，而书籍名称和书籍作者都依赖于书籍编号，因此存在传递依赖的情况，我们可以将书籍信息进行单独拆分为另一张表：

- 学生借书情况（借阅编号，学生学号，书籍编号）
- 书籍（书籍编号，书籍名称，书籍作者）

这样就消除了传递依赖，从而满足第三范式

#### BCNF

BCNF作为第三范式的补充，假设仓库管理关系表为Manage(仓库ID，存储物品，管理员ID，数量)，且有一个管理员在一个仓库中作：一个仓库可以存储多种物品，这个数据库中存在如下决定关系：

(仓库ID，存储物品ID) -> (管理员ID，数量)

(管理员ID，存储物品ID) -> (仓库ID，数量)

所以，(仓库ID，存储物品ID) 和(管理员ID，存储物品ID)都是Manage的候选关键字，表中唯一的非关键字段为数量，符合第三范式，但是，由于存在存在如下决定关系：

(仓库ID) -> (管理员ID)

(管理员ID) -> (仓库ID)

即存在关键字段决定关键字段的情况，所以不符合BCNF范式

### 认识SQL语句

**结构化查询语言**简称SQL，专门用于数据库的操作

- SQL语句不区分大小写（关键字推荐大写），它支持多行，并且需要使用；结尾
- SQL也支持注释，通过使用 -- 或 # 来编写注释内容，也可以使用/*来进行多行注释

学习目标：

- 数据查询语句
- 数据操纵语句
- 数据库定义语句
- 数据库控制语句

### 数据库定义语言(DDL)

1. 创建数据库

```
CREATE DATABASE study;
// 为了支持中文，我们在创建的时候可以设定编码格式
CREATE DATABASE IF NOT EXISTS study DEFAULT CHARSET utf8_general_ci;
```

1. 删除数据库

DROP DATABASE study;

**SQL数据类型**：

以下数据类型用于字符串存储：

- char(n)可以存储任意字符串，但是是固定长度为n，如果插入的长度小于定义长度时，则用空格填充
- varchar(n)也可以存储任意数量的字符串，长度不固定，但不能超过n，不会用空格填充

以下数据类型用于存储数字：

- smallint用于存储小的整数，范围在(-32768,32767)
- int用于存储一般的整数，范围在(-2147483648,2147483647)
- bigint用于存储大型整数，范围在(-9,223,372,036,854,775,808, 9,223,372,036,854,775,807)
- float用于存储单精度小数
- double用于存储双精度的小数

以下数据类型用于存储时间：

- date存储日期
- time存储时间
- year存储年份
- datetime用于混合存储日期+时间

**列级约束条件**：

列级约束有六种：主键，外键，唯一，检查，默认，非空/空值

**表级约束条件**：

表级约束有四种，主键，外键，唯一，检查

1. 创建表

注意：要切换到你创建的数据库目录下

```
CREATE TABLE student(sid int primary key,
                    name varchar(10) null,
                    sex enum(`男`,`女`) not null default `男`);
```

[CONSTRANINT <外键名>] FOREIGN KEY 字段名 [,字段名2,...] REFERENCES <主表名> 主键列1 [,主键列2,...];

1. 修改表

```
ALTER TABLE 表名[ADD 新列名 数据类型[列级约束条件]]
			   [DROP COLUMN 列名[restrict|cascade]]
			   [ALTER COLUMN 列名 新数据类型];
```

1. 删除表

DROP TABLE 表名[restrict|cascade];

### 数据库操纵语言(DML)

1. 插入数据

通过使用insert into语句来向数据库中插入一条数据：

INSERT INTO 表名 VALUES(值1，值2，值3);

如果插入的数据与列一一对应，那么可以省略列名，但是如果希望向指定列上插入数据，就需要给出列名：

INSERT INTO 表名(列名1，列名2) VALUES(值1，值2);

我们可以一次性向数据库中插入多条数据：

INSERT INTO 表名(列名1，列名2) VALUES（值1，值2），（值1，值2），（值1，值2）;

1. 修改数据

通过update语句来更新表中的数据：

UPDATE 表名 SET 列名=值, ... WHERE 条件;

SQL语句的判等是“=”

1. 删除数据

通过delete来删除表中的数据：

DELETE FROM 表名;

通过这种方式，将删除表中全部数据，也可以使用where来添加条件，只删除指定的数据

DELETE FROM 表名 WHERE 条件;

### 数据库查询语句(DQL)

**单表查询**

```
-- 指定查询某一列数据
SELECT 列名[,列名] FROM 表名;
-- 会以别名显示此列
SELECT 列名 别名 FROM 表名
-- 查询所有的列数据
SELECT * FROM 表名
-- 只查询不重复的值
SELECT DISTINCT 列名 FROM 表名
```

也可以添加where字句来限定查询目标：

SELECT * FROM 表名 WHERE 条件;

**常用查询条件**

- 一般的比较运算符，包括=, >, <, >=, <= , !=等
- 是否在集合中：in、 not in
- 字符模糊匹配：like、not like
- 多重条件连接查询：and、or、not

**排序查询**

通过order by来将查询结果进行排序：

SELECT * FROM 表名 WHERE 条件 ORDER BY 列名 ASC|DESC;

使用ASC表示升序排序，使用DESC表示降序排序，默认为升序

也可以同时添加多个排序

SELECT * FROM 表名 WHERE 条件 ORDER BY 列名1 ASC|DESC, 列名2 ASC|DESC;

**聚集函数**

聚集函数一般用作统计，包括：

- count([distinct*]) 统计所有的行数(distinct表示去重再统计)
- count([distinct]列名) 统计某列的值总和
- sum([distinct]列名) 求一列的和（注意必须是数字类型的）
- avg([distinct]列名) 求一列的平均值（注意必须是数据类型的）
- max([distinct]列名) 求一列的最大值
- min([distinct]列名) 求一列的最小值

一般聚集函数是这样使用的：

SELECT count(distinct 列名) FROM 表名 WHERE 条件;

**分组和分页查询**

通过使用group by来对查询结果进行分组，需要结合聚合函数一起使用：

SELECT sum(*) FROM 表名 WHERE 条件 GROUP BY 列名;

还可以添加having来限制分组条件：

SELECT sum(*) FROM 表名 WHERE 条件 GROUP BY 列名 HAVING 约束条件;

通过limit来限制查询的数量，只取n个结果

SELECT * FROM 表名 LIMIT 数量;

也可以进行分页

SELECT * FROM 表名 LIMIT 起始位置，数量;

**多表查询**

同时查询两个或两个以上的表，多表查询会通过连接转换的方式转换为单表查询

SELECT * FROM 表1，表2;

直接这样查询会得到两张表的笛卡尔积，也就是每一项数据和另一张表的每一项数据都结合一次，会产生庞大的数据

SELECT * FROM 表1，表2 WHERE 条件;

**注意**：如果两个表都带有此属性，需要添加表名前缀来指明是哪一个表的数据

**自身连接查询**

自身连接，就是将表本身和笛卡尔积计算，得到结果，但是由于表名相同，因此要先起一个别名：

SELECT * FROM 表名 别名1，表名 别名2;

**外连接查询**

外连接查询专门用于联合查询情景，比如现在有一个存储用户的表，和用户的详细的信息，如果想要得到一张完整的表，就需要用到外连接，有三种方式：

- 通过inner join进行内连接，只会返回两个满足条件的交集部分
- 通过left join进行左连接，不仅会返回两个满足条件的交集部分，也会返回左边表中的全部数据，而右边表中确实数据会使用null来代替（右连接right join同理）

### 数据库控制语言(DCL)

**创建用户**

通过create user来创建用户

CREATE USER 用户名 indentified by 密码;

也可以不带密码

CREATE USER 用户名;

可以通过@来限制用户登录的登录IP地址，%表示匹配所有的IP地址，默认使用的就是任意IP地址

**登录用户**

首先需要添加一个环境变量，然后通过cmd去登录mysql：

login -u 用户名 -p;

输入密码后即可登录此用户，然后输入以下命令来看看是否能访问所有数据库：

show databases;

我们发现，虽然用户能够登录，但并不能查看完整的数据库列表，这是因为用户还没有权限

**用户权限**

通过使用grant来为一个数据库用户进行授权：

grant all|权限1，权限2...(列1,...) on 数据库.表 to 用户 [with grant option];

其中all代表授予所有权限，当数据库和表为*，代表为所有的数据库和表都授权。如果再最后添加了with great option,那么被授权的用户还能将已获得的授权继续授权给其他用户。可以使用revoke来收回一个权限：

revoke all|权限1，权限2...(列1，...) on 数据库，表 from 用户;

### 视图

视图的本质是一个查询的结果。

通过create view来创建视图：

CREATE VIEW 视图名称(列名) as 子查询语句 [WITH CHECK OPTION];

WITH CHECK OPTION是指当创建后，如果更新视图中的数据，是否要满足子查询中的条件表达式，不满足将无法插入，创建后，我们就可以使用select语句来直接查询视图上的数据了，因此，还能在视图的基础上，导出其他的视图。

1. 若视图是由两个以上基本表导出的，则此视图不允许更新。
2. 若视图的字段来自字段表达式或常数，则不允许对此视图执行INSERT和UPDATE操作，但允许执行DELETE操作。
3. 若视图的字段来自集函数，则此视图不允许更新。
4. 若视图定义中含有GROUP BY子句，则此视图不允许更新。
5. 若视图定义中含有DISTINCT短语，则此视图不允许更新。
6. 若视图定义中有嵌套查询，并且内层查询的FROM子句中涉及的表也是导出该视图的基本表，则此视图不允许更新。
7. 一个不允许更新的视图上定义的视图也不允许更新

通过drop来删除一个视图：

drop view apptest;

### 索引

在数据量非常庞大的时候，创建索引快速地定位元素存放的位置：

```
-- 创建索引
CREATE INDEX 索引名称 ON 表名 (列名)
-- 查看表中的索引
show INDEX FROM student
```

通过下面的命令删除一个索引：

drop index 索引名称 on 表名

虽然添加索引后会使得查询效率更高，但是我们不能过度使用索引，索引为我们带来高速查询效率的同时，也会在数据更新时产生额外建立索引的开销，同时也会占用磁盘资源。

### 触发器

在某种条件下会自动触发，在select/update/delete时，会自动执行我们预先设定的内容，触发器通常用于检查内容的安全性，相比直接添加约束，触发器显得更加灵活。

触发器所依附的表称为基本表，当触发器表上发生select/update/delete等操作时，会自动生成两个临时的表（new表和old表，只能由触发器使用）

比如在insert操作时，新的内容会被插入到new表中；在delete操作时，旧的内容会被移到old表中，我们仍可在old表中拿到被删除的数据；在update操作时，旧的内容会被移到old表中，新的内容会出现在new表中。

CREATE TRIGGER 触发器名称 [BEFORE|AFTER] [INSERT|UPDATE|DELETE] ON 表名/视图名 FOR EACH ROW DELETE FROM student WHERE student.sno = new.sno

FOR EACH ROW表示针对每一行都会生效，无论哪行进行指定操作都会执行触发器！

通过下面的命令来查看触发器：

SHOW TRIGGERS

如果不需要，我们就可以删除此触发器：

DROP TRIGGER 触发器名称

### 事务

当我们要进行的操作非常多时，比如要依次删除很多个表的数据，我们就需要执行大量的SQL语句来完成，这些数据库操作语句就可以构成一个事务！只有Innodb引擎支持事务，我们可以这样来查看支持的引擎：

SHOW ENGINES;

MySQL默认采用的是Innodb引擎，我们也可以去修改为其他的引擎。

事务具有以下特性：

- **原子性：**一个事务（transaction）中的所有操作，要么全部完成，要么全部不完成，不会结束在中间某个环节。事务在执行过程中发生错误，会被回滚（Rollback）到事务开始前的状态，就像这个事务从来没有执行过一样。
- **一致性：**在事务开始之前和事务结束以后，数据库的完整性没有被破坏。这表示写入的资料必须完全符合所有的预设规则，这包含资料的精确度、串联性以及后续数据库可以自发性地完成预定的工作。
- **隔离性：**数据库允许多个并发事务同时对其数据进行读写和修改的能力，隔离性可以防止多个事务并发执行时由于交叉执行而导致数据的不一致。事务隔离分为不同级别，包括读未提交（Read uncommitted）、读提交（read committed）、可重复读（repeatable read）和串行化（Serializable）。
- **持久性：**事务处理结束后，对数据的修改就是永久的，即便系统故障也不会丢失。

我们通过以下例子来探究以下事务：

```
begin;   #开始事务
...
rollback;  #回滚事务
savepoint 回滚点;  #添加回滚点
rollback to 回滚点; #回滚到指定回滚点
...
commit; #提交事务
-- 一旦提交，就无法再进行回滚了！
```

## JDBC

Java Data Base Connectivity(Java数据库连接)，是Java编程语言和广泛的数据库之间独立于数据库的连接标准的Java API，根本上说JDBC是一种规范，它提供的接口，一套完整的，允许便捷式访问底层数据库

### 使用JDBC连接数据库

```
import java.sql.*;

public class Main {
    public static void main(String[] args) {
        //1. 通过DriverManager来获得数据库连接
        try (Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/study"
                                                                 , "root", "cwz20031028");
             //2. 创建一个用于执行SQL的Statement对象
             Statement statement = connection.createStatement()) {   
             //注意前两步都放在try()中，因为在最后需要释放资源！
            //3. 执行SQL语句，并得到结果集
            ResultSet set = statement.executeQuery("select * from student");
            //4. 查看结果
            while (set.next()) {
                System.out.println(set.getString(1));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        //5. 释放资源，try-with-resource语法会自动帮助我们close
    }
}
```

### 基础认知

**DriverManager**：用于管理数据库驱动

**Connection**：是数据库的连接对象，可以通过连接对象来创建一个Statement用于执行SQL语句

**Statement**：执行DQL语句和DDL语句

### 执行DML操作

```
import java.sql.*;

public class Main {
    public static void main(String[] args) {
        try (Connection connection = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/study", "root", "cwz20031028");
             Statement statement = connection.createStatement()) {

            //插入数据
            statement.executeUpdate("insert into student values(1029249,'小黄','女')");

            //删除数据
            statement.executeUpdate("delete from student where sid = 1");

            //更新数据
            statement.executeUpdate("update student set name = '庄墙' where sid = 2");

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### 执行DQL操作

```
import java.sql.*;

public class Main {
    public static void main(String[] args) {
        try (Connection connection = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/study", "root", "cwz20031028");
             Statement statement = connection.createStatement()) {

            ResultSet set = statement.executeQuery("select * from student");
            while (set.next()){
                System.out.println(set.getInt(1));
                System.out.println(set.getString(2));
                System.out.println(set.getString(3));
            }

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### 执行批处理

一次性处理，提高操作效率

```
import java.sql.*;

public class Main {
    public static void main(String[] args) {
        try (Connection connection = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/study", "root", "cwz20031028");
             Statement statement = connection.createStatement()) {

            statement.addBatch("insert into teach values(1,1)");
            statement.addBatch("insert into teach values(2,2)");
            statement.addBatch("insert into teach values(3,3)");
            statement.addBatch("insert into teach values(4,4)");
            statement.addBatch("insert into teach values(5,5)");

            statement.executeBatch();

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### 将查询结果映射为对象

首先定义一个的实体类：

```
public class Student {
    Integer sid;
    String name;
    String sex;

    public Student(Integer sid, String name, String sex) {
        this.sid = sid;
        this.name = name;
        this.sex = sex;
    }

    public void say(){
        System.out.println("我叫："+name+"，学号为："+sid+"，我的性别是："+sex);
    }
}
```

进行一个转换：

```
import java.sql.*;

public class Main {
    public static void main(String[] args) {
        try (Connection connection = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/study", "root", "cwz20031028");
             Statement statement = connection.createStatement()) {

            ResultSet set = statement.executeQuery("select * from student");
            while(set.next()){
                Student student = new Student(set.getInt(1),set.getString(2),set.getString(3));
                student.say();
            }


        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### 实现登录与SQL注入攻击

模拟一个用户登录：

```
import java.sql.*;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        try (Connection connection = DriverManager.getConnection( "jdbc:mysql://localhost:3306/study", "root", "cwz20031028");
             Statement statement = connection.createStatement();
             Scanner scanner = new Scanner(System.in)){

            ResultSet res = statement.executeQuery("select * from user where username='"+scanner.nextLine()+"'and pwd='"+scanner.nextLine()+"';");
            while (res.next()){
                String username = res.getString(1);
                System.out.println(username+" 登陆成功！");
            }

        }catch (SQLException e){
            e.printStackTrace();
        }
    }
}
```

用户可以通过自己输入用户名和密码来登陆，乍一看好像没啥问题，那如果我输入的是以下内容呢：

```
Test
1111' or 1=1; -- 
# Test 登陆成功！
```

1=1一定是true，那么我们原本的SQL语句会变为：

select * from user where username='Test' and pwd='1111' or 1=1; -- '

如果允许这样的数据插入，那么我们原有的SQL语句结构就遭到了破坏，使得用户能够随意登陆别人的账号。因此我们可能需要限制用户的输入来防止用户输入一些SQL语句关键字，但是关键字非常多，这并不是解决问题的最好办法。

### PreparedStatement

我们发现，如果单纯地使用Statement来执行SQL命令，会存在严重的SQL注入攻击漏洞！而这种问题，我们可以使用PreparedStatement来解决：

```
import java.sql.*;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        try (Connection connection = DriverManager.getConnection( 
            "jdbc:mysql://localhost:3306/study", "root", "cwz20031028");
             PreparedStatement statement = connection.prepareStatement("select * from user where 
                                                                       username=? and pwd=?");
             Scanner scanner = new Scanner(System.in)){

            statement.setString(1, scanner.nextLine());
            statement.setString(2, scanner.nextLine());

            ResultSet res = statement.executeQuery();
            while (res.next()){
                String username = res.getString(1);
                System.out.println(username + "登录成功！");
            }


        }catch (SQLException e){
            e.printStackTrace();
        }
    }
}
```

需要提前给到PreparedStatement一个SQL语句，并且使用?作为占位符，它会预编译一个SQL语句，通过直接将我们的内容进行替换的方式来填写数据

### 管理事务

JDBC默认的事务处理行为是自动提交，所以前面我们执行一个SQL语句就会被直接提交（相当于没有启动事务），所以JDBC需要进行事务管理时，首先要通过Connection对象调用setAutoCommit(false) 方法, 将SQL语句的提交（commit）由驱动程序转交给应用程序负责。

```
con.setAutoCommit();   //关闭自动提交后相当于开启事务。
// SQL语句
// SQL语句
// SQL语句
con.commit();或 con.rollback();
```

一旦关闭自动提交，那么现在执行所有的操作如果在最后不进行commit()来提交事务的话，那么所有的操作都会丢失，只有提交之后，所有的操作才会被保存！也可以使用rollback()来手动回滚之前的全部操作！

```
public static void main(String[] args) throws ClassNotFoundException {
    try (Connection connection = DriverManager.getConnection("URL","用户名","密码");
         Statement statement = connection.createStatement()){

        connection.setAutoCommit(false);  //关闭自动提交，现在将变为我们手动提交
        statement.executeUpdate("insert into user values ('a', 1234)");
        statement.executeUpdate("insert into user values ('b', 1234)");
        statement.executeUpdate("insert into user values ('c', 1234)");

        connection.commit();   //如果前面任何操作出现异常，将不会执行commit()，之前的操作也就不会生效
    }catch (SQLException e){
        e.printStackTrace();
    }
}
```

## Lombok

### 基本操作

我们发现，在以往编写项目时，尤其是在类进行类内部成员字段封装时，需要编写大量的get/set方法，这不仅使得我们类定义中充满了get和set方法，同时如果字段名称发生改变，又要挨个进行修改，甚至当字段变得很多时，构造方法的编写会非常麻烦！

通过使用Lombok（小辣椒）就可以解决这样的问题！

```
public class Student {
    private Integer sid;
    private String name;
    private String sex;

    public Student(Integer sid, String name, String sex) {
        this.sid = sid;
        this.name = name;
        this.sex = sex;
    }

    public Integer getSid() {             
        return sid;
    }

    public void setSid(Integer sid) {     
        this.sid = sid;
    }

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
}
```

使用Lombok之后：

```
@Getter
@Setter
@AllArgsConstructor
public class Student {
    private Integer sid;
    private String name;
    private String sex;
}
```

使用Lombok之后，只需要添加几个注解，就能够解决掉我们之前长长的一串代码！

```
package com.test;

public class Main {
    public static void main(String[] args) {
        Student student = new Student(1,"小明", "男");
        System.out.println(student.getName());
    }
}
```

### 使用Lombok

- 我们通过添加@Getter和@Setter来为当前类的所有字段生成get/set方法，他们可以添加到类或是字段上，注意静态字段不会生成，final字段无法生成set方法。

- 我们还可以使用@Accessors来控制生成Getter和Setter的样式。

- 我们通过添加@ToString来为当前类生成预设的toString方法。
- 我们可以通过添加@EqualsAndHashCode来快速生成比较和哈希值方法。
- 我们可以通过添加@AllArgsConstructor和@NoArgsConstructor来快速生成全参构造和无参构造。
- 我们可以添加@RequiredArgsConstructor来快速生成参数只包含final或被标记为@NonNull的成员字段。
- 使用@Data能代表@Setter、@Getter、@RequiredArgsConstructor、@ToString、@EqualsAndHashCode全部注解。

- 一旦使用@Data就不建议此类有继承关系，因为equal方法可能不符合预期结果（尤其是仅比较子类属性）。

- 使用@Value与@Data类似，但是并不会生成setter并且成员属性都是final的。
- 使用@SneakyThrows来自动生成try-catch代码块。
- 使用@Cleanup作用与局部变量，在最后自动调用其close()方法（可以自由更换）
- 使用@Builder来快速生成建造者模式。

- 通过使用@Builder.Default来指定默认值。
- 通过使用@Builder.ObtainVia来指定默认值的获取方式。

## Mybatis

MyBatis 是一款优秀的持久层框架，它支持定制化 SQL、存储过程以及高级映射。MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。MyBatis 可以使用简单的 XML 或注解来配置和映射原生信息，将接口和 Java 的 POJOs(Plain Ordinary Java Object,普通的 Java对象)映射成数据库中的记录

### XML语言

**XML用来存放数据，更像一个配置文件**

```
<?xml version="1.0" encoding="UTF-8" ?>
<!-- 注释内容 -->
<outer>
	<name>阿伟</name>
	<desc>怎么又在玩电动啊</desc>
	<inner type="1">
    	<age>10</age>
        <sex>男</sex>
    </inner>
</outer>
```

XML文件存在以下的格式规范：

- 必须存在一个根节点，将所有的子标签全部包含
- 可以但不必须包含一个头部声明（主要是可以设定编码格式）
- 所有的标签必须成对出现，可以嵌套但不能交叉嵌套
- 区分大小写
- 标签中可以存在属性，比如上面的type="1"就是inner标签的一个属性，属性的值由单引号或双引号包括

可以使用CD来快速创建不解析区域：

```
<test>
    <name><![CDATA[我看你<><><>是一点都不懂哦>>>]]></name>
</test>
```

如何将xml文件读取到java程序中：

```
package com.test;

import org.w3c.dom.Document;
import org.w3c.dom.Node;
import org.w3c.dom.NodeList;

import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;

public class Main {
    public static void main(String[] args) {
        // 创建DocumentBuilderFactory对象
        DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
        // 创建DocumentBuilder对象
        try {
            DocumentBuilder builder = factory.newDocumentBuilder();
            Document d = builder.parse("file:text.xml");
            // 每一个标签都作为一个节点
            NodeList nodeList = d.getElementsByTagName("outer");  // 可能有很多个名字为test的标签
            Node rootNode = nodeList.item(0); // 获取首个
			// 一个节点下可能会有很多个节点，比如根节点下就囊括了所有的节点
            NodeList childNodes = rootNode.getChildNodes(); 
            //节点可以是一个带有内容的标签（它内部就还有子节点），也可以是一段文本内容

            for (int i = 0; i < childNodes.getLength(); i++) {
                Node child = childNodes.item(i);
                if(child.getNodeType() == Node.ELEMENT_NODE)  
                    //过滤换行符之类的内容，因为它们都被认为是一个文本节点
                    System.out.println(child.getNodeName() + "：" +child.getFirstChild().getNodeValue());
                
                // 输出节点名称，也就是标签名称，以及标签内部的文本（内部的内容都是子节点，所以要获取内部的节点）
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### 配置Mybatis

配置xml文件，输入相关信息

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/study"/>
                <property name="username" value="root"/>
                <property name="password" value="cwz20031028"/>
            </dataSource>
        </environment>
    </environments>
</configuration>
```

```
package com.test;

import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.FileInputStream;
import java.io.FileNotFoundException;

public class Main {
    public static void main(String[] args) throws FileNotFoundException {
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().
            									build(new 	FileInputStream("mybatis-config.xml"));
        try(SqlSession session = sqlSessionFactory.openSession(true)){

        }catch (Exception e){

        }

    }
}
```

由于SqlSessionFactory一般只需要创建一次，因此我们可以创建一个工具类来集中创建SqlSession：

```
package com.test;

import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.FileInputStream;
import java.io.FileNotFoundException;

public class MybatisUtil {

    //在类加载时就进行创建
    private static SqlSessionFactory sqlSessionFactory;
    static {
        try {
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(new FileInputStream("mybatis-config.xml"));
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
    }

    /**
     * 获取一个新的会话
     * @param autoCommit 是否开启自动提交（跟JDBC是一样的，如果不自动提交，则会变成事务操作）
     * @return SqlSession对象
     */
    public static SqlSession getSession(boolean autoCommit){
        return sqlSessionFactory.openSession(autoCommit);
    }
}
```

```
package com.test;

import org.apache.ibatis.session.SqlSession;


public class Main {
    public static void main(String[] args) {

        try(SqlSession session = MybatisUtil.getSession(true)){

        }

    }
}
```

### 复杂查询

一个老师可以教授多个学生，那么能否一次性将老师的学生全部映射给此老师的对象呢，比如：

```
@Data
public class Teacher {
    int tid;
    String name;
    List<Student> studentList;
}
```

映射为Teacher对象时，同时将其教授的所有学生一并映射为List列表，显然这是一种一对多的查询，那么这时就需要进行复杂查询了。而我们之前编写的都非常简单，直接就能完成映射，因此我们现在需要使用resultMap来自定义映射规则：

```
<select id="getTeacherByTid" resultMap="asTeacher">
        select *, teacher.name as tname from student inner join teach on student.sid = teach.sid
                              inner join teacher on teach.tid = teacher.tid where teach.tid = #{tid}
</select>

<resultMap id="asTeacher" type="Teacher">
    <id column="tid" property="tid"/>
    <result column="tname" property="name"/>
    <collection property="studentList" ofType="Student">
        <id property="sid" column="sid"/>
        <result column="name" property="name"/>
        <result column="sex" property="sex"/>
    </collection>
</resultMap>
```

可以看到，我们的查询结果是一个多表联查的结果，而联查的数据就是我们需要映射的数据（比如这里是一个老师有N个学生，联查的结果也是这一个老师对应N个学生的N条记录），其中id标签用于在多条记录中辨别是否为同一个对象的数据，比如上面的查询语句得到的结果中，tid这一行始终为1，因此所有的记录都应该是tid=1的教师的数据，而不应该变为多个教师的数据，如果不加id进行约束，那么会被识别成多个教师的数据

通过使用collection来表示将得到的所有结果合并为一个集合，比如上面的数据中每个学生都有单独的一条记录，因此tid相同的全部学生的记录就可以最后合并为一个List，得到最终的映射结果，当然，为了区分，最好也设置一个id，只不过这个例子中可以当做普通的result使用。

**多对一**

```
@Data
@Accessors(chain = true)
public class Student {
    private int sid;
    private String name;
    private String sex;
    private Teacher teacher;
}

@Data
public class Teacher {
    int tid;
    String name;
}
```

```
<resultMap id="test2" type="Student">
    <id column="sid" property="sid"/>
    <result column="name" property="name"/>
    <result column="sex" property="sex"/>
    <association property="teacher" javaType="Teacher">
        <id column="tid" property="tid"/>
        <result column="tname" property="name"/>
    </association>
</resultMap>
<select id="selectStudent" resultMap="test2">
    select *, teacher.name as tname from student left join teach on student.sid = teach.sid
                                                 left join teacher on teach.tid = teacher.tid
</select>
```

### 事务操作

我们可以在获取SqlSession关闭自动提交来开启事务模式，和JDBC其实都差不多：

```
public static void main(String[] args) {
    try (SqlSession sqlSession = MybatisUtil.getSession(false)){
        TestMapper testMapper = sqlSession.getMapper(TestMapper.class);

        testMapper.addStudent(new Student().setSex("男").setName("小王"));

        testMapper.selectStudent().forEach(System.out::println);
    }
}
```

我们发现，在关闭自动提交后，我们的内容是没有进入到数据库的，现在我们来试一下在最后提交事务：

sqlSession.commit();

在事务提交后，我们的内容才会被写入到数据库中。回滚操作：

```
try (SqlSession sqlSession = MybatisUtil.getSession(false)){
    TestMapper testMapper = sqlSession.getMapper(TestMapper.class);

    testMapper.addStudent(new Student().setSex("男").setName("小王"));

    testMapper.selectStudent().forEach(System.out::println);
    sqlSession.rollback();
    sqlSession.commit();
}
```

### 动态SQL

动态 SQL 是 MyBatis 的强大特性之一。如果你使用过 JDBC 或其它类似的框架，你应该能理解根据不同条件拼接 SQL 语句有多痛苦，例如拼接时要确保不能忘记添加必要的空格，还要注意去掉列表最后一个列名的逗号。利用动态 SQL，可以彻底摆脱这种痛苦。

```
<select id="getStudentSid" resultType="student">
    	select * from student where sid = #{sid}
		<if test="sid % 2 = 0">
            and sex="男"
        <if>
</select>
```

### 缓存机制

Mybatis存在一级缓存和二级缓存，我们首先来看一下一级缓存，默认情况下，只启用了本地的会话缓存，它仅仅对一个会话中的数据进行缓存（一级缓存无法关闭，只能调整），我们来看看下面这段代码：

```
public static void main(String[] args) throws InterruptedException {
    try (SqlSession sqlSession = MybatisUtil.getSession(true)){
        TestMapper testMapper = sqlSession.getMapper(TestMapper.class);
        Student student1 = testMapper.getStudentBySid(1);
        Student student2 = testMapper.getStudentBySid(1);
        System.out.println(student1 == student2);
    }
}
```

```
true
//代表数据在第一次的时候就放在一级缓存中
```

两次得到的是同一个Student对象，也就是说我们第二次查询并没有重新去构造对象，而是直接得到之前创建好的对象。如果还不是很明显，我们可以修改一下实体类：

```
@Data
@Accessors(chain = true)
public class Student {

    public Student(){
        System.out.println("我被构造了");
    }

    private int sid;
    private String name;
    private String sex;
}
```

如果修改了数据库中的内容，缓存还会生效吗：

```
public static void main(String[] args) throws InterruptedException {
    try (SqlSession sqlSession = MybatisUtil.getSession(true)){
        TestMapper testMapper = sqlSession.getMapper(TestMapper.class);
        Student student1 = testMapper.getStudentBySid(1);
        testMapper.addStudent(new Student().setName("小李").setSex("男"));
        Student student2 = testMapper.getStudentBySid(1);
        System.out.println(student1 == student2);
    }
}
```

当我们进行了插入操作后，缓存就没有生效了，我们再次进行查询得到的是一个新创建的对象。

也就是说，一级缓存，在进行DML操作后，会使得缓存失效，也就是说Mybatis知道我们对数据库里面的数据进行了修改，所以之前缓存的内容可能就不是当前数据库里面最新的内容了。还有一种情况就是，当前会话结束后，也会清理全部的缓存，因为已经不会再用到了。但是一定注意，一级缓存只针对于单个会话，多个会话之间不相通。

```
public static void main(String[] args) {
    try (SqlSession sqlSession = MybatisUtil.getSession(true)){
        TestMapper testMapper = sqlSession.getMapper(TestMapper.class);

        Student student2;
        try(SqlSession sqlSession2 = MybatisUtil.getSession(true)){
            TestMapper testMapper2 = sqlSession2.getMapper(TestMapper.class);
            student2 = testMapper2.getStudentBySid(1);
        }

        Student student1 = testMapper.getStudentBySid(1);
        System.out.println(student1 == student2);
    }
}
```

**注意：**一个会话DML操作只会重置当前会话的缓存，不会重置其他会话的缓存，也就是说，其他会话缓存是不会更新的！

一级缓存给我们提供了很高速的访问效率，但是它的作用范围实在是有限，如果一个会话结束，那么之前的缓存就全部失效了，但是我们希望缓存能够扩展到所有会话都能使用，因此我们可以通过二级缓存来实现，二级缓存默认是关闭状态，要开启二级缓存，我们需要在映射器XML文件中添加：

<cache/>

可见二级缓存是Mapper级别的，也就是说，当一个会话失效时，它的缓存依然会存在于二级缓存中，因此如果我们再次创建一个新的会话会直接使用之前的缓存，我们首先根据官方文档进行一些配置：

```
<cache
  eviction="FIFO"
  flushInterval="60000"
  size="512"
  readOnly="true"/>
```

```
public static void main(String[] args) {
    Student student;
    try (SqlSession sqlSession = MybatisUtil.getSession(true)){
        TestMapper testMapper = sqlSession.getMapper(TestMapper.class);
        student = testMapper.getStudentBySid(1);
    }

    try (SqlSession sqlSession2 = MybatisUtil.getSession(true)){
        TestMapper testMapper2 = sqlSession2.getMapper(TestMapper.class);
        Student student2 = testMapper2.getStudentBySid(1);
        System.out.println(student2 == student);
    }
}
```

上面的代码中首先是第一个会话在进行读操作，完成后会结束会话，而第二个操作重新创建了一个新的会话，再次执行了同样的查询，我们发现得到的依然是缓存的结果。

那么如果我不希望某个方法开启缓存呢？我们可以添加useCache属性来关闭缓存：

```
<select id="getStudentBySid" resultType="Student" useCache="false">
    select * from student where sid = #{sid}
</select>
```

我们也可以使用flushCache="false"在每次执行后都清空缓存，通过这这个我们还可以控制DML操作完成之后不清空缓存。

```
<select id="getStudentBySid" resultType="Student" flushCache="true">
    select * from student where sid = #{sid}
</select>
```

添加了二级缓存之后，会先从二级缓存中查找数据，当二级缓存中没有时，才会从一级缓存中获取，当一级缓存中都还没有数据时，才会请求数据库，因此我们再来执行上面的代码：

```
public static void main(String[] args) {
    try (SqlSession sqlSession = MybatisUtil.getSession(true)){
        TestMapper testMapper = sqlSession.getMapper(TestMapper.class);

        Student student2;
        try(SqlSession sqlSession2 = MybatisUtil.getSession(true)){
            TestMapper testMapper2 = sqlSession2.getMapper(TestMapper.class);
            student2 = testMapper2.getStudentBySid(1);
        }

        Student student1 = testMapper.getStudentBySid(1);
        System.out.println(student1 == student2);
    }
}
```

得到的结果就会是同一个对象了，因为现在是优先从二级缓存中获取。

读取顺序：二级缓存 => 一级缓存 => 数据库

### 使用注解开发

首先我们来看一下，使用XML进行映射器编写时，我们需要现在XML中定义映射规则和SQL语句，然后再将其绑定到一个接口的方法定义上，然后再使用接口来执行：

```
<insert id="addStudent">
    insert into student(name, sex) values(#{name}, #{sex})
</insert>
```

int addStudent(Student student);

而现在，我们可以直接使用注解来实现，每个操作都有一个对应的注解：

```
@Insert("insert into student(name, sex) values(#{name}, #{sex})")
int addStudent(Student student);
```

当然，我们还需要修改一下配置文件中的映射器注册：

```
<mappers>
    <mapper class="com.test.mapper.MyMapper"/>
    <!--  也可以直接注册整个包下的 <package name="com.test.mapper"/>  -->
</mappers>
```

通过直接指定Class，来让Mybatis知道我们这里有一个通过注解实现的映射器。

我们接着来看一下，如何使用注解进行自定义映射规则：

```
@Results({
        @Result(id = true, column = "sid", property = "sid"),
        @Result(column = "sex", property = "name"),
        @Result(column = "name", property = "sex")
})
@Select("select * from student")
List<Student> getAllStudent();
```

直接通过@Results注解，就可以直接进行配置了，此注解的value是一个@Result注解数组，每个@Result注解都都一个单独的字段配置，其实就是我们之前在XML映射器中写的：

```
<resultMap id="test" type="Student">
    <id property="sid" column="sid"/>
    <result column="name" property="sex"/>    
  	<result column="sex" property="name"/>
</resultMap>
```

以通过注解来自定义映射规则了。那么如何使用注解来完成复杂查询呢？

```
@Results({
        @Result(id = true, column = "tid", property = "tid"),
        @Result(column = "name", property = "name"),
        @Result(column = "tid", property = "studentList", many =
            @Many(select = "getStudentByTid")
        )
})
@Select("select * from teacher where tid = #{tid}")
Teacher getTeacherBySid(int tid);

@Select("select * from student inner join teach on student.sid = teach.sid where tid = #{tid}")
List<Student> getStudentByTid(int tid);
```

我们发现，多出了一个子查询，而这个子查询是单独查询该老师所属学生的信息，而子查询结果作为@Result注解的一个many结果，代表子查询的所有结果都归入此集合中（也就是之前的collection标签）

```
<resultMap id="asTeacher" type="Teacher">
    <id column="tid" property="tid"/>
    <result column="tname" property="name"/>
    <collection property="studentList" ofType="Student">
        <id property="sid" column="sid"/>
        <result column="name" property="name"/>
        <result column="sex" property="sex"/>
    </collection>
</resultMap>
```

同理，@Result也提供了@One子注解来实现一对一的关系表示，类似于之前的assocation标签：

```
@Results({
        @Result(id = true, column = "sid", property = "sid"),
        @Result(column = "sex", property = "name"),
        @Result(column = "name", property = "sex"),
        @Result(column = "sid", property = "teacher", one =
            @One(select = "getTeacherBySid")
        )
})
@Select("select * from student")
List<Student> getAllStudent();
```

如果现在我希望直接使用注解编写SQL语句但是我希望映射规则依然使用XML来实现，这时该怎么办呢？

```
@ResultMap("test")
@Select("select * from student")
List<Student> getAllStudent();
```

提供了@ResultMap注解，直接指定ID即可，这样我们就可以使用XML中编写的映射规则了，这里就不再演示了。

那么如果出现之前的两个构造方法的情况，且没有任何一个构造方法匹配的话，该怎么处理呢？

```
@Data
@Accessors(chain = true)
public class Student {

    public Student(int sid){
        System.out.println("我是一号构造方法"+sid);
    }

    public Student(int sid, String name){
        System.out.println("我是二号构造方法"+sid+name);
    }

    private int sid;
    private String name;
    private String sex;
}
```

我们可以通过@ConstructorArgs注解来指定构造方法：

```
@ConstructorArgs({
        @Arg(column = "sid", javaType = int.class),
        @Arg(column = "name", javaType = String.class)
})
@Select("select * from student where sid = #{sid} and sex = #{sex}")
Student getStudentBySidAndSex(@Param("sid") int sid, @Param("sex") String sex);
```

得到的结果和使用constructor标签效果一致，这里就不多做讲解了。

我们发现，当参数列表中出现两个以上的参数时，会出现错误：

```
@Select("select * from student where sid = #{sid} and sex = #{sex}")
Student getStudentBySidAndSex(int sid, String sex);
```

```
Exception in thread "main" org.apache.ibatis.exceptions.PersistenceException: 
### Error querying database.  Cause: org.apache.ibatis.binding.BindingException: Parameter 'sid' not found. Available parameters are [arg1, arg0, param1, param2]
### Cause: org.apache.ibatis.binding.BindingException: Parameter 'sid' not found. Available parameters are [arg1, arg0, param1, param2]
	at org.apache.ibatis.exceptions.ExceptionFactory.wrapException(ExceptionFactory.java:30)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.selectList(DefaultSqlSession.java:153)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.selectList(DefaultSqlSession.java:145)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.selectList(DefaultSqlSession.java:140)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.selectOne(DefaultSqlSession.java:76)
	at org.apache.ibatis.binding.MapperMethod.execute(MapperMethod.java:87)
	at org.apache.ibatis.binding.MapperProxy$PlainMethodInvoker.invoke(MapperProxy.java:145)
	at org.apache.ibatis.binding.MapperProxy.invoke(MapperProxy.java:86)
	at com.sun.proxy.$Proxy6.getStudentBySidAndSex(Unknown Source)
	at com.test.Main.main(Main.java:16)
```

原因是Mybatis不明确到底哪个参数是什么，因此我们可以添加@Param来指定参数名称：

```
@Select("select * from student where sid = #{sid} and sex = #{sex}")
Student getStudentBySidAndSex(@Param("sid") int sid, @Param("sex") String sex);
```

**探究：**要是我两个参数一个是基本类型一个是对象类型呢？

System.out.println(testMapper.addStudent(100, new Student().setName("小陆").setSex("男")));

```
@Insert("insert into student(sid, name, sex) values(#{sid}, #{name}, #{sex})")
int addStudent(@Param("sid") int sid, @Param("student")  Student student);
```

那么这个时候，就出现问题了，Mybatis就不能明确这些属性是从哪里来的：

```
### SQL: insert into student(sid, name, sex) values(?, ?, ?)
### Cause: org.apache.ibatis.binding.BindingException: Parameter 'name' not found. Available parameters are [student, param1, sid, param2]
	at org.apache.ibatis.exceptions.ExceptionFactory.wrapException(ExceptionFactory.java:30)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.update(DefaultSqlSession.java:196)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.insert(DefaultSqlSession.java:181)
	at org.apache.ibatis.binding.MapperMethod.execute(MapperMethod.java:62)
	at org.apache.ibatis.binding.MapperProxy$PlainMethodInvoker.invoke(MapperProxy.java:145)
	at org.apache.ibatis.binding.MapperProxy.invoke(MapperProxy.java:86)
	at com.sun.proxy.$Proxy6.addStudent(Unknown Source)
	at com.test.Main.main(Main.java:16)
```

那么我们就通过参数名称.属性的方式去让Mybatis知道我们要用的是哪个属性：

```
@Insert("insert into student(sid, name, sex) values(#{sid}, #{student.name}, #{student.sex})")
int addStudent(@Param("sid") int sid, @Param("student")  Student student);
```

那么如何通过注解控制缓存机制呢？

```
@CacheNamespace(readWrite = false)
public interface MyMapper {

    @Select("select * from student")
    @Options(useCache = false)
    List<Student> getAllStudent();
```

使用@CacheNamespace注解直接定义在接口上即可，然后我们可以通过使用@Options来控制单个操作的缓存启用。

### 探究Mybatis的动态代理机制

在探究动态代理机制之前，我们要先聊聊什么是代理：其实顾名思义，就好比我开了个大棚，里面栽种的西瓜，那么西瓜成熟了是不是得去卖掉赚钱，而我们的西瓜非常多，一个人肯定卖不过来，肯定就要去多找几个开水果摊的帮我们卖，这就是一种代理。实际上是由水果摊老板在帮我们卖瓜，我们只告诉老板卖多少钱，而至于怎么卖的是由水果摊老板决定的。

那么现在我们来尝试实现一下这样的类结构，首先定义一个接口用于规范行为：

```
public interface Shopper {

    //卖瓜行为
    void saleWatermelon(String customer);
}
```

然后需要实现一下卖瓜行为，也就是我们要告诉老板卖多少钱，这里就直接写成成功出售：

```
public class ShopperImpl implements Shopper{

    //卖瓜行为的实现
    @Override
    public void saleWatermelon(String customer) {
        System.out.println("成功出售西瓜给 ===> "+customer);
    }
}
```

最后老板代理后肯定要用自己的方式去出售这些西瓜，成交之后再按照我们告诉老板的价格进行出售：

```
public class ShopperProxy implements Shopper{

    private final Shopper impl;

    public ShopperProxy(Shopper impl){
        this.impl = impl;
    }

    //代理卖瓜行为
    @Override
    public void saleWatermelon(String customer) {
        //首先进行 代理商讨价还价行为
        System.out.println(customer + "：哥们，这瓜多少钱一斤啊？");
        System.out.println("老板：两块钱一斤。");
        System.out.println(customer + "：你这瓜皮子是金子做的，还是瓜粒子是金子做的？");
        System.out.println("老板：你瞅瞅现在哪有瓜啊，这都是大棚的瓜，你嫌贵我还嫌贵呢。");
        System.out.println(customer + "：给我挑一个。");

        impl.saleWatermelon(customer);   //讨价还价成功，进行我们告诉代理商的卖瓜行为
    }
}
```

现在我们来试试看：

```
public class Main {
    public static void main(String[] args) {
        Shopper shopper = new ShopperProxy(new ShopperImpl());
        shopper.saleWatermelon("小强");
    }
}
```

这样的操作称为静态代理，也就是说我们需要提前知道接口的定义并进行实现才可以完成代理，而Mybatis这样的是无法预知代理接口的，我们就需要用到动态代理。

JDK提供的反射框架就为我们很好地解决了动态代理的问题，在这里相当于对JavaSE阶段反射的内容进行一个补充。

```
public class ShopperProxy implements InvocationHandler {

    Object target;
    public ShopperProxy(Object target){
        this.target = target;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        String customer = (String) args[0];
        System.out.println(customer + "：哥们，这瓜多少钱一斤啊？");
        System.out.println("老板：两块钱一斤。");
        System.out.println(customer + "：你这瓜皮子是金子做的，还是瓜粒子是金子做的？");
        System.out.println("老板：你瞅瞅现在哪有瓜啊，这都是大棚的瓜，你嫌贵我还嫌贵呢。");
        System.out.println(customer + "：行，给我挑一个。");
        return method.invoke(target, args);
    }
}
```

通过实现InvocationHandler来成为一个动态代理，我们发现它提供了一个invoke方法，用于调用被代理对象的方法并完成我们的代理工作。现在就可以通过Proxy.newProxyInstance来生成一个动态代理类：

```
public static void main(String[] args) {
    Shopper impl = new ShopperImpl();
    Shopper shopper = (Shopper) Proxy.newProxyInstance(impl.getClass().getClassLoader(),
            impl.getClass().getInterfaces(), new ShopperProxy(impl));
    shopper.saleWatermelon("小强");
  	System.out.println(shopper.getClass());
}
```

通过打印类型我们发现，就是我们之前看到的那种奇怪的类：class com.sun.proxy.$Proxy0，因此Mybatis其实也是这样的来实现的（肯定有人问了：Mybatis是直接代理接口啊，你这个不还是要把接口实现了吗？）那我们来改改，现在我们不代理任何类了，直接做接口实现：

```
public class ShopperProxy implements InvocationHandler {

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        String customer = (String) args[0];
        System.out.println(customer + "：哥们，这瓜多少钱一斤啊？");
        System.out.println("老板：两块钱一斤。");
        System.out.println(customer + "：你这瓜皮子是金子做的，还是瓜粒子是金子做的？");
        System.out.println("老板：你瞅瞅现在哪有瓜啊，这都是大棚的瓜，你嫌贵我还嫌贵呢。");
        System.out.println(customer + "：行，给我挑一个。");
        return null;
    }
}
```

```
public static void main(String[] args) {
    Shopper shopper = (Shopper) Proxy.newProxyInstance(Shopper.class.getClassLoader(),
            new Class[]{ Shopper.class },   //因为本身就是接口，所以直接用就行
            new ShopperProxy());
    shopper.saleWatermelon("小强");
    System.out.println(shopper.getClass());
}
```

我们可以去看看Mybatis的源码。

Mybatis的学习差不多就到这里为止了，不过，同样类型的框架还有很多，Mybatis属于半自动框架，SQL语句依然需要我们自己编写，虽然存在一定的麻烦，但是会更加灵活，而后面我们还会学习JPA，它是全自动的框架，你几乎见不到SQL的影子！

## JUnit

### 单元测试框架

```
package com.test.test;

import org.junit.Test;

public class MainTest {
    @Test
    public void method(){
        System.out.println("我是测试用例1");
    }

    @Test
    public void method2(){
        System.out.println("我是测试用例2");
    }
}
```

我们可以点击类前面的测试按钮，或是单个方法前的测试按钮，如果点击类前面的测试按钮，会执行所有的测试用例。

运行测试后，我们发现控制台得到了一个测试结果，显示为绿色表示测试通过。

只需要通过打上@Test注解，即可将一个方法标记为测试案例，我们可以直接运行此测试案例，但是我们编写的测试方法有以下要求：

- 方法必须是public的
- 不能是静态方法
- 返回值必须是void
- 必须是没有任何参数的方法

对于一个测试案例来说，我们肯定希望测试的结果是我们所期望的一个值，因此，如果测试的结果并不是我们所期望的结果，那么这个测试就应该没有成功通过！

我们可以通过**断言工具类**来进行判定：

```
package com.test.test;

import org.junit.Assert;
import org.junit.Test;

public class MainTest {
    @Test
    public void method(){
        System.out.println("我是测试用例1");
        Assert.assertEquals(1,2);
    }

    @Test
    public void method2(){
        System.out.println("我是测试用例2");
    }
}
```

如果我们想做一些前置的操作，通过@Before注解添加测试用例开始前置操作：

```
public class TestMain {

    private SqlSessionFactory sqlSessionFactory;
    @Before
    public void before(){
        System.out.println("测试前置正在初始化...");
        try {
            sqlSessionFactory = new SqlSessionFactoryBuilder()
                    .build(new FileInputStream("mybatis-config.xml"));
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
        System.out.println("测试初始化完成，正在开始测试案例...");
    }

    @Test
    public void method1(){
        try (SqlSession sqlSession = sqlSessionFactory.openSession(true)){
            TestMapper mapper = sqlSession.getMapper(TestMapper.class);
            Student student = mapper.getStudentBySidAndSex(1, "男");

            Assert.assertEquals(new Student().setName("小明").setSex("男").setSid(1), student);
            System.out.println("测试用例1通过！");
        }
    }

    @Test
    public void method2(){
        try (SqlSession sqlSession = sqlSessionFactory.openSession(true)){
            TestMapper mapper = sqlSession.getMapper(TestMapper.class);
            Student student = mapper.getStudentBySidAndSex(2, "女");

            Assert.assertEquals(new Student().setName("小红").setSex("女").setSid(2), student);
            System.out.println("测试用例2通过！");
        }
    }
}
```

还想添加一个收尾的动作，那么只需要使用@After注解即可添加结束动作：

```
@After
public void after(){
    System.out.println("测试结束，收尾工作正在进行...");
}
```

## JUL日志系统

目的：使用日志规范我们的输出

```
public class Main {
    public static void main(String[] args) {
      	// 首先获取日志打印器
        Logger logger = Logger.getLogger(Main.class.getName());
      	// 调用info来输出一个普通的信息，直接填写字符串即可
        logger.info("我是普通的日志");
    }
}
```

```
一月 29, 2024 1:06:41 下午 com.test.Main main
信息: 我是一个日志信息

进程已结束，退出代码为 0
```

### JUL日志讲解

日志分为7个级别，详细信息我们可以在Level类中查看：

- SEVERE（最高值）- 一般用于代表严重错误
- WARNING - 一般用于表示某些警告，但是不足以判断为错误
- INFO （默认级别） - 常规消息
- CONFIG
- FINE
- FINER
- FINEST（最低值）

我们之前通过info方法直接输出的结果就是使用的默认级别的日志，我们可以通过log方法来设定该条日志的输出级别：

```
public static void main(String[] args) {
    Logger logger = Logger.getLogger(Main.class.getName());
    logger.log(Level.SEVERE, "严重的错误", new IOException("我就是错误"));
    logger.log(Level.WARNING, "警告的内容");
    logger.log(Level.INFO, "普通的信息");
    logger.log(Level.CONFIG, "级别低于普通信息");
}
```

级别低于默认级别的日志信息，无法输出到控制台，我们可以通过设置来修改日志的打印级别：

好处：可以给根据需求调整等级--->过滤器

```
public static void main(String[] args) {
    Logger logger = Logger.getLogger(Main.class.getName());

    //修改日志级别
    logger.setLevel(Level.CONFIG);
    //不使用父日志处理器
    logger.setUseParentHandlers(false);
    //使用自定义日志处理器
    ConsoleHandler handler = new ConsoleHandler();
    handler.setLevel(Level.CONFIG);
    logger.addHandler(handler);

    logger.log(Level.SEVERE, "严重的错误", new IOException("我就是错误"));
    logger.log(Level.WARNING, "警告的内容");
    logger.log(Level.INFO, "普通的信息");
    logger.log(Level.CONFIG, "级别低于普通信息");
}
```

每个Logger都有一个父日志打印器，我们可以通过getParent()来获取：

```
public static void main(String[] args) throws IOException {
    Logger logger = Logger.getLogger(Main.class.getName());
    System.out.println(logger.getParent().getClass());
}
```

得到的是java.util.logging.LogManager$RootLogger这个类，它默认使用的是ConsoleHandler，且日志级别为INFO，由于每一个日志打印器都会直接使用父类的处理器，因此我们之前需要关闭父类然后使用我们自己的处理器。

通过使用自己日志处理器来自定义级别的信息打印到控制台，当然，日志处理器不仅仅只有控制台打印，我们也可以使用文件处理器来处理日志信息，我们继续添加一个处理器：

```
//添加输出到本地文件
FileHandler fileHandler = new FileHandler("test.log");
fileHandler.setLevel(Level.WARNING);
logger.addHandler(fileHandler);
```

注意，这个时候就有两个日志处理器了，因此控制台和文件的都会生效。如果日志的打印格式我们不喜欢，我们还可以自定义打印格式，比如我们控制台处理器就默认使用的是SimpleFormatter，而文件处理器则是使用的XMLFormatter，我们可以自定义：

```
//使用自定义日志处理器(控制台)
ConsoleHandler handler = new ConsoleHandler();
handler.setLevel(Level.CONFIG);
handler.setFormatter(new XMLFormatter());
logger.addHandler(handler);
```

我们可以直接配置为想要的打印格式，如果这些格式还不能满足你，那么我们也可以自行实现：

```
public static void main(String[] args) throws IOException {
    Logger logger = Logger.getLogger(Main.class.getName());
    logger.setUseParentHandlers(false);

    //为了让颜色变回普通的颜色，通过代码块在初始化时将输出流设定为System.out
    ConsoleHandler handler = new ConsoleHandler(){{
        setOutputStream(System.out);
    }};
    //创建匿名内部类实现自定义的格式
    handler.setFormatter(new Formatter() {
        @Override
        public String format(LogRecord record) {
            SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss.SSS");
            String time = format.format(new Date(record.getMillis()));  //格式化日志时间
            String level = record.getLevel().getName();  // 获取日志级别名称
            // String level = record.getLevel().getLocalizedName();   // 获取本地化名称（语言跟随系统）
            String thread = String.format("%10s", Thread.currentThread().getName());  //线程名称（做了格式化处理，留出10格空间）
            long threadID = record.getThreadID();   //线程ID
            String className = String.format("%-20s", record.getSourceClassName());  //发送日志的类名
            String msg = record.getMessage();   //日志消息

          //\033[33m作为颜色代码，30~37都有对应的颜色，38是没有颜色，IDEA能显示，但是某些地方可能不支持
            return "\033[38m" + time + "  \033[33m" + level + " \033[35m" + threadID
                    + "\033[38m --- [" + thread + "] \033[36m" + className + "\033[38m : " + msg + "\n";
        }
    });
    logger.addHandler(handler);

    logger.info("我是测试消息1...");
    logger.log(Level.INFO, "我是测试消息2...");
    logger.log(Level.WARNING, "我是测试消息3...");
}
```

日志可以设置过滤器，如果我们不希望某些日志信息被输出，我们可以配置过滤规则：

```
public static void main(String[] args) throws IOException {
    Logger logger = Logger.getLogger(Main.class.getName());

    //自定义过滤规则
    logger.setFilter(record -> !record.getMessage().contains("普通"));

    logger.log(Level.SEVERE, "严重的错误", new IOException("我就是错误"));
    logger.log(Level.WARNING, "警告的内容");
    logger.log(Level.INFO, "普通的信息");
}
```

### Properties配置文件

```
name=Test
desc=Description
```

该文件配置很简单，格式为配置项=配置值，我们可以直接通过Properties类来将其读取为一个类似于Map一样的对象：

```
public static void main(String[] args) throws IOException {
    Properties properties = new Properties();
    properties.load(new FileInputStream("test.properties"));
    System.out.println(properties);
}
```

Properties类是继承自Hashtable，而Hashtable是实现的Map接口，也就是说，Properties本质上就是一个Map一样的结构，它会把所有的配置项映射为一个Map，这样我们就可以快速地读取对应配置的值了。

我们也可以将已经存在的Properties对象放入输出流进行保存，我们这里就不保存文件了，而是直接打印到控制台，我们只需要提供输出流即可：

```
public static void main(String[] args) throws IOException {
    Properties properties = new Properties();
  	// properties.setProperty("test", "lbwnb");  //和put效果一样
    properties.put("test", "lbwnb");
    properties.store(System.out, "????");
  	//properties.storeToXML(System.out, "????");  保存为XML格式
}
```

可以通过System.getProperties()获取系统的参数：

```
public static void main(String[] args) throws IOException {
    System.getProperties().store(System.out, "系统信息：");
}
```

### 编写日志配置文件

通过进行配置文件来规定日志打印器的一些默认值：

```
# RootLogger 的默认处理器为
handlers= java.util.logging.ConsoleHandler
# RootLogger 的默认的日志级别
.level= CONFIG
```

使用配置文件来进行配置：

```
public static void main(String[] args) throws IOException {
    //获取日志管理器
    LogManager manager = LogManager.getLogManager();
    //读取我们自己的配置文件
    manager.readConfiguration(new FileInputStream("logging.properties"));
    //再获取日志打印器
    Logger logger = Logger.getLogger(Main.class.getName());
    logger.log(Level.CONFIG, "我是一条日志信息");   //通过自定义配置文件，我们发现默认级别不再是INFO了
}
```

修改ConsoleHandler的默认配置：

```
# 指定默认日志级别
java.util.logging.ConsoleHandler.level = ALL
# 指定默认日志消息格式
java.util.logging.ConsoleHandler.formatter = java.util.logging.SimpleFormatter
# 指定默认的字符集
java.util.logging.ConsoleHandler.encoding = UTF-8
```

其实，我们阅读ConsoleHandler的源码就会发现，它就是通过读取配置文件来进行某些参数设置：

```
// Private method to configure a ConsoleHandler from LogManager
// properties and/or default values as specified in the class
// javadoc.
private void configure() {
    LogManager manager = LogManager.getLogManager();
    String cname = getClass().getName();

    setLevel(manager.getLevelProperty(cname +".level", Level.INFO));
    setFilter(manager.getFilterProperty(cname +".filter", null));
    setFormatter(manager.getFormatterProperty(cname +".formatter", new SimpleFormatter()));
    try {
        setEncoding(manager.getStringProperty(cname +".encoding", null));
    } catch (Exception ex) {
        try {
            setEncoding(null);
        } catch (Exception ex2) {
            // doing a setEncoding with null should always work.
            // assert false;
        }
    }
}
```

###

### 使用Lombok快速开启日志

我们发现，如果我们现在需要全面使用日志系统，而不是传统的直接打印，那么就需要在每个类都去编写获取Logger的代码，这样显然是很冗余的，能否简化一下这个流程呢？

**Logger也是可以使用Lombok快速生成的**

```
@Log
public class Main {
    public static void main(String[] args) {
        System.out.println("自动生成的Logger名称："+log.getName());
        log.info("我是日志信息");
    }
}
```

只需要添加一个@Log注解即可，添加后，我们可以直接使用一个静态变量log，而它就是自动生成的Logger。我们也可以手动指定名称：

```
@Log(topic = "打工是不可能打工的")
public class Main {
    public static void main(String[] args) {
        System.out.println("自动生成的Logger名称："+log.getName());
        log.info("我是日志信息");
    }
}
```

### Mybatis日志系统

Mybatis也有日志系统，它详细记录了所有的数据库操作等，监控所有的数据库操作，要开启日志系统，我们需要进行配置：

<setting name="logImpl" value="STDOUT_LOGGING" />

logImpl包括很多种配置项，包括 SLF4J | LOG4J | LOG4J2 | JDK_LOGGING | COMMONS_LOGGING | STDOUT_LOGGING | NO_LOGGING，而默认情况下是未配置，也就是说不打印。我们这里将其设定为STDOUT_LOGGING表示直接使用标准输出将日志信息打印到控制台，下面是一个测试案例：

```
public class TestMain {

    private SqlSessionFactory sqlSessionFactory;
    @Before
    public void before(){
        try {
            sqlSessionFactory = new SqlSessionFactoryBuilder()
                    .build(new FileInputStream("mybatis-config.xml"));
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
    }

    @Test
    public void test(){
        try(SqlSession sqlSession = sqlSessionFactory.openSession(true)){
            TestMapper mapper = sqlSession.getMapper(TestMapper.class);
            System.out.println(mapper.getStudentBySidAndSex(1, "男"));
            System.out.println(mapper.getStudentBySidAndSex(1, "男"));
        }
    }
}
```

我们发现，两次获取学生信息，只有第一次打开了数据库连接，而第二次并没有。

现在我们学习了日志系统，那么我们来尝试使用日志系统输出Mybatis的日志信息：

<setting name="logImpl" value="JDK_LOGGING" />

将其配置为JDK_LOGGING表示使用JUL进行日志打印，因为Mybatis的日志级别都比较低，因此我们需要设置一下logging.properties默认的日志级别：

```
handlers= java.util.logging.ConsoleHandler
.level= ALL
java.util.logging.ConsoleHandler.level = ALL
```

代码编写如下：

```
@Log
public class TestMain {

    private SqlSessionFactory sqlSessionFactory;
    @Before
    public void before(){
        try {
            sqlSessionFactory = new SqlSessionFactoryBuilder()
                    .build(new FileInputStream("mybatis-config.xml"));
            LogManager manager = LogManager.getLogManager();
            manager.readConfiguration(new FileInputStream("logging.properties"));
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    @Test
    public void test(){
        try(SqlSession sqlSession = sqlSessionFactory.openSession(true)){
            TestMapper mapper = sqlSession.getMapper(TestMapper.class);
            log.info(mapper.getStudentBySidAndSex(1, "男").toString());
            log.info(mapper.getStudentBySidAndSex(1, "男").toString());
        }
    }
}
```

但是我们发现，这样的日志信息根本没法看，因此我们需要修改一下日志的打印格式，我们自己创建一个格式化类：

```
public class TestFormatter extends Formatter {
    @Override
    public String format(LogRecord record) {
        SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss.SSS");
        String time = format.format(new Date(record.getMillis()));  //格式化日志时间
        return time + " : " + record.getMessage() + "\n";
    }
}
```

现在再来修改一下默认的格式化实现：

```
handlers= java.util.logging.ConsoleHandler
.level= ALL
java.util.logging.ConsoleHandler.level = ALL
java.util.logging.ConsoleHandler.formatter = com.test.TestFormatter
```

## Maven

### 使用Maven管理项目

Maven 翻译为"专家"、"内行"，是 Apache 下的一个纯 Java 开发的开源项目。基于项目对象模型（缩写：POM）概念，Maven利用一个中央信息片断能管理一个项目的构建、报告和文档等步骤。Maven 是一个项目管理工具，可以对 Java 项目进行构建、依赖管理。

通过Maven，可以帮助我们做：

- 项目的自动构建，包括代码的编译、测试、打包、安装、部署等操作。
- 依赖管理，项目使用到哪些依赖，可以快速完成导入。

### Maven项目结构

我们需要了解一下POM文件，它相当于是我们整个Maven项目的配置文件，它也是使用XML编写的：

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>MavenTest</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

</project>
```

我们可以看到，Maven的配置文件是以project为根节点，而modelVersion定义了当前模型的版本，一般是4.0.0，我们不用去修改。

groupId、artifactId、version这三个元素合在一起，用于唯一区别每个项目，别人如果需要将我们编写的代码作为依赖，那么就必须通过**这三个元素来定位我们的项目**，我们称为一个项目的基本坐标，所有的项目一般都有自己的Maven坐标，因此我们通过Maven导入其他的依赖只需要填写这三个基本元素就可以了，无需再下载Jar文件，而是Maven自动帮助我们下载依赖并导入。

- groupId 一般用于指定组名称，命名规则一般和包名一致，比如我们这里使用的是org.example，一个组下面可以有很多个项目。
- artifactId 一般用于指定项目在当前组中的唯一名称，也就是说在组中用于区分于其他项目的标记。
- version 代表项目版本，随着我们项目的开发和改进，版本号也会不断更新，就像LOL一样，每次赛季更新都会有一个大版本更新，我们的Maven项目也是这样，我们可以手动指定当前项目的版本号，其他人使用我们的项目作为依赖时，也可以根本版本号进行选择（这里的SNAPSHOT代表快照，一般表示这是一个处于开发中的项目，正式发布项目一般只带版本号）

properties中一般都是一些变量和选项的配置，我们这里指定了JDK的源代码和编译版本为1.8，无需进行修改。

### Maven依赖导入

现在我们尝试使用Maven来帮助我们快速导入依赖，我们需要导入之前的JDBC驱动依赖、JUnit依赖、Mybatis依赖、Lombok依赖，那么如何使用Maven来管理依赖呢？

我们可以创建一个dependencies节点：

```
<dependencies>
    //里面填写的就是所有的依赖
</dependencies>
```

那么现在就可以向节点中填写依赖了，那么我们如何知道每个依赖的坐标呢？我们可以在：[https://mvnrepository.com/](https://mvnrepository.com/) 进行查询（可能打不开，建议用流量，或是直接百度某个项目的Maven依赖），我们直接搜索lombok即可，打开后可以看到已经给我们写出了依赖的坐标：

```
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.22</version>
    <scope>provided</scope>
</dependency>
```

我们直接将其添加到dependencies节点中即可，现在我们来编写一个测试用例看看依赖导入成功了没有：

```
public class Main {
    public static void main(String[] args) {
        Student student = new Student("小明", 18);
        System.out.println(student);
    }
}
```

```
@Data
@AllArgsConstructor
public class Student {
    String name;
    int age;
}
```

项目运行成功，表示成功导入了依赖。那么，Maven是如何进行依赖管理呢，以致于如此便捷的导入依赖，我们来看看Maven项目的依赖管理流程：

### Maven依赖作用域

除了三个基本的属性用于定位坐标外，依赖还可以添加以下属性：

- **type**：依赖的类型，对于项目坐标定义的packaging。大部分情况下，该元素不必声明，其默认值为jar
- **scope**：依赖的范围（作用域，着重讲解）
- **optional**：标记依赖是否可选
- **exclusions**：用来排除传递性依赖（一个项目有可能依赖于其他项目，就像我们的项目，如果别人要用我们的项目作为依赖，那么就需要一起下载我们项目的依赖，如Lombok）

我们着重来讲解一下scope属性，它决定了依赖的作用域范围：

- **compile** ：为默认的依赖有效范围。如果在定义依赖关系的时候，没有明确指定依赖有效范围的话，则默认采用该依赖有效范围。此种依赖，在编译、运行、测试时均有效。
- **provided** ：在编译、测试时有效，但是在运行时无效，也就是说，项目在运行时，不需要此依赖，比如我们上面的Lombok，我们只需要在编译阶段使用它，编译完成后，实际上已经转换为对应的代码了，因此Lombok不需要在项目运行时也存在。
- **runtime** ：在运行、测试时有效，但是在编译代码时无效。比如我们如果需要自己写一个JDBC实现，那么肯定要用到JDK为我们指定的接口，但是实际上在运行时是不用自带JDK的依赖，因此只保留我们自己写的内容即可。
- **test** ：只在测试时有效，例如：JUnit，我们一般只会在测试阶段使用JUnit，而实际项目运行时，我们就用不到测试了，那么我们来看看，导入JUnit的依赖：

同样的，我们可以在网站上搜索Junit的依赖，我们这里导入最新的JUnit5作为依赖：

```
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.8.1</version>
    <scope>test</scope>
</dependency>
```

我们所有的测试用例全部编写到Maven项目给我们划分的test目录下，位于此目录下的内容不会在最后被打包到项目中，只用作开发阶段测试使用：

```
public class MainTest {

    @Test
    public void test(){
        System.out.println("测试");
      	//Assert在JUnit5时名称发生了变化Assertions
        Assertions.assertArrayEquals(new int[]{1, 2, 3}, new int[]{1, 2});
    }
}
```

因此，一般仅用作测试的依赖如JUnit只保留在测试中即可，那么现在我们再来添加JDBC和Mybatis的依赖：

```
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.27</version>
</dependency>
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.7</version>
</dependency>
```

我们发现，Maven还给我们提供了一个resource文件夹，我们可以将一些静态资源，比如配置文件，放入到这个文件夹中，项目在打包时会将资源文件夹中文件一起打包的Jar中，比如我们在这里编写一个Mybatis的配置文件：

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <settings>
        <setting name="mapUnderscoreToCamelCase" value="true"/>
        <setting name="cacheEnabled" value="true"/>
        <setting name="logImpl" value="JDK_LOGGING" />
    </settings>
    <!-- 需要在environments的上方 -->
    <typeAliases>
        <package name="com.test.entity"/>
    </typeAliases>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/study"/>
                <property name="username" value="test"/>
                <property name="password" value="123456"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <mapper class="com.test.mapper.TestMapper"/>
    </mappers>
</configuration>
```

现在我们创建一下测试用例，顺便带大家了解一下Junit5的一些比较方便的地方：

```
public class MainTest {

    //因为配置文件位于内部，我们需要使用Resources类的getResourceAsStream来获取内部的资源文件
    private static SqlSessionFactory factory;

    //在JUnit5中@Before被废弃，它被细分了：
    @BeforeAll // 一次性开启所有测试案例只会执行一次 (方法必须是static)
    // @BeforeEach 一次性开启所有测试案例每个案例开始之前都会执行一次
    @SneakyThrows
    public static void before(){
        factory = new SqlSessionFactoryBuilder()
                .build(Resources.getResourceAsStream("mybatis.xml"));
    }


    @DisplayName("Mybatis数据库测试")  //自定义测试名称
    @RepeatedTest(3)  //自动执行多次测试
    public void test(){
        try (SqlSession sqlSession = factory.openSession(true)){
            TestMapper testMapper = sqlSession.getMapper(TestMapper.class);
            System.out.println(testMapper.getStudentBySid(1));
        }
    }
}
```

那么就有人提问了，如果我需要的依赖没有上传的远程仓库，而是只有一个Jar怎么办呢？我们可以使用第四种作用域：

- **system**：作用域和provided是一样的，但是它不是从远程仓库获取，而是直接导入本地Jar包：

```
<dependency>
     <groupId>javax.jntm</groupId>
     <artifactId>lbwnb</artifactId>
     <version>2.0</version>
     <scope>system</scope>
     <systemPath>C://学习资料/4K高清无码/test.jar</systemPath>
</dependency>
```

### Maven可选依赖

当项目中的某些依赖不希望被使用此项目作为依赖的项目使用时，我们可以给依赖添加optional标签表示此依赖是可选的，默认在导入依赖时，不会导入可选的依赖：

<optional>true</optional>

比如Mybatis的POM文件中，就存在大量的可选依赖：

```
<dependency>
  <groupId>org.slf4j</groupId>
  <artifactId>slf4j-api</artifactId>
  <version>1.7.30</version>
  <optional>true</optional>
</dependency>
<dependency>
  <groupId>org.slf4j</groupId>
  <artifactId>slf4j-log4j12</artifactId>
  <version>1.7.30</version>
  <optional>true</optional>
</dependency>
<dependency>
  <groupId>log4j</groupId>
  <artifactId>log4j</artifactId>
  <version>1.2.17</version>
  <optional>true</optional>
</dependency>
 ...
```

由于Mybatis要支持多种类型的日志，需要用到很多种不同的日志框架，因此需要导入这些依赖来做兼容，但是我们项目中并不一定会使用这些日志框架作为Mybatis的日志打印器，因此这些日志框架仅Mybatis内部做兼容需要导入使用，而我们可以选择不使用这些框架或是选择其中一个即可，也就是说我们导入Mybatis之后想用什么日志框架再自己加就可以了。

### Maven排除依赖

默认不使用可选依赖，但是如果存在那种不是可选依赖，但是我们导入此项目有不希望使用此依赖该怎么办呢，这个时候我们就可以通过排除依赖来防止添加不必要的依赖：

```
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.8.1</version>
    <scope>test</scope>
    <exclusions>
        <exclusion>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

### Maven继承关系

一个Maven项目可以继承自另一个Maven项目，比如多个子项目都需要父项目的依赖，我们就可以使用继承关系来快速配置。

我们右键左侧栏，新建一个模块，来创建一个子项目：

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>MavenTest</artifactId>
        <groupId>org.example</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>ChildModel</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

</project>
```

我们可以看到，IDEA默认给我们添加了一个parent节点，表示此Maven项目是父Maven项目的子项目，子项目直接继承父项目的groupId，子项目会直接继承父项目的所有依赖，除非依赖添加了optional标签，我们来编写一个测试用例尝试一下:

```
import lombok.extern.java.Log;

@Log
public class Main {
    public static void main(String[] args) {
        log.info("我是日志信息");
    }
}
```

可以看到，子项目也成功继承了Lombok依赖。

我们还可以让父Maven项目统一管理所有的依赖，包括版本号等，子项目可以选取需要的作为依赖，而版本全由父项目管理，我们可以将dependencies全部放入dependencyManagement节点，这样父项目就完全作为依赖统一管理。

```
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.22</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>5.8.1</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.27</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.7</version>
        </dependency>
    </dependencies>
</dependencyManagement>
```

我们发现，子项目的依赖失效了，因为现在父项目没有依赖，而是将所有的依赖进行集中管理，子项目需要什么再拿什么即可，同时子项目无需指定版本，所有的版本全部由父项目决定，子项目只需要使用即可：

```
<dependencies>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <scope>provided</scope>
    </dependency>
</dependencies>
```

当然，父项目如果还存在dependencies节点的话，里面的内依赖依然是直接继承：

```
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>5.8.1</version>
        <scope>test</scope>
    </dependency>
</dependencies>

<dependencyManagement>
    <dependencies>
      ...
```

### Maven常用命令

我们可以看到在IDEA右上角Maven板块中，每个Maven项目都有一个生命周期，实际上这些是Maven的一些插件，每个插件都有各自的功能，比如：

- clean命令，执行后会清理整个target文件夹，在之后编写Springboot项目时可以解决一些缓存没更新的问题。
- validate命令可以验证项目的可用性。
- compile命令可以将项目编译为.class文件。
- install命令可以将当前项目安装到本地仓库，以供其他项目导入作为依赖使用
- verify命令可以按顺序执行每个默认生命周期阶段（validate，compile，package等）

### Maven测试项目

通过使用test命令，可以一键测试所有位于test目录下的测试案例，请注意有以下要求：

- 测试类的名称必须是以Test结尾，比如MainTest
- 测试方法上必须标注@Test注解，实测@RepeatedTest无效

这是由于JUnit5比较新，我们需要重新配置插件升级到高版本，才能完美的兼容Junit5：

```
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <!-- JUnit 5 requires Surefire version 2.22.0 or higher -->
            <version>2.22.0</version>
        </plugin>
    </plugins>
</build>
```

现在@RepeatedTest、@BeforeAll也能使用了。

### Maven打包项目

我们的项目在编写完成之后，要么作为Jar依赖，供其他模型使用，要么就作为一个可以执行的程序，在控制台运行，我们只需要直接执行package命令就可以直接对项目的代码进行打包，生成jar文件。

当然，以上方式仅适用于作为Jar依赖的情况，如果我们需要打包一个可执行文件，那么我不仅需要将自己编写的类打包到Jar中，同时还需要将依赖也一并打包到Jar中，因为我们使用了别人为我们通过的框架，自然也需要运行别人的代码，我们需要使用另一个插件来实现一起打包：

```
<plugin>
    <artifactId>maven-assembly-plugin</artifactId>
    <version>3.1.0</version>
    <configuration>
        <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
        </descriptorRefs>
        <archive>
            <manifest>
                <addClasspath>true</addClasspath>
                <mainClass>com.test.Main</mainClass>
            </manifest>
        </archive>
    </configuration>
    <executions>
        <execution>
            <id>make-assembly</id>
            <phase>package</phase>
            <goals>
                <goal>single</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

在打包之前也会执行一次test命令，来保证项目能够正常运行，当测试出现问题时，打包将无法完成，我们也可以手动跳过，选择执行Maven目标来手动执行Maven命令，输入mvn package -Dmaven.test.skip=true来以跳过测试的方式进行打包。

最后得到我们的Jar文件，在同级目录下输入java -jar xxxx.jar来运行我们打包好的Jar可执行程序（xxx代表文件名称）

- deploy命令用于发布项目到本地仓库和远程仓库
- site命令用于生成当前项目的发布站点，暂时不需要了解。

我们之前还讲解了多模块项目，那么多模块下父项目存在一个packing打包类型标签，所有的父级项目的packing都为pom，packing默认是jar类型，如果不作配置，maven会将该项目打成jar包。作为父级项目，还有一个重要的属性，那就是modules，通过modules标签将项目的所有子项目引用进来，在build父级项目时，会根据子模块的相互依赖关系整理一个build顺序，然后依次build。

## 前端基础

- 前端：我们网站的页面，包括网站的样式、图片、视频等一切用户可见的内容都是前端的内容。
- 后端：处理网站的所有数据来源，比如我们之前从数据库中查询数据，而我们查询的数据经过处理最终会被展示到前端，而用于处理前端数据的工作就是由后端来完成的。

相当于，前端仅仅是一层皮，它直接决定了整个网站的美观程度，我们可以自由地编排页面的布局，甚至可以编写好看的特效；而灵魂则是后端，如何处理用户的交互、如何处理数据查询是后端的职责所在，我们前面学习的都是后端内容，而Java也是一门专注于后端开发的语言。

### HTML页面

#### 第一个HTML页面

通过浏览器可以直接浏览XML文件，而浏览器一般是用于浏览HTML文件的，以HTML语言编写的内容，会被浏览器识别为一个页面，并根据我们编写的内容，将对应的组件添加到浏览器窗口中。

我们可以创建一个Html文件来看看浏览器会如何识别，使用IDEA也能编写HTML页面，我们在IDEA中新建一个Web模块，进入之后我们发现，项目中没有任何内容，我们右键新建一个HTML文件，选择HTML5文件，并命名为index，创建后出现：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

</body>
</html>
```

我们发现，它和XML基本长得一样，并且还自带了一些标签，那么现在我们通过浏览器来浏览这个HTML文件（这里推荐使用内置预览，不然还得来回切换窗口）

我们发现现在什么东西都没有，但是在浏览器的标签位置显示了网页的名称为Title，并且显示了一个IDEA的图标作为网页图标。

现在我们稍微进行一些修改：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>lbw的直播间</title>
</head>
<body>
    现在全体起立
</body>
</html>
```

我们还可以在页面中添加一个图片，随便将一张图片放到html文件的同级目录下，命名为image.xxx，其中xxx是后缀名称，不要修改，我们在body节点中添加以下内容：

```
<img width="300" src="image.xxx" alt="剑光如我，斩尽牛杂">
<!--  注意xxx替换成对应的后缀名称  -->
```

我们发现，我们的页面中居然能够显示我们添加的图片内容。因此，我们只需要编写对应的标签，浏览器就能够自动识别为对应的组件，并将其展示到我们的浏览器窗口中。

我们再来看看插入一个B站的视频，很简单，只需要到对应的视频下方，找到分享，我们看到有一个嵌入代码：

<iframe src="//player.bilibili.com/player.html?aid=333231998&bvid=BV1rA411g7q8&cid=346917516&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" width="800" height="500"> </iframe>

每一个页面都是通过这些标签来编写的，几乎所有的网站都是使用HTML编写页面。

#### HTML语法规范

一个HTML文件中一般分为两个部分：

- 头部：一般包含页面的标题、页面的图标、还有页面的一些设置，也可以在这里导入css、js等内容。
- 主体：整个页面所有需要显示的内容全部在主体编写。

我们首先来看头部，我们之前使用的HTML文件中头部包含了这些内容：

```
<meta charset="UTF-8">
<title>lbw的直播间</title>
```

首先meta标签用于定义页面的一些元信息，这里使用它来定义了一个字符集（编码格式），一般是UTF-8，下面的title标签就是页面的标题，会显示在浏览器的上方。我们现在来给页面设置一个图标，图标一般可以在字节跳动的IconPark网站找到：[https://iconpark.oceanengine.com/home](https://iconpark.oceanengine.com/home)，选择一个自己喜欢的图标下载即可。

将图标放入到项目目录中，并命名为icon.png，在HTML头部添加以下内容：

<link rel="icon" href="icon.png" type="image/x-icon" />

link标签用于关联当前HTML页面与其他资源的关系，关系通过rel属性指定，这里使用的是icon表示这个文件是当前页面图标。

在主体内部编写该页面要展示的所有内容，比如我们之前就用到了img标签来展示一个图片，其中每一个标签都称为一个元素：

<img width="300" src="image.xxx" alt="当图片加载失败时，显示的文本">

我们发现，这个标签只存在一个，并没有成对出现，HTML中有些标签是单标签，也就是说只有这一个，还有一些标签是双标签，必须成对出现，HTML中，也不允许交叉嵌套，但是出现交叉嵌套时，浏览器并不会提示错误，而是仍旧尝试去解析这些内容，甚至会帮助我们进行一定程度的修复，比如：

```
<body>

    <iframe src="//player.bilibili.com/player.html?aid=333231998&bvid=BV1rA411g7q8&cid=346917516&page=1" width="800" height="500"
            scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true">
</body>
</iframe>
```

很明显上面的代码已经出现交叉嵌套的情况了，但是依然能够在浏览器中正确地显示。

在主体中，我们一般使用div标签来分割页面：

```
<body>
    <div>我是第一块</div>
    <div>我是第二块</div>
</body>
```

通过使用div标签，我们将整个页面按行划分，而高度就是内部元素的高度，那么如果只希望按元素划分，也就是说元素占多大就划分多大的空间，那么我们就可以使用span标签来划分：

```
<body>
    <div>
        <span>我是第一块第一个部分</span>
        <span>我是第一块第二个部分</span>
    </div>
    <div>我是第二块</div>
</body>
```

我们也可以使用p段落标签，它一般用于文章分段：

```
<body>
    <p>
        你看这个彬彬啊，才喝几罐就醉了，真的太逊了。 这个彬彬就是逊呀！
        听你这么说，你很勇哦？ 开玩笑，我超勇的，超会喝的啦。
        超会喝，很勇嘛。身材不错哦，蛮结实的嘛。
    </p>
    <p>
        哎，杰哥，你干嘛啊。都几岁了，还那么害羞！我看你，完全是不懂哦！
        懂，懂什么啊？ 你想懂？我房里有一些好康的。
        好康，是新游戏哦！ 什么新游戏，比游戏还刺激！
    </p>
    <p>
        杰哥，这是什么啊？ 哎呦，你脸红啦！来，让我看看。
        不要啦！！ 让我看看嘛。 不要啦，杰哥，你干嘛啊！
        让我看看你法语正不正常啊！
    </p>
</body>
```

那么如果遇到特殊字符该怎么办呢？和XML一样，我们可以使用转义字符：

![](https://cdn.nlark.com/yuque/0/2024/jpeg/43159521/1711506834806-3cffc397-f58c-4b16-b3e1-fef3cbd5bda6.jpeg)

**注意：**多个连续的空格字符只能被识别为一个，如果需要连续多个必须使用转义字符，同时也不会识别换行，换行只会变成一个空格，需要换行必须使用br标签。

通过了解了HTML的一些基础语法，我们现在就知道一个页面大致是如何编写了。

#### HTML常用标签

前面我们已经了解了HTML的基本语法规范，那么现在我们就来看看，有哪些常用的标签吧，首先是换行和分割线：

- br 换行
- hr 分割线

```
<body>
    <div>
        我是一段文字<br>我是第二段文字
    </div>
    <hr>
    <div>我是底部文字</div>
</body>
```

标题一般用h1到h6表示，我们来看看效果：

```
<body>
<h1>一级标题</h1>
<h2>二级标题</h2>
<h3>三级标题</h3>
<h4>四级标题</h4>
<h5>五级标题</h5>
<h6>六级标题</h6>
<p>我是正文内容，真不错。</p>
</body>
```

现在我们来看看超链接，我们可以添加一个链接用于指向其他网站：

<a href="https://www.bilibili.com">点击访问小破站</a>

我们也可以指定页面上的一个锚点进行滚动：

```
<body>
<a href="#test">跳转锚点</a>
<img src="image.jpeg" width="500">
<img src="image.jpeg" width="500">
<img src="image.jpeg" width="500">
<img src="image.jpeg" width="500">
<div id="test">我是锚点</div>
<img src="image.jpeg" width="500">
<img src="image.jpeg" width="500">
<img src="image.jpeg" width="500">
</body>
```

每个元素都可以有一个id属性，我们只需要给元素添加一个id属性，就使用a标签可以跳转到一个指定锚点。

我们接着来看看列表元素，这是一个无需列表，其中每一个li表示一个列表项：

```
<ul>
    <li>一号选项</li>
    <li>二号选项</li>
    <li>三号选项</li>
    <li>四号选项</li>
    <li>五号选项</li>
</ul>
```

我们也可以使用ol来显示一个有序列表：

```
<ol>
    <li>一号选项</li>
    <li>二号选项</li>
    <li>三号选项</li>
    <li>四号选项</li>
    <li>五号选项</li>
</ol>
```

表格也是很重要的一种元素，但是它编写起来相对有一点麻烦：

```
<table>
    <thead>
    <tr>
        <th>学号</th>
        <th>姓名</th>
        <th>性别</th>
        <th>年级</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>0001</td>
        <td>小明</td>
        <td>男</td>
        <td>2019</td>
    </tr>
    <tr>
        <td>0002</td>
        <td>小红</td>
        <td>女</td>
        <td>2020</td>
    </tr>
    </tbody>
</table>
```

虽然这样生成了一个表格，但是这个表格并没有分割线，并且格式也不符合我们想要的样式，那么如何才能修改这些基础属性的样式呢，我们就需要聊聊CSS了。

#### HTML表单

表单就像其名字一样，用户在页面中填写了对应的内容，点击按钮就可以提交到后台，比如登陆界面，就可以使用表单来实现：

一个网页中最重要的当属输入框和按钮了，那么我们来看看如何创建一个输入框和按钮：

```
<label>
    我是输入框
    <input type="text">
</label>
```

对于一个输入框，我们一般会将其包括在一个lable标签中，它和span效果一样，但是我们点击前面文字也能快速获取输入框焦点。

```
<body>
<div>登陆我们的网站</div>
<hr>
<div>
    <label>
        账号：
        <input type="text">
    </label>
</div>
<div>
    <label>
        密码：
        <input type="password">
    </label>
</div>
</body>
```

输入框可以有很多类型，我们来试试看password，现在输入内容就不会直接展示原文了。

创建一个按钮有以下几种方式，在学习JavaWeb时，我们更推荐第二种方式，我们后面进行登陆操作需要配合表单使用：

```
<button>登陆</button>
<input type="submit" value="登陆">
<input type="button" value="登陆">
```

现在我们就可以写一个大致的登陆页面了：

```
<body>
    <h1>登陆我们的网站</h1>
    <form>
        <div>
            <label>
                账号：
                <input type="text" placeholder="Username...">
            </label>
        </div>
        <div>
            <label>
                密码：
                <input type="password" placeholder="Password...">
            </label>
        </div>
        <br>
        <a href="https://www.baidu.com">忘记密码</a>
        <br>
        <br>
        <div>
            <input type="submit" value="登陆">
        </div>
    </form>
</body>
```

表单一般使用form标签将其囊括，但是现在我们还用不到表单提交，因此之后我们再来讲解表单的提交。

input只能实现单行文本，那么如何实现多行文本呢？

```
<label>
    这是我们的文本框<br>
    <textarea placeholder="文本内容..." cols="10" rows="10"></textarea>
</label>
```

我们还可以指定默认的行数和列数，拖动左下角可以自定义文本框的大小。

我们还可以在页面中添加勾选框：

```
<label>
    <input type="checkbox">
    我同意本网站的隐私政策
</label>
```

上面演示的是一个多选框，那么我们来看看单选框：

```
<label>
    <input type="radio" name="role">
    学生
</label>
<label>
    <input type="radio" name="role">
    教师
</label>
```

这里需要使用name属性进行分组，同一个组内的选项只能选择一个。

我们也可以添加列表让用户进行选择，创建一个下拉列表：

```
<label>
    登陆身份：
    <select>
        <option>学生</option>
        <option>教师</option>
    </select>
</label>
```

默认选取的是第一个选项，我们可以通过selected属性来决定默认使用的是哪个选项。

当然，HTML的元素远不止我们所提到的这些，有关更多HTML元素的内容，可以自行了解。

### CSS样式

首先我们创建一个名为style.css的文件。

首先在我们HTML文件的头部添加：

<link href="style.css" rel="stylesheet">

我们在CSS文件中添加以下内容：

```
body {
    text-align: center;
}
```

网页的内容全部变为居中显示了

当然，我们也可以选择不使用CSS，而是直接对某个元素添加样式：

```
<body style="text-align: center;">
  ...
```

这样的效果其实是等同于上面的css文件的，相当于我们直接把样式定义在指定元素上。

也可以在头部直接定义样式，而不是使用外部文件：

```
<style>
    body {
        text-align: center;
    }
</style>
```

使用以上三种方式都可以自定义页面的样式，我们推荐使用还是第一种，不然我们的代码会很繁杂。

样式的属性是非常多的，我们不可能一个一个全部讲完，视频中用到什么再来讲解什么，如果同学们感兴趣，可以自行下去了解。

#### CSS选择器

```
input {
    width: 200px;
}
```

页面中所有的input元素宽度全部被设定为了200个像素（px是单位大小，代表像素，除了px还有em和rem，他们是根据当前元素字体大小决定的相对大小，一般用于适配各种大小的浏览器窗口，这里暂时不用）

样式编写完成后，如果只有一个属性，可以不带;若多个属性则每个属性后面都需要添加一个;

因此，一个标签选择器的格式为：

```
标签名称 {
  属性名称: 属性值
}
```

我们还可以设定输入框的字体大小、行高等：

```
input {
    width: 200px;
    font-size: 20px;
    line-height: 40px;
}
```

现在可以通过选择器快速地去设置某个元素样式了，那么如何实现只设置某个元素的样式呢，现在我们来看看，id选择器，我们之前已经讲解过了，每个元素都可以有一个id属性，我们可以将其当做一个跳转的锚点使用，而现在，我们可以使用css来进行定位：

我们先为元素添加id属性：

<h1 id="title">登陆我们的网站</h1>

现在使用CSS选择我们的元素，并设定一个属性，选择某个id需要在前面加上一个#：

```
#title {
    color: red;
}
```

每个元素都可以有一个class属性，表示当前元素属于某个类（注意这里的类和我们Java中的类概念完全不同）一个元素可以属于很多个类，一个类也可以被很多个元素使用：

```
<form>
    <div >
        <label class="test">
            账号：
            <input type="text" placeholder="Username...">
        </label>
    </div>
    <div>
        <label class="test">
            密码：
            <input type="password" placeholder="Password...">
        </label>
    </div>
</form>
```

上面的例子中，两个label元素都使用了test类（类名称是我们自定义的），现在我们在css文件中编写以下内容来以类进行选择：

```
.test{
    color: blue;
}
```

#### 组合选择器和优先级问题

我们也可以让多个选择器，共用一个css样式：

```
.test, #title {
    color: red;
}
```

只需要并排写即可，注意中间需要添加一个英文的逗号用于分割，我们也可以使用*来一次性选择所有的元素：

```
* {
    color: red;
}
```

我们还可以选择位于某个元素内的某个元素：

```
div label {
    color: red;
}
```

这样的话，就会选择所有位于div元素中的label元素。

当然，我们这里只介绍了一些常用的选择器，有关详细的CSS选择器可以查阅：[https://www.runoob.com/cssref/css-selectors.html](https://www.runoob.com/cssref/css-selectors.html)

#### 自定义边距

我们来看看，如何使用css控制一个div板块的样式，首先编写以下代码，相当于一个div嵌套了一个div元素：

```
<div id="outer">
    <div id="inner">
        
    </div>
</div>
```

现在编写一下自定义的css样式，我们将div设定为固定大小，并且背景颜色添加为绿色：

```
#outer {
    background: palegreen;
    width: 300px;
    height: 300px;
}
```

我们发现左侧快速预览页面存在空隙，这是因为浏览器给我们添加了一个边距属性，我们只需要覆盖此属性并将其设定为0即可：

```
body {
    margin: 0;
}
```

现在我们给内部嵌套的div也设定一个大小，并将颜色设定为橙色：

```
#inner {
    background: darkorange;
    width: 100px;
    height: 100px;
}
```

现在我们发现内部的div元素位于右上角，我们还可以以百分比的形式来指定大小：

```
#inner {
    background: darkorange;
    width: 100%;
    height: 100%;
}
```

百分比会依照当前可用大小来进行分配，比如当前位于一个div内部，并且外部div元素是固定大小300px，因此100%就相当于使用了外部的全部大小，也是300px，现在内部元素完全将外部元素覆盖了，整个元素现在呈现为橙色。

我们可以为一个元素设定边距，边距分为外边距和内边距，外部元素内边距决定了内部元素与外部元素之间的间隔，我们来修改一下css样式：

```
#outer {
    background: palegreen;
    width: 300px;
    height: 300px;
    padding: 10px;
}
```

我们发现，内部的div元素小了一圈，这是因为外部div元素设定了内边距，上下左右都被设定为10px大小。

而我们发现，实际上我们在一开始也是将body的外边距设定为了0，整个页面跟浏览器窗口直接间隔0px的宽度。

### JavaScript语言

相当于是前端静态页面的一个补充，它可以让一个普通的页面在后台执行一些程序，比如我们点击一个按钮，我们可能希望执行某些操作，比如下载文件、页面跳转、页面弹窗、进行登陆等，都可以使用JavaScript来帮助我们实现。

我们来看看一个简单的JavaScript程序：

```
const arr = [0, 2, 1, 5, 9, 3, 4, 6, 7, 8]

for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - 1; j++) {
        if(arr[j] > arr[j+1]){
            const tmp = arr[j]
            arr[j] = arr[j+1]
            arr[j+1] = tmp
        }
    }
}

window.alert(arr)
```

这段代码实际上就是实现了一个冒泡排序算法，我们可以直接在页面的头部中引用此js文件，浏览器会在加载时自动执行js文件中编写的内容：

<script src="test.js"></script>

我们发现JS的语法和Java非常相似，但是它还是和Java存在一些不同之处，而且存在很多阴间语法，那么我们来看看JS的语法。

#### JavaScript基本语法

在js中，定义变量和Java中有一些不同，定义一个变量可以使用let关键字或是var关键字，IDEA推荐我们使用let关键字，因为var存在一定的设计缺陷（这里就不做讲解了，之后一律使用let关键字进行变量声明）：

```
let a = 10;
a++;
window.alert(a)
```

js并不是Java那样的强类型语言（任意变量的类型一定是明确的），它是一门弱类型语言，变量的类型并不会在一开始确定，因此我们在定义变量时无需指定变量的确切类型，而是在运行时动态解析类型：

```
let a = 10;
a = "HelloWorld！"
console.info(a)
```

我们发现，变量a已经被赋值为数字类型，但是我们依然在后续能将其赋值一个字符串，它的类型是随时可变的。

我们接着来看看，JS中存在的基本数据类型：

- Number：数字类型（包括小数和整数）
- String：字符串类型（可以使用单引号或是双引号）
- Boolean：布尔类型（与Java一致）

还包括一些特殊值：

- undefined：未定义 - 变量声明但不赋值默认为undefined
- null：空值 - 等同于Java中的null
- NaN：非数字 - 值不是合法数字，比如：window.alert(100/'xx')

我们可以使用typeof关键字来查看当前变量值的类型：

```
let a = 10;
console.info(typeof a)
a = 'Hello World'
console.info(typeof a)
```

#### JavaScript逻辑运算和流程控制

我们接着来看看js中的关系运算符，包括如下8个关系运算符：大于（>）,小于（<）,小于等于（<=）,大于等于（>=）,相等（==），不等（!=），全等（===），不全等（!==）

其实关系运算符大致和Java中的使用方法一致，不过它还可以进行字符串比较，有点像C++的语法：

```
console.info(666 > 777)
console.info('aa' > 'ab')
```

那么，相等和全等有什么区别呢？

```
console.info('10' == 10)
console.info('10' === 10)
```

==的比较规则是：当操作数类型一样时，比较的规则和恒等运算符一样，都相等才相等，如果两个操作数是字符串，则进行字符串的比较，如果里面有一个操作数不是字符串，那两个操作数通过Number()方法进行转换，转成数字进行比较。

因此，我们上面进行的判断实际上是运算符两边都进行了数字转换的结果进行比较，自然也就得到了true，而全等判断才是我们在Java中认识的相等判断。

我们接着来看逻辑运算，JS中包括&&、||、&、|、?:等，我们先来看看位运算符：

```
console.info(4 & 7)
console.info(4 | 7)
```

实际上和Java中是一样的，那么我再来看看逻辑运算：

console.info(true || false)

对于boolean变量的判断，是与Java一致的，但是JS也可以使用非Boolen类型变量进行判断：

```
console.info(!0)
console.info(!1)
```

和C/C++语言一样，0代表false，非0代表true，那么字符串呢？

```
console.info(!"a")
console.info(!"")
```

我们发现，空串为false，非空串为true，我们再来看看：

```
console.info(true || 7)
console.info(7 || true)
```

我们发现，前者得到的结果为true，而后者得到的结果却是是7，真是滑天下之大稽，什么鬼玩意，实际上是因为，默认非0都是true，而后者又是先判断的7，因此会直接得到7而不是被转换为true

那么我们再来看看几个特殊值默认代表什么：

```
console.info(!undefined)
console.info(!null)
console.info(!NaN)
```

最后来使用一下三元运算符，实际上和Java中是一样的：

```
let a = true ? "xx" : 20
console.info(a)
```

得益于JS的动态类型，emmm，三元运算符不一定需要固定的返回值类型。

JS的分支结构，实际上和Java是一样的，也是使用if-else语句来进行：

```
if("lbwnb"){   //非空串为true
    console.info("!!!")
} else {
    console.info("???")
}
```

同理，多分支语句也能实现：

```
if(""){
    console.info("!!!")
} else if(-666){
    console.info("???")
} else {
    console.info("O.O")
}
```

当然，多分支语句也可以使用switch来完成：

```
let a = "a"
switch (a){
    case "a":
        console.info("1")
        break
    case "b":
        console.info("2")
        break
    case "c":
        console.info("3")
        break
    default:
        console.info("4")
}
```

接着我们来看看循环结构，其实循环结构也和Java相差不大：

```
let i = 10
while(i--){
    console.info("100")
}
```

```
for (let i = 0; i < 10; i++) {
    console.info("??")
}
```

#### JavaScript函数定义

JS中的方法和Java中的方法定义不太一样，JS中一般称其为函数，我们来看看定义一个函数的格式是什么：

```
function f() {
    console.info("有一个人前来买瓜")
}
```

定义一个函数，需要在前面加上function关键字表示这是一个函数，后面跟上函数名称和()，其中可以包含参数，在{}中编写函数代码。我们只需要直接使用函数名+()就能调用函数：

f();

我们接着来看一下，如何给函数添加形式参数以及返回值：

```
function f(a) {
    console.info("得到的实参为："+a)
    return 666
}

f("aa");
```

由于JS是动态类型，因此我们不必指明参数a的类型，同时也不必指明返回值的类型，一个函数可能返回不同类型的结果，因此直接编写return语句即可。同理，我们可以在调用函数时，不传参，那么默认会使用undefined：

```
function f(a) {
    console.info("得到的实参为："+a)
    return 666
}

f();
```

那么如果我们希望不传参的时候使用我们自定义的默认值呢？

```
function f(a = "6666") {
    console.info("得到的实参为："+a)
    return 666
}

f();
```

我们可以直接在形参后面指定默认值。

函数本身也是一种类型，他可以被变量接收，所有函数类型的变量，也可以直接被调用：

```
function f(a = "6666") {
    console.info("得到的实参为："+a)
    return 666
}

let k = f;
k();
```

我们也可以直接将匿名函数赋值给变量：

```
let f = function (str) {
    console.info("实参为："+str)
}
```

既然函数是一种类型，那么函数也能作为一个参数进行传递：

```
function f(test) {
    test();
}

f(function () {
    console.info("这是一个匿名函数")
})
```

对于所有的匿名函数，可以像Java的匿名接口实现一样编写lambda表达式：

```
function f(test) {
    test();
}

f(() => {
    console.info("可以，不跟你多bb")
})
```

```
function f(test) {
    test("这个是回调参数");
}

f(param => {
    console.info("接受到回调参数："+param)
})
```

#### JavaScript数组和对象

JS中的数组定义与Java不同，它更像是Python中的列表，数组中的每个元素并不需要时同样的类型：

let arr = [1, "lbwnb", false, undefined, NaN]

我们可以直接使用下标来访问：

```
let arr = [1, "lbwnb", false, undefined, NaN]
console.info(arr[1])
```

我们一开始编写的排序算法，也是使用了数组。

数组还可以动态扩容，如果我们尝试访问超出数组长度的元素，并不会出现错误，而是得到undefined，同样的，我们也可以直接往超出数组长度的地方设置元素：

```
let arr = [1, "lbwnb", false, undefined, NaN]
arr[5] = "???"
console.info(arr)
```

也可以使用push和pop来实现栈操作：

```
let arr = [1, "lbwnb", false, undefined, NaN]
arr.push("bbb")
console.info(arr.pop())
console.info(arr)
```

数组还包括一些其他的方法，这里就不一一列出了：

```
let arr = [1, "lbwnb", false, undefined, NaN]
arr.fill(1)
console.info(arr.map(o => {
    return 'xxx'+o
}))
```

我们接着来看对象，JS中也能定义对象，但是这里的对象有点颠覆我们的认知：

```
let obj = new Object()
let obj = {}
```

以上两种写法都能够创建一个对象，但是更推荐使用下面的一种。

JS中的对象也是非常随意的，我们可以动态为其添加属性：

```
let obj = {}
obj.name = "伞兵一号"
console.info(obj)
```

同理，我们也可以给对象动态添加一个函数：

```
let obj = {}
obj.f = function (){
    console.info("我是对象内部的函数")
}

obj.f()
```

我们可以在函数内使用this关键字来指定对象内的属性：

```
let name = "我是外部变量"
let obj = {}
obj.name = "我是内部变量"
obj.f = function (){
    console.info("name属性为："+this.name)
}

obj.f()
```

**注意：**如果使用lambda表达式，那么this并不会指向对象。

除了动态添加属性，我们也可以在一开始的时候指定对象内部的成员：

```
let obj = {
    name: "我是内部的变量",
  	f: function (){
        console.info("name属性为："+this.name)
    }
}

obj.f()
```

注意如果有多行属性，需要在属性定义后添加一个,进行分割！

#### JavaScript事件

当我们点击一个页面中的按钮之后，我们希望之后能够进行登陆操作，或是执行一些JS代码来实现某些功能，那么这个时候，就需要用到事件。

事件相当于一个通知，我们可以提前设定好事件发生时需要执行的内容，当事件发生时，就会执行我们预先设定好的JS代码。

事件有很多种类型，其中常用的有：

- onclick：点击事件
- oninput：内容输入事件
- onsubmit：内容提交事件

那么如何为事件添加一个动作呢？

<input type="password" oninput="console.info('正在输入文本')">

我们可以直接为一个元素添加对应事件的属性，比如oninput事件，我们可以直接在事件的值中编写js代码，但是注意，只能使用单引号，因为双引号用于囊括整个值。

我们也可以单独编写一个函数，当事件发生时直接调用我们的函数：

```
function f() {
    window.alert("你输入了一个字符")
}
```

<input type="password" oninput="oninput()">

仅仅了解了事件，还不足以实现高度自定义，我们接着来看DOM。

#### Document对象

当网页被加载时，浏览器会创建页面的文档对象模型（_D_ocument _O_bject _M_odel），它将整个页面的所有元素全部映射为JS对象，这样我们就可以在JS中操纵页面中的元素。

![](https://cdn.nlark.com/yuque/0/2024/gif/43159521/1711506833769-0631d6b7-b94f-4659-a6e0-6f4cf69210f4.gif)

比如我现在想要读取页面中某个输入框中的内容，那么我们就需要从DOM中获取此输入框元素的对象：

document.getElementById("pwd").value

通过document对象就能够快速获取当前页面中对应的元素，并且我们也可以快速获取元素中的一些属性。

比如现在我们可以结合事件，来进行密码长度的校验，密码长度小于6则不合法，不合法的密码，会让密码框边框变红，那么首先我们先来编写一个css样式：

```
.illegal-pwd{
    border: red 1px solid !important;
    box-shadow: 0 0 5px red;
}
```

接着我们来编写一下js代码，定义一个函数，此函数接受一个参数（元素本身的对象）检测输入的长度是否大于6，否则就将当前元素的class属性设定为css指定的class：

```
function checkIllegal(e) {
    if(e.value.length < 6) {
        e.setAttribute("class", "illegal-pwd")   
    }else {
        e.removeAttribute("class")
    }
}
```

最后我们将此函数绑定到oninput事件即可，注意传入了一个this，这里的this代表的是输入框元素本身：

<input id="pwd" oninput="checkIllegal(this)" type="password">

现在我们在输入的时候，会自动检查密码是否合法。

既然oninput本身也是一个属性，那么实际上我们可以动态进行修改：

document.getElementById("pwd").oninput = () => console.info("???")

那么，我们前面提及的window对象又是什么东西呢？

实际上Window对象范围更加广阔，它甚至直接代表了整个窗口，当然也包含我们的Document对象，我们一般通过Window对象来弹出提示框之类的东西。

#### 发送XHR请求

JS的大致内容我们已经全部学习完成了，那么如何使用JS与后端进行交互呢？

我们知道，如果我们需要提交表单，那么我们就需要将表单的信息全部发送给我们的服务器，那么，如何发送给服务器呢？

通过使用XMLHttpRequest对象，来向服务器发送一个HTTP请求，下面是一个最简单的请求格式：

```
let xhr = new XMLHttpRequest();
xhr.open('GET', 'https://www.baidu.com');
xhr.send();
```

上面的例子中，我们向服务器发起了一次网络请求，但是我们请求的是百度的服务器，并且此请求的方法为GET请求。

我们现在将其绑定到一个按钮上作为事件触发：

```
function http() {
    let xhr = new XMLHttpRequest();
    xhr.open('GET', 'https://www.baidu.com');
    xhr.send();    
}
```

<input id="button" type="button" onclick="http()">

我们可以在网络中查看我们发起的HTTP请求并且查看请求的响应结果，比如上面的请求，会返回百度这个页面的全部HTML代码。

实际上，我们的浏览器在我们输入网址后，也会向对应网站的服务器发起一次HTTP的GET请求。

在浏览器得到页面响应后，会加载当前页面，如果当前页面还引用了其他资源文件，那么会继续向服务器发起请求，直到页面中所有的资源文件全部加载完成后，才会停止。

## JavaWeb后端

### 计算机网络基础

**万维网**：万维网并非是某种特殊的计算机网络，万维网是一个大规模的联机式信息储藏所，英文简称web，万维网是用链接的方式，能够非常方便地从互联网上的一个站点访问另一个站点，从而主动地按需求获取丰富信息

**万维网的工作方式**：客户程序向服务器程序发出请求，服务器程序向客户程序送回客户所要的万维网文档

- 客户程序：浏览器
- 服务端：Web服务器

服务器可能不止一个页面，那么就需要用到URL统一资源定位符。网络上的资源都有一个唯一确定的URL。

<协议>://<主机>:<端口>/<路径>

- 协议是指采用什么协议来访问服务器，不同的协议决定了服务器返回信息的格式，我们一般使用HTTP协议
- 主机可以是一个域名，也可以是一个IP地址
- 端口是当前服务器Web应用程序开启的端口，HTTP协议默认80端口
- 路径就是我们希望去访问此服务器上的某个文件，不同路径代表着不同的资源

**HTTP协议**：HTTP是面向事务的应用层协议，它是万维网上能够可靠交换文件的重要基础。HTTP不仅传送完成超文本跳转所需的必须信息，而且也传送任何可从互联网上得到的信息，如文本、超文本、声音和图像。

**HTTP传输原理**：HTTP使用了面向连接的TCP作为运输层协议，保证了数据的可靠传输。HTTP不必考虑数据在传输过程中被丢弃又怎么样被重传。但是HTTP协议本身是无连接的。也就是说，HTTP虽然使用了TCP连接，但是通信双方在交换HTTP报文前不需要先建立HTTP连接。1997年以前，使用的是HTTP/1.0协议，之后就是HTTP/1.1协议

### Tomcat

Tomcat（汤姆猫）就是一个典型的Web应用服务器软件，通过运行Tomcat服务器，我们就可以快速部署我们的Web项目，并交由Tomcat进行管理，我们只需要直接通过浏览器访问我们的项目即可。

### Servlet

Java EE的一个标准，大部分的Web服务器都支持此标准，包括Tomcat，就像之前的JDBC一样，由官方定义了一系列接口，而具体实现由我们来编写，最后交给Web服务器（如Tomcat）来运行我们编写的Servlet。我们可以通过实现Servlet来进行动态网页响应，使用Servlet，不再是直接由Tomcat服务器发送我们编写好的静态网页内容（HTML文件），而是由我们通过Java代码进行动态拼接的结果，它能够很好地实现动态网页的返回。**Servlet并不是专用于HTTP协议通信，也可以用于其他的通信，但是一般都是用于HTTP。**

#### 创建Servlet

那么如何创建一个Servlet呢，非常简单，我们只需要实现Servlet类即可，并添加注解@WebServlet来进行注册。

```
@WebServlet("/test")
public class TestServlet implements Servlet {
		...实现接口方法
}
```

我们现在就可以去访问一下我们的页面：[http://localhost:8080/test/test](http://localhost:8080/test/test)

除了直接编写一个类，我们也可以在web.xml中进行注册，现将类上@WebServlet的注解去掉：

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
         version="5.0">
    <!--  名字需要写对  -->
    <servlet>
        <servlet-name>test</servlet-name>
        <servlet-class>com.example.webtest.TestServlet</servlet-class>
    </servlet>
    <!--  映射  -->
    <servlet-mapping>
        <servlet-name>test</servlet-name>
        <url-pattern>/test</url-pattern>
    </servlet-mapping>
</web-app>
```

实际上，Tomcat服务器会为我们提供一些默认的Servlet，也就是说在服务器启动后，即使我们什么都不编写，Tomcat也自带了几个默认的Servlet，他们编写在conf目录下的web.xml中：

```
<!-- The mapping for the default servlet -->
    <servlet-mapping>
        <servlet-name>default</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

    <!-- The mappings for the JSP servlet -->
    <servlet-mapping>
        <servlet-name>jsp</servlet-name>
        <url-pattern>*.jsp</url-pattern>
        <url-pattern>*.jspx</url-pattern>
    </servlet-mapping>
```

我们发现，默认的Servlet实际上可以帮助我们去访问一些静态资源，这也是为什么我们启动Tomcat服务器之后，能够直接访问webapp目录下的静态页面。

我们可以将之前编写的页面放入到webapp目录下，来测试一下是否能直接访问。

#### 探究Servlet的生命周期

首先我们需要了解，Servlet中的方法各自是在什么时候被调用的，我们先编写一个打印语句来看看：

```
public class TestServlet implements Servlet {

    public TestServlet(){
        System.out.println("我是构造方法！");
    }

    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        System.out.println("我是init");
    }

    @Override
    public ServletConfig getServletConfig() {
        System.out.println("我是getServletConfig");
        return null;
    }

    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("我是service");
    }

    @Override
    public String getServletInfo() {
        System.out.println("我是getServletInfo");
        return null;
    }

    @Override
    public void destroy() {
        System.out.println("我是destroy");
    }
}
```

我们可以多次尝试去访问此页面，但是init和构造方法只会执行一次，而每次访问都会执行的是service方法，因此，一个Servlet的生命周期为：

- 首先执行构造方法完成 Servlet 初始化
- Servlet 初始化后调用 **init ()** 方法。
- Servlet 调用 **service()** 方法来处理客户端的请求。
- Servlet 销毁前调用 **destroy()** 方法。
- 最后，Servlet 是由 JVM 的垃圾回收器进行垃圾回收的。

在Web应用程序运行时，每当浏览器向服务器发起一个请求时，都会创建一个线程执行一次service方法，来让我们**处理用户的请求**，并将结果响应给用户。我们发现service方法中，还有两个参数，ServletRequest和ServletResponse，实际上，用户发起的HTTP请求，就被Tomcat服务器封装为了一个ServletRequest对象，我们得到是其实是Tomcat服务器帮助我们创建的一个实现类，HTTP请求报文中的所有内容，都可以从ServletRequest对象中获取，同理，ServletResponse就是我们需要返回给浏览器的HTTP响应报文实体类封装。

那么我们来看看ServletRequest中有哪些内容，我们可以获取请求的一些信息：

```
@Override
public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
    //首先将其转换为HttpServletRequest（继承自ServletRequest，一般是此接口实现）
        HttpServletRequest request = (HttpServletRequest) servletRequest;
        
        System.out.println(request.getProtocol());  //获取协议版本
        System.out.println(request.getRemoteAddr());  //获取访问者的IP地址
  		  System.out.println(request.getMethod());   //获取请求方法
        //获取头部信息
        Enumeration<String> enumeration = request.getHeaderNames();
        while (enumeration.hasMoreElements()){
            String name = enumeration.nextElement();
            System.out.println(name + ": " + request.getHeader(name));
        }
}
```

我们发现，整个HTTP请求报文中的所有内容，都可以通过HttpServletRequest对象来获取，当然，它的作用肯定不仅仅是获取头部信息，我们还可以使用它来完成更多操作，后面会一一讲解。

那么我们再来看看ServletResponse，这个是服务端的响应内容，我们可以在这里填写我们想要发送给浏览器显示的内容：

```
//转换为HttpServletResponse（同上）
HttpServletResponse response = (HttpServletResponse) servletResponse;
//设定内容类型以及编码格式（普通HTML文本使用text/html，之后会讲解文件传输）
response.setHeader("Content-type", "text/html;charset=UTF-8");
//获取Writer直接写入内容
response.getWriter().write("我是响应内容！");
//所有内容写入完成之后，再发送给浏览器
```

现在我们在浏览器中打开此页面，就能够收到服务器发来的响应内容了。其中，响应头部分，是由Tomcat帮助我们生成的一个默认响应头。

![](https://cdn.nlark.com/yuque/0/2024/jpeg/43159521/1711506833791-fbd00681-1a70-49d2-a284-3f3058d197d3.jpeg)

因此，实际上整个流程就已经很清晰明了了。

#### 解读和使用HttpServlet

首先Servlet有一个直接实现抽象类GenericServlet。

这个类完善了配置文件读取和Servlet信息相关的的操作，但是依然没有去实现service方法，因此此类仅仅是用于完善一个Servlet的基本操作，那么我们接着来看HttpServlet，它是遵循HTTP协议的一种Servlet，继承自GenericServlet，它根据HTTP协议的规则，完善了service方法。

在阅读了HttpServlet源码之后，我们发现，其实我们只需要继承HttpServlet来编写我们的Servlet就可以了，并且它已经帮助我们提前实现了一些操作，这样就会给我们省去很多的时间。

```
@Log
@WebServlet("/test")
public class TestServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=UTF-8");
        resp.getWriter().write("<h1>恭喜你解锁了全新玩法</h1>");
    }
}
```

现在，我们只需要重写对应的请求方式，就可以快速完成Servlet的编写。

#### @WebServlet注解详解

首先name属性就是Servlet名称，而urlPatterns和value实际上是同样功能，就是代表当前Servlet的访问路径，它不仅仅可以是一个固定值，还可以进行通配符匹配：

@WebServlet("/test/*")

上面的路径表示，所有匹配/test/随便什么的路径名称，都可以访问此Servlet。

也可以进行某个扩展名称的匹配：

@WebServlet("*.js")

这样的话，获取任何以js结尾的文件，都会由我们自己定义的Servlet处理。

@WebServlet("/")

此路径和Tomcat默认为我们提供的Servlet冲突，会直接替换掉默认的，而使用我们的，此路径的意思为，如果没有找到匹配当前访问路径的Servlet，那么久会使用此Servlet进行处理。

我们还可以为一个Servlet配置多个访问路径：

@WebServlet({"/test1", "/test2"})

我们接着来看loadOnStartup属性，此属性决定了是否在Tomcat启动时就加载此Servlet，默认情况下，Servlet只有在被访问时才会加载，它的默认值为-1，表示不在启动时加载，我们可以将其修改为大于等于0的数，来开启启动时加载。并且数字的大小决定了此Servlet的启动优先级。

```
@Log
@WebServlet(value = "/test", loadOnStartup = 1)
public class TestServlet extends HttpServlet {

    @Override
    public void init() throws ServletException {
        super.init();
        log.info("我被初始化了！");
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=UTF-8");
        resp.getWriter().write("<h1>恭喜你解锁了全新玩法</h1>");
    }
}
```

#### 使用POST请求完成登陆

我们需要修改一下我们的Servlet，现在我们要让其能够接收一个POST请求：

```
@Log
@WebServlet("/login")
public class LoginServlet extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        req.getParameterMap().forEach((k, v) -> {
            System.out.println(k + ": " + Arrays.toString(v));
        });
    }
}
```

ParameterMap存储了我们发送的POST请求所携带的表单数据，我们可以直接将其遍历查看，浏览器发送了什么数据。

现在我们再来修改一下前端：

```
<body>
    <h1>登录到系统</h1>
    <form method="post" action="login">
        <hr>
        <div>
            <label>
                <input type="text" placeholder="用户名" name="username">
            </label>
        </div>
        <div>
            <label>
                <input type="password" placeholder="密码" name="password">
            </label>
        </div>
        <div>
            <button>登录</button>
        </div>
    </form>
</body>
```

通过修改form标签的属性，现在我们点击登录按钮，会自动向后台发送一个POST请求，请求地址为当前地址+/login（注意不同路径的写法），也就是我们上面编写的Servlet路径。

运行服务器，测试后发现，在点击按钮后，确实向服务器发起了一个POST请求，并且携带了表单中文本框的数据。

现在，我们根据已有的基础，将其与数据库打通，我们进行一个真正的用户登录操作，首先修改一下Servlet的逻辑：

```
@Override
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    //首先设置一下响应类型
    resp.setContentType("text/html;charset=UTF-8");
    //获取POST请求携带的表单数据
    Map<String, String[]> map = req.getParameterMap();
    //判断表单是否完整
    if(map.containsKey("username") && map.containsKey("password")) {
        String username = req.getParameter("username");
        String password = req.getParameter("password");

        //权限校验（待完善）
    }else {
        resp.getWriter().write("错误，您的表单数据不完整！");
    }
}
```

接下来我们再去编写Mybatis的依赖和配置文件，创建一个表，用于存放我们用户的账号和密码。

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${驱动类（含包名）}"/>
                <property name="url" value="${数据库连接URL}"/>
                <property name="username" value="${用户名}"/>
                <property name="password" value="${密码}"/>
            </dataSource>
        </environment>
    </environments>
</configuration>
```

```
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.7</version>
</dependency>
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.27</version>
</dependency>
```

配置完成后，在我们的Servlet的init方法中编写Mybatis初始化代码，因为它只需要初始化一次。

```
SqlSessionFactory factory;
@SneakyThrows
@Override
public void init() throws ServletException {
    factory = new SqlSessionFactoryBuilder().build(Resources.getResourceAsReader("mybatis-config.xml"));
}
```

现在我们创建一个实体类以及Mapper来进行用户信息查询：

```
@Data
public class User {
    String username;
    String password;
}
```

```
public interface UserMapper {

    @Select("select * from users where username = #{username} and password = #{password}")
    User getUser(@Param("username") String username, @Param("password") String password);
}
```

```
<mappers>
    <mapper class="com.example.dao.UserMapper"/>
</mappers>
```

好了，现在完事具备，只欠东风了，我们来完善一下登陆验证逻辑：

```
//登陆校验（待完善）
try (SqlSession sqlSession = factory.openSession(true)){
    UserMapper mapper = sqlSession.getMapper(UserMapper.class);
    User user = mapper.getUser(username, password);
    //判断用户是否登陆成功，若查询到信息则表示存在此用户
    if(user != null){
        resp.getWriter().write("登陆成功！");
    }else {
        resp.getWriter().write("登陆失败，请验证您的用户名或密码！");
    }
}
```

现在再去浏览器上进行测试吧！

注册界面其实是同理的，这里就不多做讲解了。

#### 上传和下载文件

首先我们来看看比较简单的下载文件，首先将我们的icon.png放入到resource文件夹中，接着我们编写一个Servlet用于处理文件下载：

```
@WebServlet("/file")
public class FileServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
      resp.setContentType("image/png");  
      OutputStream outputStream = resp.getOutputStream();
      InputStream inputStream = Resources.getResourceAsStream("icon.png");

    }
}
```

为了更加快速地编写IO代码，我们可以引入一个工具库：

```
<dependency>
    <groupId>commons-io</groupId>
    <artifactId>commons-io</artifactId>
    <version>2.6</version>
</dependency>
```

使用此类库可以快速完成IO操作：

```
resp.setContentType("image/png");
OutputStream outputStream = resp.getOutputStream();
InputStream inputStream = Resources.getResourceAsStream("icon.png");
//直接使用copy方法完成转换
IOUtils.copy(inputStream, outputStream);
```

现在我们在前端页面添加一个链接，用于下载此文件：

```
<hr>
<a href="file" download="icon.png">点我下载高清资源</a>
```

下载文件搞定，那么如何上传一个文件呢？

首先我们编写前端部分：

```
<form method="post" action="file" enctype="multipart/form-data">
    <div>
        <input type="file" name="test-file">
    </div>
    <div>
        <button>上传文件</button>
    </div>
</form>
```

注意必须添加enctype="multipart/form-data"，来表示此表单用于文件传输。

现在我们来修改一下Servlet代码：

```
@MultipartConfig
@WebServlet("/file")
public class FileServlet extends HttpServlet {

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        try(FileOutputStream stream = new FileOutputStream("/Users/nagocoler/Documents/IdeaProjects/WebTest/test.png")){
            Part part = req.getPart("test-file");
            IOUtils.copy(part.getInputStream(), stream);
            resp.setContentType("text/html;charset=UTF-8");
            resp.getWriter().write("文件上传成功！");
        }
    }
}
```

注意，必须添加@MultipartConfig注解来表示此Servlet用于处理文件上传请求。

现在我们再运行服务器，并将我们刚才下载的文件又上传给服务端。

#### 使用XHR请求数据

现在我们希望，网页中的部分内容，可以动态显示，比如网页上有一个时间，旁边有一个按钮，点击按钮就可以刷新当前时间。

这个时候就需要我们在网页展示时向后端发起请求了，并根据后端响应的结果，动态地更新页面中的内容，要实现此功能，就需要用到JavaScript来帮助我们，首先在js中编写我们的XHR请求，并在请求中完成动态更新：

```
function updateTime() {
    let xhr = new XMLHttpRequest();
    xhr.onreadystatechange = function() {
        if (xhr.readyState === 4 && xhr.status === 200) {
            document.getElementById("time").innerText = xhr.responseText
        }
    };
    xhr.open('GET', 'time', true);
    xhr.send();
}
```

接着修改一下前端页面，添加一个时间显示区域：

```
<hr>
<div id="time"></div>
<br>
<button onclick="updateTime()">更新数据</button>
<script>
    updateTime()
</script>
```

最后创建一个Servlet用于处理时间更新请求：

```
@WebServlet("/time")
public class TimeServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
        String date = dateFormat.format(new Date());
        resp.setContentType("text/html;charset=UTF-8");
        resp.getWriter().write(date);
    }
}
```

现在点击按钮就可以更新了。

#### 重定向与请求转发

当我们希望用户登录完成之后，直接跳转到网站的首页，那么这个时候，我们就可以使用重定向来完成。当浏览器收到一个重定向的响应时，会按照重定向响应给出的地址，再次向此地址发出请求。

实现重定向很简单，只需要调用一个方法即可，我们修改一下登陆成功后执行的代码：

resp.sendRedirect("time");

调用后，响应的状态码会被设置为302，并且响应头中添加了一个Location属性，此属性表示，需要重定向到哪一个网址。

如果我们成功登陆，服务器会发送给我们一个重定向响应，这时，我们的浏览器会去重新请求另一个网址。这样，我们在登陆成功之后，就可以直接帮助用户跳转到用户首页了。

那么我们接着来看请求转发，请求转发其实是一种服务器内部的跳转机制，我们知道，重定向会使得浏览器去重新请求一个页面，而请求转发则是服务器内部进行跳转，它的目的是，直接将本次请求转发给其他Servlet进行处理，并由其他Servlet来返回结果，因此它是在进行内部的转发。

req.getRequestDispatcher("/time").forward(req, resp);

现在，在登陆成功的时候，我们将请求转发给处理时间的Servlet，注意这里的路径规则和之前的不同，我们需要填写Servlet上指明的路径，并且请求转发只能转发到此应用程序内部的Servlet，不能转发给其他站点或是其他Web应用程序。

现在再次进行登陆操作，我们发现，返回结果为一个405页面，证明了，我们的请求现在是被另一个Servlet进行处理，并且请求的信息全部被转交给另一个Servlet，由于此Servlet不支持POST请求，因此返回405状态码。

那么也就是说，该请求包括请求参数也一起被传递了，那么我们可以尝试获取以下POST请求的参数。

现在我们给此Servlet添加POST请求处理，直接转交给Get请求处理：

```
@Override
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    this.doGet(req, resp);
}
```

再次访问，成功得到结果，但是我们发现，浏览器只发起了一次请求，并没有再次请求新的URL，也就是说，这一次请求直接返回了请求转发后的处理结果。

那么，请求转发有什么好处呢？它可以携带数据！

```
req.setAttribute("test", "我是请求转发前的数据");
req.getRequestDispatcher("/time").forward(req, resp);
```

System.out.println(req.getAttribute("test"));

通过setAttribute方法来给当前请求添加一个附加数据，在请求转发后，我们可以直接获取到该数据。

重定向属于2次请求，因此无法使用这种方式来传递数据，那么，如何在重定向之间传递数据呢？我们可以使用即将要介绍的ServletContext对象。

最后总结，两者的区别为：

- 请求转发是一次请求，重定向是两次请求
- 请求转发地址栏不会发生改变， 重定向地址栏会发生改变
- 请求转发可以共享请求参数 ，重定向之后，就获取不了共享参数了
- 请求转发只能转发给内部的Servlet

#### 了解ServletContext对象

ServletContext全局唯一，它是属于整个Web应用程序的，我们可以通过getServletContext()来获取到此对象。

此对象也能设置附加值：

```
ServletContext context = getServletContext();
context.setAttribute("test", "我是重定向之前的数据");
resp.sendRedirect("time");
```

System.out.println(getServletContext().getAttribute("test"));

因为无论在哪里，无论什么时间，获取到的ServletContext始终是同一个对象，因此我们可以随时随地获取我们添加的属性。

它不仅仅可以用来进行数据传递，还可以做一些其他的事情，比如请求转发：

context.getRequestDispatcher("/time").forward(req, resp);

它还可以获取根目录下的资源文件（注意是webapp根目录下的，不是resource中的资源）

#### 了解ServletContext对象

ServletContext全局唯一，它是属于整个Web应用程序的，我们可以通过getServletContext()来获取到此对象。

此对象也能设置附加值：

```
ServletContext context = getServletContext();
context.setAttribute("test", "我是重定向之前的数据");
resp.sendRedirect("time");
```

System.out.println(getServletContext().getAttribute("test"));

因为无论在哪里，无论什么时间，获取到的ServletContext始终是同一个对象，因此我们可以随时随地获取我们添加的属性。

它不仅仅可以用来进行数据传递，还可以做一些其他的事情，比如请求转发：

context.getRequestDispatcher("/time").forward(req, resp);

它还可以获取根目录下的资源文件（注意是webapp根目录下的，不是resource中的资源）

#### 初始化参数

初始化参数类似于初始化配置需要的一些值，比如我们的数据库连接相关信息，就可以通过初始化参数来给予Servlet，或是一些其他的配置项，也可以使用初始化参数来实现。

我们可以给一个Servlet添加一些初始化参数：

```
@WebServlet(value = "/login", initParams = {
        @WebInitParam(name = "test", value = "我是一个默认的初始化参数")
})
```

它也是以键值对形式保存的，我们可以直接通过Servlet的getInitParameter方法获取：

System.out.println(getInitParameter("test"));

但是，这里的初始化参数仅仅是针对于此Servlet，我们也可以定义全局初始化参数，只需要在web.xml编写即可：

```
<context-param>
    <param-name>lbwnb</param-name>
    <param-value>我是全局初始化参数</param-value>
</context-param>
```

我们需要使用ServletContext来读取全局初始化参数：

```
ServletContext context = getServletContext();
System.out.println(context.getInitParameter("lbwnb"));
```

有关ServletContext其他的内容，我们需要完成后面内容的学习，才能理解。

### Cookie

它可以在浏览器中保存一些信息，并且在下次请求时，请求头中会携带这些信息。

我们可以编写一个测试用例来看看：

```
Cookie cookie = new Cookie("test", "yyds");
resp.addCookie(cookie);
resp.sendRedirect("time");
```

```
for (Cookie cookie : req.getCookies()) {
    System.out.println(cookie.getName() + ": " + cookie.getValue());
}
```

我们可以观察一下，在HttpServletResponse中添加Cookie之后，浏览器的响应头中会包含一个Set-Cookie属性，同时，在重定向之后，我们的请求头中，会携带此Cookie作为一个属性，同时，我们可以直接通过HttpServletRequest来快速获取有哪些Cookie信息。

|   |   |
|---|---|
|**名字**|**属性**|
|name|Cookie的名称，Cookie一旦创建，名称便不可更改|
|value|Cookie的值，如果值为Unicode字符，需要为字符编码。如果为二进制数据，则需要使用BASE64编码|
|maxAge|Cookie失效的时间，单位秒。如果为正数，则该Cookie在maxAge秒后失效。如果为负数，该Cookie为临时Cookie，关闭浏览器即失效，浏览器也不会以任何形式保存该Cookie。如果为0，表示删除该Cookie。默认为-1|
|secure|该Cookie是否仅被使用安全协议传输。安全协议。安全协议有HTTPS，SSL等，在网络上传输数据之前先将数据加密。默认为false|
|path|Cookie的使用路径。如果设置为“/sessionWeb/”，则只有contextPath为“/sessionWeb”的程序可以访问该Cookie。如果设置为“/”，则本域名下contextPath都可以访问该Cookie。注意最后一个字符必须为“/”|
|domain|可以访问该Cookie的域名。如果设置为“.google.com”，则所有以“google.com”结尾的域名都可以访问该Cookie。注意第一个字符必须为“.”|
|comment|该Cookie的用处说明，浏览器显示Cookie信息的时候显示该说明|
|version|Cookie使用的版本号。0表示遵循Netscape的Cookie规范，1表示遵循W3C的RFC 2109规范|

**最关键的其实是****name****、****value****、****maxAge****、****domain****属性。**

那么我们来尝试修改一下maxAge来看看失效时间：

cookie.setMaxAge(20);

设定为20秒，我们可以直接看到，响应头为我们设定了20秒的过期时间。20秒内访问都会携带此Cookie，而超过20秒，Cookie消失。

既然了解了Cookie的作用，我们就可以通过使用Cookie来实现记住我功能，我们可以将用户名和密码全部保存在Cookie中，如果访问我们的首页时携带了这些Cookie，那么我们就可以直接为用户进行登陆，如果登陆成功则直接跳转到首页，如果登陆失败，则清理浏览器中的Cookie。

那么首先，我们先在前端页面的表单中添加一个勾选框：

```
<div>
    <label>
        <input type="checkbox" placeholder="记住我" name="remember-me">
        记住我
    </label>
</div>
```

接着，我们在登陆成功时进行判断，如果用户勾选了记住我，那么就讲Cookie存储到本地：

```
if(map.containsKey("remember-me")){   //若勾选了勾选框，那么会此表单信息
    Cookie cookie_username = new Cookie("username", username);
    cookie_username.setMaxAge(30);
    Cookie cookie_password = new Cookie("password", password);
    cookie_password.setMaxAge(30);
    resp.addCookie(cookie_username);
    resp.addCookie(cookie_password);
}
```

然后，我们修改一下默认的请求地址，现在一律通过http://localhost:8080/yyds/login进行登陆，那么我们需要添加GET请求的相关处理：

```
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    Cookie[] cookies = req.getCookies();
    if(cookies != null){
        String username = null;
        String password = null;
        for (Cookie cookie : cookies) {
            if(cookie.getName().equals("username")) username = cookie.getValue();
            if(cookie.getName().equals("password")) password = cookie.getValue();
        }
        if(username != null && password != null){
            //登陆校验
            try (SqlSession sqlSession = factory.openSession(true)){
                UserMapper mapper = sqlSession.getMapper(UserMapper.class);
                User user = mapper.getUser(username, password);
                if(user != null){
                    resp.sendRedirect("time");
                    return;   //直接返回
                }
            }
        }
    }
    req.getRequestDispatcher("/").forward(req, resp);   //正常情况还是转发给默认的Servlet帮我们返回静态页面
}
```

### Session

Session用来处理够辨别当前的请求是来自哪个用户发起的，每个用户的会话都会有一个自己的Session对象，来自同一个浏览器的所有请求，就属于同一个会话。Session是基于Cookie实现的，，服务端可以将Cookie保存到浏览器，当浏览器下次访问时，就会附带这些Cookie信息。Session也利用了这一点，它会给浏览器设定一个叫做JSESSIONID的Cookie，值是一个随机的排列组合，而此Cookie就对应了你属于哪一个对话，只要我们的浏览器携带此Cookie访问服务器，服务器就会通过Cookie的值进行辨别，得到对应的Session对象，因此，这样就可以追踪到底是哪一个浏览器在访问服务器。

那么现在，我们在用户登录成功之后，将用户对象添加到Session中，只要是此用户发起的请求，我们都可以从HttpSession中读取到存储在会话中的数据：

```
HttpSession session = req.getSession();
session.setAttribute("user", user);
```

同时，如果用户没有登录就去访问首页，那么我们将发送一个重定向请求，告诉用户，需要先进行登录才可以访问：

```
HttpSession session = req.getSession();
User user = (User) session.getAttribute("user");
if(user == null) {
    resp.sendRedirect("login");
    return;
}
```

Session并不是永远都存在的，它有着自己的过期时间，默认时间为30分钟，若超过此时间，Session将丢失，我们可以在配置文件中修改过期时间：

```
<session-config>
    <session-timeout>1</session-timeout>
</session-config>
```

我们也可以在代码中使用invalidate方法来使Session立即失效：

session.invalidate();

现在，通过Session，我们就可以更好地控制用户对于资源的访问，只有完成登陆的用户才有资格访问首页。

### Filter

**过滤器**相当于在所有访问前加了一堵墙，来自浏览器的所有访问请求都会首先经过过滤器，只有过滤器允许通过的请求，才可以顺利地到达对应的Servlet，而过滤器不允许的通过的请求，我们可以自由地进行控制是否进行重定向或是请求转发。

添加一个过滤器非常简单，只需要实现Filter接口，并添加@WebFilter注解即可：

```
@WebFilter("/*")   //路径的匹配规则和Servlet一致，这里表示匹配所有请求
public class TestFilter implements Filter {
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        
    }
}
```

这样我们就成功地添加了一个过滤器，那么添加一句打印语句看看，是否所有的请求都会经过此过滤器：

```
HttpServletRequest request = (HttpServletRequest) servletRequest;
System.out.println(request.getRequestURL());
```

如何让请求可以顺利地到达对应的Servlet，也就是说怎么让这个请求顺利通过呢？我们只需要在最后添加一句：

filterChain.doFilter(servletRequest, servletResponse);

由于我们整个应用程序可能存在多个过滤器，那么这行代码的意思实际上是将此请求继续传递给下一个过滤器，当没有下一个过滤器时，才会到达对应的Servlet进行处理，我们可以再来创建一个过滤器看看效果：

```
@WebFilter("/*")
public class TestFilter2 implements Filter {
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        System.out.println("我是2号过滤器");
        filterChain.doFilter(servletRequest, servletResponse);
    }
}
```

由于过滤器的过滤顺序是按照类名的自然排序进行的，因此我们将第一个过滤器命名进行调整。

我们发现，在经过第一个过滤器之后，会继续前往第二个过滤器，只有两个过滤器全部经过之后，才会到达我们的Servlet中。

实际上，当doFilter方法调用时，就会一直向下直到Servlet，在Servlet处理完成之后，又依次返回到最前面的Filter，类似于递归的结构，我们添加几个输出语句来判断一下：

```
@Override
public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
    System.out.println("我是2号过滤器");
    filterChain.doFilter(servletRequest, servletResponse);
    System.out.println("我是2号过滤器，处理后");
}
```

```
@Override
public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
    System.out.println("我是1号过滤器");
    filterChain.doFilter(servletRequest, servletResponse);
    System.out.println("我是1号过滤器，处理后");
}
```

同Servlet一样，Filter也有对应的HttpFilter专用类，它针对HTTP请求进行了专门处理，因此我们可以直接使用HttpFilter来编写：

```
public abstract class HttpFilter extends GenericFilter {
    private static final long serialVersionUID = 7478463438252262094L;

    public HttpFilter() {
    }

    public void doFilter(ServletRequest req, ServletResponse res, FilterChain chain) throws IOException, ServletException {
        if (req instanceof HttpServletRequest && res instanceof HttpServletResponse) {
            this.doFilter((HttpServletRequest)req, (HttpServletResponse)res, chain);
        } else {
            throw new ServletException("non-HTTP request or response");
        }
    }

    protected void doFilter(HttpServletRequest req, HttpServletResponse res, FilterChain chain) throws IOException, ServletException {
        chain.doFilter(req, res);
    }
}
```

那么现在，我们就可以给我们的应用程序添加一个过滤器，用户在未登录情况下，只允许静态资源和登陆页面请求通过，登陆之后畅行无阻：

```
@WebFilter("/*")
public class MainFilter extends HttpFilter {
    @Override
    protected void doFilter(HttpServletRequest req, HttpServletResponse res, FilterChain chain) throws IOException, ServletException {
        String url = req.getRequestURL().toString();
        //判断是否为静态资源
        if(!url.endsWith(".js") && !url.endsWith(".css") && !url.endsWith(".png")){
            HttpSession session = req.getSession();
            User user = (User) session.getAttribute("user");
            //判断是否未登陆
            if(user == null && !url.endsWith("login")){
                res.sendRedirect("login");
                return;
            }
        }
        //交给过滤链处理
        chain.doFilter(req, res);
    }
}
```

### Listener

监听器并不是我们学习的重点内容，那么什么是监听器呢？

如果我们希望，在应用程序加载的时候，或是Session创建的时候，亦或是在Request对象创建的时候进行一些操作，那么这个时候，我们就可以使用监听器来实现。

默认为我们提供了很多类型的监听器，我们这里就演示一下监听Session的创建即可：

```
@WebListener
public class TestListener implements HttpSessionListener {
    @Override
    public void sessionCreated(HttpSessionEvent se) {
        System.out.println("有一个Session被创建了");
    }
}
```

### 了解JSP页面与加载规则

JSP并不是需要重点学习的内容，因为它已经过时了，使用JSP会导致前后端严重耦合。

JSP其实就是一种模板引擎，那么何谓模板引擎呢？顾名思义，它就是一个模板，而模板需要我们填入数据，才可以变成一个页面，也就是说，我们可以直接在前端页面中直接填写数据，填写后生成一个最终的HTML页面返回给前端。

首先我们来创建一个新的项目，项目创建成功后，删除Java目录下的内容，只留下默认创建的jsp文件，我们发现，在webapp目录中，存在一个index.jsp文件，现在我们直接运行项目，会直接访问这个JSP页面。

```
<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<!DOCTYPE html>
<html>
<head>
    <title>JSP - Hello World</title>
</head>
<body>
<h1><%= "Hello World!" %>
</h1>
<br/>
<a href="hello-servlet">Hello Servlet</a>
</body>
</html>
```

但是我们并没有编写对应的Servlet来解析啊，那么为什么这个JSP页面会被加载呢？

实际上，我们一开始提到的两个Tomcat默认的Servlet中，一个是用于请求静态资源，还有一个就是用于处理jsp的：

```
<!-- The mappings for the JSP servlet -->
    <servlet-mapping>
        <servlet-name>jsp</servlet-name>
        <url-pattern>*.jsp</url-pattern>
        <url-pattern>*.jspx</url-pattern>
    </servlet-mapping>
```

那么，JSP和普通HTML页面有什么区别呢，我们发现它的语法和普通HTML页面几乎一致，我们可以直接在JSP中编写Java代码，并在页面加载的时候执行，我们随便找个地方插入：

```
<%
    System.out.println("JSP页面被加载");
%>
```

我们发现，请求一次页面，页面就会加载一次，并执行我们填写的Java代码。也就是说，我们可以直接在此页面中执行Java代码来填充我们的数据，这样我们的页面就变成了一个动态页面，使用<%= %>来填写一个值：

<h1><%= new Date() %></h1>

现在访问我们的网站，每次都会创建一个新的Date对象，因此每次访问获取的时间都不一样，我们的网站已经算是一个动态的网站的了。

虽然这样在一定程度上上为我们提供了便利，但是这样的写法相当于整个页面既要编写前端代码，也要编写后端代码，随着项目的扩大，整个页面会显得难以阅读，并且现在都是前后端开发人员职责非常明确的，如果要编写JSP页面，那就必须要招一个既会前端也会后端的程序员，这样显然会导致不必要的开销。

那么我们来研究一下，为什么JSP页面能够在加载的时候执行Java代码呢？

首先我们将此项目打包，并在Tomcat服务端中运行，生成了一个文件夹并且可以正常访问。

我们现在看到work目录，我们发现这个里面多了一个index_jsp.java和index_jsp.class，那么这些东西是干嘛的呢，我们来反编译一下就啥都知道了：

```
public final class index_jsp extends org.apache.jasper.runtime.HttpJspBase  //继承自HttpServlet
    implements org.apache.jasper.runtime.JspSourceDependent,
                 org.apache.jasper.runtime.JspSourceImports {

 ...

  public void _jspService(final jakarta.servlet.http.HttpServletRequest request, final jakarta.servlet.http.HttpServletResponse response)
      throws java.io.IOException, jakarta.servlet.ServletException {

    if (!jakarta.servlet.DispatcherType.ERROR.equals(request.getDispatcherType())) {
      final java.lang.String _jspx_method = request.getMethod();
      if ("OPTIONS".equals(_jspx_method)) {
        response.setHeader("Allow","GET, HEAD, POST, OPTIONS");
        return;
      }
      if (!"GET".equals(_jspx_method) && !"POST".equals(_jspx_method) && !"HEAD".equals(_jspx_method)) {
        response.setHeader("Allow","GET, HEAD, POST, OPTIONS");
        response.sendError(HttpServletResponse.SC_METHOD_NOT_ALLOWED, "JSP 只允许 GET、POST 或 HEAD。Jasper 还允许 OPTIONS");
        return;
      }
    }

    final jakarta.servlet.jsp.PageContext pageContext;
    jakarta.servlet.http.HttpSession session = null;
    final jakarta.servlet.ServletContext application;
    final jakarta.servlet.ServletConfig config;
    jakarta.servlet.jsp.JspWriter out = null;
    final java.lang.Object page = this;
    jakarta.servlet.jsp.JspWriter _jspx_out = null;
    jakarta.servlet.jsp.PageContext _jspx_page_context = null;


    try {
      response.setContentType("text/html; charset=UTF-8");
      pageContext = _jspxFactory.getPageContext(this, request, response,
             null, true, 8192, true);
      _jspx_page_context = pageContext;
      application = pageContext.getServletContext();
      config = pageContext.getServletConfig();
      session = pageContext.getSession();
      out = pageContext.getOut();
      _jspx_out = out;

      out.write("\n");
      out.write("\n");
      out.write("<!DOCTYPE html>\n");
      out.write("<html>\n");
      out.write("<head>\n");
      out.write("    <title>JSP - Hello World</title>\n");
      out.write("</head>\n");
      out.write("<body>\n");
      out.write("<h1>");
      out.print( new Date() );
      out.write("</h1>\n");

    System.out.println("JSP页面被加载");

      out.write("\n");
      out.write("<br/>\n");
      out.write("<a href=\"hello-servlet\">Hello Servlet</a>\n");
      out.write("</body>\n");
      out.write("</html>");
    } catch (java.lang.Throwable t) {
      if (!(t instanceof jakarta.servlet.jsp.SkipPageException)){
        out = _jspx_out;
        if (out != null && out.getBufferSize() != 0)
          try {
            if (response.isCommitted()) {
              out.flush();
            } else {
              out.clearBuffer();
            }
          } catch (java.io.IOException e) {}
        if (_jspx_page_context != null) _jspx_page_context.handlePageException(t);
        else throw new ServletException(t);
      }
    } finally {
      _jspxFactory.releasePageContext(_jspx_page_context);
    }
  }
}
```

我们发现，它是继承自HttpJspBase类，我们可以反编译一下jasper.jar（它在tomcat的lib目录中）来看看:

```
package org.apache.jasper.runtime;

import jakarta.servlet.ServletConfig;
import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import jakarta.servlet.jsp.HttpJspPage;
import java.io.IOException;
import org.apache.jasper.compiler.Localizer;

public abstract class HttpJspBase extends HttpServlet implements HttpJspPage {
    private static final long serialVersionUID = 1L;

    protected HttpJspBase() {
    }

    public final void init(ServletConfig config) throws ServletException {
        super.init(config);
        this.jspInit();
        this._jspInit();
    }

    public String getServletInfo() {
        return Localizer.getMessage("jsp.engine.info", new Object[]{"3.0"});
    }

    public final void destroy() {
        this.jspDestroy();
        this._jspDestroy();
    }

    public final void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this._jspService(request, response);
    }

    public void jspInit() {
    }

    public void _jspInit() {
    }

    public void jspDestroy() {
    }

    protected void _jspDestroy() {
    }

    public abstract void _jspService(HttpServletRequest var1, HttpServletResponse var2) throws ServletException, IOException;
}
```

实际上，Tomcat在加载JSP页面时，会将其动态转换为一个java类并编译为class进行加载，而生成的Java类，正是一个Servlet的子类，而页面的内容全部被编译为输出字符串，这便是JSP的加载原理，因此，JSP本质上依然是一个Servlet！

![](https://cdn.nlark.com/yuque/0/2024/gif/43159521/1711506833816-d02393fc-901b-4337-9200-38aca9ef515f.gif)

### 使用Thymeleaf模板引擎

虽然JSP为我们带来了便捷，但是其缺点也是显而易见的，那么有没有一种既能实现模板，又能兼顾前后端分离的模板引擎呢？

**Thymeleaf**（百里香叶）是一个适用于Web和独立环境的现代化服务器端Java模板引擎，官方文档：[https://www.thymeleaf.org/documentation.html](https://www.thymeleaf.org/documentation.html)。

那么它和JSP相比，好在哪里呢，我们来看官网给出的例子：

```
<table>
  <thead>
    <tr>
      <th th:text="#{msgs.headers.name}">Name</th>
      <th th:text="#{msgs.headers.price}">Price</th>
    </tr>
  </thead>
  <tbody>
    <tr th:each="prod: ${allProducts}">
      <td th:text="${prod.name}">Oranges</td>
      <td th:text="${#numbers.formatDecimal(prod.price, 1, 2)}">0.99</td>
    </tr>
  </tbody>
</table>
```

我们可以在前端页面中填写占位符，而这些占位符的实际值则由后端进行提供，这样，我们就不用再像JSP那样前后端都写在一起了。

那么我们来创建一个例子感受一下，首先还是新建一个项目，注意，在创建时，勾选Thymeleaf依赖。

首先编写一个前端页面，名称为test.html，注意，是放在resource目录下，在html标签内部添加xmlns:th="http://www.thymeleaf.org"引入Thymeleaf定义的标签属性：

```
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div th:text="${title}"></div>
</body>
</html>
```

接着我们编写一个Servlet作为默认页面：

```
@WebServlet("/index")
public class HelloServlet extends HttpServlet {

    TemplateEngine engine;
    @Override
    public void init() throws ServletException {
        engine = new TemplateEngine();
        ClassLoaderTemplateResolver r = new ClassLoaderTemplateResolver();
        engine.setTemplateResolver(r);
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        Context context = new Context();
        context.setVariable("title", "我是标题");
        engine.process("test.html", context, resp.getWriter());
    }
}
```

我们发现，浏览器得到的页面，就是已经经过模板引擎解析好的页面，而我们的代码依然是后端处理数据，前端展示数据，因此使用Thymeleaf就能够使得当前Web应用程序的前后端划分更加清晰。

虽然Thymeleaf在一定程度上分离了前后端，但是其依然是在后台渲染HTML页面并发送给前端，并不是真正意义上的前后端分离。

#### Thymeleaf语法基础

那么，如何使用Thymeleaf呢？

首先我们看看后端部分，我们需要通过TemplateEngine对象来将模板文件渲染为最终的HTML页面：

```
TemplateEngine engine;
@Override
public void init() throws ServletException {
    engine = new TemplateEngine();
  	//设定模板解析器决定了从哪里获取模板文件，这里直接使用ClassLoaderTemplateResolver表示加载内部资源文件
    ClassLoaderTemplateResolver r = new ClassLoaderTemplateResolver();
    engine.setTemplateResolver(r);
}
```

由于此对象只需要创建一次，之后就可以一直使用了。接着我们来看如何使用模板引擎进行解析：

```
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    //创建上下文，上下文中包含了所有需要替换到模板中的内容
    Context context = new Context();
    context.setVariable("title", "<h1>我是标题</h1>");
    //通过此方法就可以直接解析模板并返回响应
    engine.process("test.html", context, resp.getWriter());
}
```

操作非常简单，只需要简单几步配置就可以实现模板的解析。接下来我们就可以在前端页面中通过上下文提供的内容，来将Java代码中的数据解析到前端页面。

接着我们来了解Thymeleaf如何为普通的标签添加内容，比如我们示例中编写的：

<div th:text="${title}"></div>

我们使用了th:text来为当前标签指定内部文本，注意任何内容都会变成普通文本，即使传入了一个HTML代码，如果我希望向内部添加一个HTML文本呢？我们可以使用th:utext属性：

<div th:utext="${title}"></div>

并且，传入的title属性，不仅仅只是一个字符串的值，而是一个字符串的引用，我们可以直接通过此引用调用相关的方法：

<div th:text="${title.toLowerCase()}"></div>

这样看来，Thymeleaf既能保持JSP为我们带来的便捷，也能兼顾前后端代码的界限划分。

除了替换文本，它还支持替换一个元素的任意属性，我们发现，th:能够拼接几乎所有的属性，一旦使用th:属性名称，那么属性的值就可以通过后端提供了，比如我们现在想替换一个图片的链接：

```
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    Context context = new Context();
    context.setVariable("url", "http://n.sinaimg.cn/sinakd20121/600/w1920h1080/20210727/a700-adf8480ff24057e04527bdfea789e788.jpg");
  	context.setVariable("alt", "图片就是加载不出来啊");
    engine.process("test.html", context, resp.getWriter());
}
```

```
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <img width="700" th:src="${url}" th:alt="${alt}">
</body>
</html>
```

现在访问我们的页面，就可以看到替换后的结果了。

Thymeleaf还可以进行一些算术运算，几乎Java中的运算它都可以支持：

<div th:text="${value % 2}"></div>

同样的，它还支持三元运算：

<div th:text="${value % 2 == 0 ? 'yyds' : 'lbwnb'}"></div>

多个属性也可以通过+进行拼接，就像Java中的字符串拼接一样，这里要注意一下，字符串不能直接写，要添加单引号：

<div th:text="${name}+' 我是文本 '+${value}"></div>

#### Thymeleaf流程控制语法

除了一些基本的操作，我们还可以使用Thymeleaf来处理流程控制语句，当然，不是直接编写Java代码的形式，而是添加一个属性即可。

首先我们来看if判断语句，如果if条件满足，则此标签留下，若if条件不满足，则此标签自动被移除：

```
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    Context context = new Context();
    context.setVariable("eval", true);
    engine.process("test.html", context, resp.getWriter());
}
```

<div th:if="${eval}">我是判断条件标签</div>

th:if会根据其中传入的值或是条件表达式的结果进行判断，只有满足的情况下，才会显示此标签，具体的判断规则如下：

- 如果值不是空的：

- 如果值是布尔值并且为true。
- 如果值是一个数字，并且是非零
- 如果值是一个字符，并且是非零
- 如果值是一个字符串，而不是“错误”、“关闭”或“否”
- 如果值不是布尔值、数字、字符或字符串。

- 如果值为空，th:if将计算为false

th:if还有一个相反的属性th:unless，效果完全相反，这里就不演示了。

我们接着来看多分支条件判断，我们可以使用th:switch属性来实现：

```
<div th:switch="${eval}">
    <div th:case="1">我是1</div>
    <div th:case="2">我是2</div>
    <div th:case="3">我是3</div>
</div>
```

只不过没有default属性，但是我们可以使用th:case="*"来代替：

<div th:case="*">我是Default</div>

最后我们再来看看，它如何实现遍历，假如我们有一个存放书籍信息的List需要显示，那么如何快速生成一个列表呢？我们可以使用th:each来进行遍历操作：

```
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    Context context = new Context();
    context.setVariable("list", Arrays.asList("伞兵一号的故事", "倒一杯卡布奇诺", "玩游戏要啸着玩", "十七张牌前的电脑屏幕"));
    engine.process("test.html", context, resp.getWriter());
}
```

```
<ul>
    <li th:each="title : ${list}" th:text="'《'+${title}+'》'"></li>
</ul>
```

th:each中需要填写 "单个元素名称 : ${列表}"，这样，所有的列表项都可以使用遍历的单个元素，只要使用了th:each，都会被循环添加。因此最后生成的结果为：

```
<ul>
        <li>《伞兵一号的故事》</li>
        <li>《倒一杯卡布奇诺》</li>
        <li>《玩游戏要啸着玩》</li>
        <li>《十七张牌前的电脑屏幕》</li>
    </ul>
```

我们还可以获取当前循环的迭代状态，只需要在最后添加iterStat即可，从中可以获取很多信息，比如当前的顺序：

```
<ul>
    <li th:each="title, iterStat : ${list}" th:text="${iterStat.index}+'.《'+${title}+'》'"></li>
</ul>
```

状态变量在th:each属性中定义，并包含以下数据：

- 当前_迭代索引_，以0开头。这是index属性。
- 当前_迭代索引_，以1开头。这是count属性。
- 迭代变量中的元素总量。这是size属性。
- 每个迭代的_迭代变量_。这是current属性。
- 当前迭代是偶数还是奇数。这些是even/odd布尔属性。
- 当前迭代是否是第一个迭代。这是first布尔属性。
- 当前迭代是否是最后一个迭代。这是last布尔属性。

通过了解了流程控制语法，现在我们就可以很轻松地使用Thymeleaf来快速替换页面中的内容了。

#### Thymeleaf模板布局

在某些网页中，我们会发现，整个网站的页面，除了中间部分的内容会随着我们的页面跳转而变化外，有些部分是一直保持一个状态的，比如打开小破站，我们翻动评论或是切换视频分P的时候，变化的仅仅是对应区域的内容，实际上，其他地方的内容会无论内部页面如何跳转，都不会改变。

Thymeleaf就可以轻松实现这样的操作，我们只需要将不会改变的地方设定为模板布局，并在不同的页面中插入这些模板布局，就无需每个页面都去编写同样的内容了。现在我们来创建两个页面：

```
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div class="head">
        <div>
            <h1>我是标题内容，每个页面都有</h1>
        </div>
        <hr>
    </div>
    <div class="body">
        <ul>
            <li th:each="title, iterStat : ${list}" th:text="${iterStat.index}+'.《'+${title}+'》'"></li>
        </ul>
    </div>
</body>
</html>
```

```
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div class="head">
        <div>
            <h1>我是标题内容，每个页面都有</h1>
        </div>
        <hr>
    </div>
    <div class="body">
        <div>这个页面的样子是这样的</div>
    </div>
</body>
</html>
```

接着将模板引擎写成工具类的形式：

```
public class ThymeleafUtil {

    private static final TemplateEngine engine;
    static  {
        engine = new TemplateEngine();
        ClassLoaderTemplateResolver r = new ClassLoaderTemplateResolver();
        engine.setTemplateResolver(r);
    }

    public static TemplateEngine getEngine() {
        return engine;
    }
}
```

```
@WebServlet("/index2")
public class HelloServlet2 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        Context context = new Context();
        ThymeleafUtil.getEngine().process("test2.html", context, resp.getWriter());
    }
}
```

现在就有两个Servlet分别对应两个页面了，但是这两个页面实际上是存在重复内容的，我们要做的就是将这些重复内容提取出来。

我们单独编写一个head.html来存放重复部分：

```
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org" lang="en">
<body>
    <div class="head" th:fragment="head-title">
        <div>
            <h1>我是标题内容，每个页面都有</h1>
        </div>
        <hr>
    </div>
</body>
</html>
```

现在，我们就可以直接将页面中的内容快速替换：

```
<div th:include="head.html::head-title"></div>
<div class="body">
    <ul>
        <li th:each="title, iterStat : ${list}" th:text="${iterStat.index}+'.《'+${title}+'》'"></li>
    </ul>
</div>
```

我们可以使用th:insert和th:replace和th:include这三种方法来进行页面内容替换，那么th:insert和th:replace（和th:include，自3.0年以来不推荐）有什么区别？

- th:insert最简单：它只会插入指定的片段作为标签的主体。
- th:replace实际上将标签直接_替换_为指定的片段。
- th:include和th:insert相似，但它没有插入片段，而是只插入此片段_的内容_。

你以为这样就完了吗？它还支持参数传递，比如我们现在希望插入二级标题，并且由我们的子页面决定：

```
<div class="head" th:fragment="head-title">
    <div>
        <h1>我是标题内容，每个页面都有</h1>
        <h2>我是二级标题</h2>
    </div>
    <hr>
</div>
```

稍加修改，就像JS那样添加一个参数名称：

```
<div class="head" th:fragment="head-title(sub)">
    <div>
        <h1>我是标题内容，每个页面都有</h1>
        <h2 th:text="${sub}"></h2>
    </div>
    <hr>
</div>
```

现在直接在替换位置添加一个参数即可：

```
<div th:include="head.html::head-title('这个是第1个页面的二级标题')"></div>
<div class="body">
    <ul>
        <li th:each="title, iterStat : ${list}" th:text="${iterStat.index}+'.《'+${title}+'》'"></li>
    </ul>
</div>
```

### 探讨Tomcat类加载机制

有关JavaWeb的内容，我们就聊到这里，在最后，我们还是来看一下Tomcat到底是如何加载和运行我们的Web应用程序的。

Tomcat服务器既然要同时运行多个Web应用程序，那么就必须要实现不同应用程序之间的隔离，也就是说，Tomcat需要分别去加载不同应用程序的类以及依赖，还必须保证应用程序之间的类无法相互访问，而传统的类加载机制无法做到这一点，同时每个应用程序都有自己的依赖，如果两个应用程序使用了同一个版本的同一个依赖，那么还有必要去重新加载吗，带着诸多问题，Tomcat服务器编写了一套自己的类加载机制。

![](https://cdn.nlark.com/yuque/0/2024/png/43159521/1711506834260-ff2e3b26-af59-492a-b69d-dc093d53e7ce.png)

首先我们要知道，Tomcat本身也是一个Java程序，它要做的是去动态加载我们编写的Web应用程序中的类，而要解决以上提到的一些问题，就出现了几个新的类加载器，我们来看看各个加载器的不同之处：

- Common ClassLoader：Tomcat最基本的类加载器，加载路径中的class可以被Tomcat容器本身以及各个Web应用程序访问。
- Catalina ClassLoader：Tomcat容器私有的类加载器，加载路径中的class对于Web应用程序不可见。
- Shared ClassLoader：各个Web应用程序共享的类加载器，加载路径中的class对于所有Web应用程序可见，但是对于Tomcat容器不可见。
- Webapp ClassLoader：各个Web应用程序私有的类加载器，加载路径中的class只对当前Web应用程序可见，每个Web应用程序都有一个自己的类加载器，此加载器可能存在多个实例。
- JasperLoader：JSP类加载器，每个JSP文件都有一个自己的类加载器，也就是说，此加载器可能会存在多个实例。

通过这样进行划分，就很好地解决了我们上面所提到的问题，但是我们发现，这样的类加载机制，破坏了JDK的双亲委派机制（在JavaSE阶段讲解过），比如Webapp ClassLoader，它只加载自己的class文件，它没有将类交给父类加载器进行加载，也就是说，我们可以随意创建和JDK同包同名的类，岂不是就出问题了？

难道Tomcat的开发团队没有考虑到这个问题吗？

![](https://cdn.nlark.com/yuque/0/2024/jpeg/43159521/1711506834384-d9639518-bce0-4478-844e-bc6df99c5d67.jpeg)

实际上，WebAppClassLoader的加载机制是这样的：WebAppClassLoader 加载类的时候，绕开了 AppClassLoader，直接先使用 ExtClassLoader 来加载类。这样的话，如果定义了同包同名的类，就不会被加载，而如果是自己定义 的类，由于该类并不是JDK内部或是扩展类，所有不会被加载，而是再次回到WebAppClassLoader进行加载，如果还失败，再使用AppClassloader进行加载。