`sudo apt-get update`

等上面命令执行完后，再执行sudo apt-get install就可以了！其实错误信息已经很明确了，Unable to locate packet就是无法找到包嘛，那还不赶紧sudo apt-get update下！



附另一篇文章：

原文地址：http://blog.chinaunix.net/uid-22002627-id-3475650.html

碰到这个问题后找到这个帖子就转了过来 当用apt-get更新软件包时常出现错误提示Unable to locate package update, 尤其是在ubuntu server上,解决方法是： 先更新apt-get #sudo apt-get update 执行完后，问题就解决了。 继续更新： #sudo apt-get upgrade 然后就可以

