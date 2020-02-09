### 文章目录

- [XTU 设置教程 自动化 睡眠 休眠](https://blog.csdn.net/qq_43041976/article/details/104087965#XTU_____2)

- - [原理](https://blog.csdn.net/qq_43041976/article/details/104087965#_3)
  - [确认/验证您的降压没有持续](https://blog.csdn.net/qq_43041976/article/details/104087965#_38)
  - [正确设置降压的指南](https://blog.csdn.net/qq_43041976/article/details/104087965#_48)



# XTU 设置教程 自动化 睡眠 休眠

## 原理

先将XTU服务改为 `自动运行` 而不是 `自动运行（延迟）`

\#XTU参数id代码: `powershell` 运行

```shell
&'C:\Program Files (x86)\Intel\Intel(R) Extreme Tuning Utility\Client\XTUCli.exe' -i all
1
Kill_XTU_Service.bat
```

这个bat会在每次系统休眠或睡眠时启动

把xtu的GUI app跟service关掉

这样可以防止休眠或睡眠失败直接重开机

```
XTU_cli_1.bat` 跟 `XTU_cli_2.bat
```

这两个会在系统从休眠或睡眠唤醒时启动

两个档案除了降压数值以外是一样的

用两个降压设定来解决xtu显示有降但是实际没降的情况

`xml`

任务计划程序

`XTU_cli_1.bat` 跟 `XTU_cli_2.bat`会隔一分钟启动

这样电压设定就一定会改变

xtu就不会显示有降 实际没降

## 确认/验证您的降压没有持续

如果您不在乎，并想直接转到有关如何正确设置降压以使其即使在恢复后也能正常工作的指南，则可以跳过本节。这仅对当前通过脚本进行降压设置的用户有用。

1. 启动`HWInfo`或XTU并监视系统空闲时报告的最低核心电压。对于i5，该值应约为0.6 + V。
2. 启动XTU应用并施加降压（假设内核上为-100mV）
3. 空转时监视`HWInfo`或XTU中的核心电压。本质上，该数字应比步骤1中的数字低100mV。这证明了正确施加了降压
4. 现在休眠系统，然后恢复它
5. 重复步骤1。您会发现，即使XTU和HWInfo“认为”施加了降压，所报告的CPU核心电压仍在0.6 + V范围内（对于i5），表示未施加降压。“重新施加”降压的唯一方法是进入XTU应用程序并选择一个不同的UV电压，然后施加它。

## 正确设置降压的指南

脚本/任务所做的主要事情如下：

1. `Kill_XTU_Service.bat`每次使系统进入睡眠/休眠状态时都会由任务启动。这将杀死性能程序（XTU GUI应用程序）以及XTU服务。之所以需要这样做，是因为如果不将其杀死，恢复将导致完全重启。
2. `XTU_cli_1.bat`和`XTU_cli_2.bat`-这些是适用略有不同`undervolts`的CPU，GPU和高速缓存相同的批处理文件。每当系统从睡眠/休眠状态恢复时，它们都是通过计划任务启动的。批处理文件将启动XTU服务，等待几秒钟，然后运行两个批处理文件。
3. 计划任务（XML文件）被设置为在适当的时间启动上述批处理文件。`XTU_cli_1.bat`和`XTU_cli_2.bat`分别在1分钟和2分钟的延迟后启动。如果批处理文件的电压设置过高，这将给您时间手动停止或取消这些任务。

因为这两个降压批处理文件都已运行，所以两个“降压”批处理文件之一将被“占用”并应用，因为它与XTU服务仍认为处于活动状态的以前的XTU设置不同。这与连续的恢复保持交替，以确保在从休眠状态恢复后的1-2分钟内施加降压。

**文件和安装**

1. 下载以下zip文件，其中包含3个计划任务和3个批处理文件的3个XML文件。[https://www.dropbox.com/s/y8leustr8cqdohf/Intel%20XTU%20Tuning.zip?dl=0](https://www.dropbox.com/s/y8leustr8cqdohf/Intel XTU Tuning.zip?dl=0)
2. 将所有3个批处理文件放在以下位置：`C:\Program Files (x86)\Intel\Intel(R) Extreme Tuning Utility\`。如果选择其他位置，则需要在导入后相应地编辑XML文件或计划的任务。
3. 编辑批处理文件，然后将CPU，GPU和缓存降压设置设置为适合您的数字。这些数字必须精确到批处理文件中的小数位数。最初设置降压和压力测试以确保稳定性时，您可以从XTU GUI应用程序中找出正确的数字。
4. 从任务计划程序中导入每个XML任务。

> 引用：
>
> 1. https://www.reddit.com/r/Surface/comments/3y1pk2/psa_your_undervolt_is_likely_not_sticking/
> 2. https://www.ptt.cc/bbs/WindowsPhone/M.1450937658.A.233.html

 