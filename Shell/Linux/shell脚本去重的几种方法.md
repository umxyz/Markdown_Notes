# [shell脚本去重](https://blog.csdn.net/laobai1015/article/details/91455406)

测试文件如下

```shell
jason
jason
jason
fffff
jason
```

### 第一种去重方法： sort -u 文件名 或者 cat 文件名 | sort -u

```shell
[root@bogon ~]# sort -u test
fffff
jason
```

但这样只是将去重后的结果打印在屏幕上，如果想将去重后的内容保存下来，语句为：

sort -u 文件名 > 新文件名

或者

cat 文件名 | sort -u > 新文件名

即可将去重后的内容保存在新文件名中

### 第二种去重方法： **uniq 文件名 或者 cat 文件名 | uniq**

```shell
[root@bogon ~]# uniq test
jason
fffff
jason
```

**由此可见，uniq需要先排序后才能去重，同时将去重后的结果保存在新文件中：cat 文件名 | sort | uniq > 新文件名**

### 第三种去重方法：**sort、管道和uniq结合运用**

（1）去除重复并保留一份重复的数据

```shell
[root@bogon ~]# sort test|uniq
fffff
jason
```

（2）去除所有重复的行（不保留重复的行），并计算行数

```shell
[root@bogon ~]# sort test|uniq -uc
fffff
```

（3）找出所有重复的行，并计算行数

```shell
[root@bogon ~]# sort test|uniq -dc
jason
```

（4）根据某个字段去重

```shell
[root@bogon ~]# sort -k 1,1 -u test
fffff
jason
```

查看sort的用法，-k参数是这么描述的：

​       -k, --key=POS1[,POS2]
　　　　start a key at POS1 (origin 1), end it at POS2 (default end of line)

也就是说-k哪几个列进行排序，pos1是开始列，pos2是结束列

