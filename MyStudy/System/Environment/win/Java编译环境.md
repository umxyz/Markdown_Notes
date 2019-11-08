## Windows 10 Java环境变量配置

**Win10下 Java环境变量配置**

JDK下载：http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html

（注：win10的Java环境变量配置和其他的windows版本稍有不同）

**在电脑桌面 按 `win + s`  搜索`control panel`**

**打开 系统和安全 然后 再打开 系统**

**选择“高级系统设置”选项**

![img](https://images2015.cnblogs.com/blog/805379/201605/805379-20160512223219655-1251440251.png)

**点击下面的“环境变量”选项**

![img](https://images2015.cnblogs.com/blog/805379/201605/805379-20160512223357046-1881703129.png)

接下来就是具体的配置过程：

**点击“系统变量”下面的”新建“选项**

![img](https://images2015.cnblogs.com/blog/805379/201605/805379-20160512223611077-1852208980.png)

**在”变量名“处填上`Java_Home`**

**”变量值“为JDK安装路径，`C:\Program Files\Java\jdk1.8.0_211`**

**点击”确定“选项**

![img](https://images2015.cnblogs.com/blog/805379/201605/805379-20160512223838546-1858485630.png)

**在”系统变量“中找到`Path`**

![img](https://images2015.cnblogs.com/blog/805379/201605/805379-20160512224107702-1187773252.png)

**选中”`Path`“点击”编辑“选项**

新建两个变量分别为

**`%Java_Home%\bin`**

**`%Java_Home%\jre\bin;`，到“变量值”栏的最前面，“确定”**

或

**`C:\Program Files\Java\jdk1.8.0_211\bin`**

**`C:\Program Files\Java\jdk1.8.0_211\jre\bin`**

**在“系统变量”栏，“新建”，“变量名”为`CLASSPATH`，“变量值”为**

**`.;%Java_Home%\bin;%Java_Home%\lib\dt.jar;%Java_Home%\lib\tools.jar`，“确定”**

或

**`.;C:\Program Files\Java\jdk1.8.0_211\bin;C:\Program Files\Java\jdk1.8.0_211\lib\dt.jar;C:\Program Files\Java\jdk1.8.0_211\lib\tools.jar`**

![img](https://images2015.cnblogs.com/blog/805379/201605/805379-20160512224843484-1356351538.png)

点击“环境变量”最下面的“确定”选项

**回到电脑桌面，按快捷键`Win + R`，输入`cmd`**

![img](https://images2015.cnblogs.com/blog/805379/201605/805379-20160512225105562-1578800234.png)

检查Java环境是否配置成功

输入`Java`

![img](https://images2015.cnblogs.com/blog/805379/201605/805379-20160512225343452-1007903408.png)

 

输入`javac`

![img](https://images2015.cnblogs.com/blog/805379/201605/805379-20160512225205765-304825305.png)

输入`java -version`

![img](https://images2015.cnblogs.com/blog/805379/201605/805379-20160512225445859-652093728.png)

 

如果上面的三幅图都看见了，恭喜，环境变量配置好了！

