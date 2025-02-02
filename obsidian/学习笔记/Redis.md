# 概念

## 认识redis

Redis：键值数据库

SQL：关系型数据库

NoSQL：非关系型数据库

特征：

- 键值型，value支持多种不同数据结构，功能丰富
- 单线程，每个命令具备原子性
- 低延迟，速度快（基于内存、IO多路复用、良好的编码）
- 支持数据持久化
- 支持主从集群、分片集群
- 支持多语言客户端

# 基本操作

## 数据操作

在Redis下，数据库是由一个整数索引表示，而不是一个数据库名称，默认是16个

选择数据库

```
select 序号;
```

向redis中添加数据

```
set <key> <value>
-- 一次性多个
mset [<key> <value>]...
```

所有存入的数据默认会以字符串的形式保存，键值具有一定的命名规范，以方便我们可以快速我们的数据属于哪一个部分，比如用户的数据：

```
-- 使用冒号来进行板块的分割，比如下面表示用户xxx的信息中的name属性，值为lbw
set user:info:用户ID:name lbw
```

读取存入的值

```
get <key>
```

过期事件设定

```
set <key> <value> EX 秒
set <key> <value> PX 毫秒
```

当数据到达指定时间时，会被自动删除，我们也可以单独为其他的键值对设置过期的时间：

```
expire <key> 秒
```

查询某个键值对还有多久过期

```
ttl <key>
-- 毫秒显示
pttl <key>
-- 转换为永久
persist <key>
```

想要直接删除这个数据：

```
del <key>...
```

删除命令可以同时拼接多个键值一起删除

想要查看库中所有的键值时：

```
keys *
```

也可以查询某个键值是否存在

```
exists <key>
```

随机拿一个值

```
randomkey
```

将一个数据库中的内容移到另一个数据库中

```
move <key> <新的名称>
-- 下面这个会检查新的名称是否存在
renamenx <key> <新的名称>
```

如果存放的数据是一个数字，我们还可以对其进行自增自减的操作：

```
-- 等价于a = a + 1
incr <key>

-- 等价于a = a + b
incr <key> b

-- 等价于a = a - 1
decr <key>
```

最后就是查看值的数据类型

```
type <key>
```

# 数据类型

## Hash

类型的本质是HashMap,也就是嵌套了一个HashMap

它比较适合存储类这样的数据，由于值本身又是一个Map,因此我们可以在此Map中放入类的各种属性和值，以实现一个Hash数据类型存储一个类的数据

```
hset <key> [<字段> <值>]
```

我们可以直接获取

```
hget <key> <字段>
-- 如果想一次性获取所有的字段
hgetall <key>
```

判断某个字段是否存在

```
hexists <key> <字段>
```

删除Hash中的某个字段

```
hdel <字段>
```

想知道hash中一共有多少个键值对

```
hlen <key>
```

一次性获取所有字段的值

```
hvals <key>
```

## List

可以向一个已存在或不存在的List中添加数据，如果不存在、会自动创建

```
-- 向列表头部添加元素
lpush <key> <element>
-- 向列表尾部添加元素
rpush <key> <element>
-- 在指定元素前面/后面插入元素
linsert <key> before/after <指定元素> <element>
```

获取元素

```
-- 根据下标获取元素
lindex <key> <下标>
-- 获取并移除头部元素
rpop <key>
-- 获取并移除尾部元素
rpop <key>
-- 获取指定范围内
lrange <key> start stop
```

从前一个数组的最后去一个数出来放到另一个数组的头部，并返回元素

```
rpoplpush 当前数组 目标数组
```

阻塞操作，等待列表中有了数据后再进行pop操作

```
-- 如果列表中没有元素，那就等待，如果指定时间(秒)内被添加了数据，那么执行pop操作，如果超时就作废，支持同时等待多个列表，只要其中一个列表有元素了，那么他就执行
blpop <key>... timeout
```

## Set和SortedSet

向Set中添加一个或多个值：

```
sadd <key> <value>
```

查看Set集合中有多少个值:

```
scard <key>
```

判断你集合中是否包含:

```
-- 是否包含指定值
sismember <key> <value>
-- 列出所有值
smembers <key>
```

集合之间的运算:

```
-- 集合之间的差集
sdiff <key1> <key2>
-- 集合之间的交集
sinetr <key1> <key2>
-- 求并集
sunion <key> <key2>
-- 将集合之间的差集存到目标集合中
sdiffstore 目标 <key1> <key2>
-- 同上
sinterstore 目标 <key1> <key2>
-- 同上
sunionstore 目标 <key1> <key2>
```

移动指定值到另一个集合中

```
smove <key> 目标 value
```

移除操作：

```
-- 随机移除一个幸运儿
spop <key>
-- 移除指定
srem <key> <value>
```

# 持久化

redis中的数据是存在内存中的，高效但是数据没保存 -> 进行持久化操作保存数据

- 保存当前已经存储的数据
- 保存存放数据的所有过程

## RDB

保存当前已经存储的数据

```
save 
-- 注意上面这个命令是直接保存，会占用一定的时间，也可以单独开一个子进程后台执行保存
bgsave
```