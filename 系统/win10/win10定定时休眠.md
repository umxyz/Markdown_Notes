# win10定定时休眠

## 计划任务

首先，shutdown.exe 的参数 -h 是睡眠。
其次，在windows10的控制面板-管理工具-任务计划程序（当然，你从其他路径进去也一样）

### 1，打开任务计划程序，在操作里选择创建基本任务。

### 2，第一步页面是让你写个你的任务名称，这个随意。

### 3，点下一步后会来到触发器页面，在这里你选每天。

### 4，继续下一步会来到每日页面，在这里设置一个开始的时间，然后间隔是一天。

### 5，再下一步会来到操作页面，选择启动程序。

### 6，再再下一步会来到完成页面，程序填shutdown.exe，然后添加参数（可选）里填 -h

到时间电脑就会睡眠了，然后再开机后你会发现电脑之前打开的页面都还原封不动在。

## 命令行定时休眠和定时睡眠问题：

定时休眠：以管理员身份运行cmd或者powershell

```shell
powercfg -h on
schtasks /create /tn my-standby /tr "rundll32.exe powrprof.dll,SetSuspendState" /sc once /st 23:30
取消定时任务：schtasks /delete /tn my-standby
```



定时睡眠（定时待机）：

以管理员身份运行cmd或者powershell

```shell
powercfg -h off
schtasks /create /tn my-standby /tr "rundll32.exe powrprof.dll,SetSuspendState" /sc once /st 23:30
```



[注：查看休眠是否开启：powercfg /a

在"powercfg -h on"状态下，以管理员身份运行"rundll32.exe powrprof.dll,SetSuspendState 0,1,0"不会进入睡眠，而是休眠。

在"powercfg -h on"状态下，以管理员身份运行"rundll32.exe powrprof.dll,SetSuspendState Sleep"不会进入睡眠，而是休眠。]

