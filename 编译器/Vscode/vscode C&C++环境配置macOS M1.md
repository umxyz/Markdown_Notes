# M1 MacOS VSCode配置C++环境

## 第一步：下载VSCode

vscode官网国内访问确实很慢，耐心等

点击前往vscode官网

选择下载Universal版本（支持arm架构）![img](../../_ImageAssets/dda38846ad22d67d888d98ea4d1920b1.png)

## 第二步：安装VSCode

选择好路径无脑下一步就行

## 第三步：安装插件

安装C/C++、CodeLLDB、C++ Intellisense

![img](../../_ImageAssets/7cc2d3e45b672d641d7205df48d07c35-20210506232143987.png)

**一定要安装CodeLLDB**，要不然会无法debug，听说是apple取消了macos对lldb的支持，所以要用这个插件才能使用debug

#### 第四步：生成c_cpp_properties.json配置文件

首先新建一个cpp文件，随便写点啥。

接着shift+command+p，选择C/C++:Edit Configurations(UI)

按照下图配置

![image-20210506232813670](../../_ImageAssets/image-20210506232813670.png)