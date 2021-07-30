# 删除我的电脑WPS云文档图标和禁止启动WPS云文档右下角图标方法

## 一、去除资源管理器“WPS云文档”：

打开注册表，定位到：HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace 将此键值下面的“wps项”删除。

## 二、去除资源管理器左侧栏的“WPS云文档”：

打开注册表，定位到：HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Desktop\NameSpace 将此键值下面的“wps项”删除。

## 三、去除WPS界面右上角“xxxx机关单位WPS专属服务通道”

--找到安装目录，进入office6\cfgs\ 将oeminfo文件夹改为oeminfo.bak

## 四、禁止启动WPS时同时启动“WPS云文档”(禁用右下角托盘图标)：

找到安装目录，进入office6文件夹，找到wpscloudsvrimp.dll，将其修改为：wpscloudsvrimp.dll.bak