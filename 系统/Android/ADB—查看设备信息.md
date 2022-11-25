# ADB—查看设备信息

ADB，即 [Android Debug Bridge](https://developer.android.com/studio/command-line/adb.html)，它是 Android 开发/测试人员不可替代的强大工具，也是 Android 设备玩家的好玩具。

**注：** 有部分命令的支持情况可能与 Android 系统版本及定制 ROM 的实现有关。

- [查看设备信息]
  - [型号]
  - [电池状况]
  - [屏幕分辨率]
  - [屏幕密度]
  - [显示屏参数]
  - [android_id]
  - [IMEI]
  - [Android 系统版本]
  - [IP 地址]
  - [Mac 地址]
  - [CPU 信息]
  - [内存信息]
  - [更多硬件与系统属性]

## 查看设备信息

### 型号

命令：

```sh
adb shell getprop ro.product.model
```

输出示例：

```sh
Nexus 5
```

### 电池状况

命令：

```sh
adb shell dumpsys battery
```

输入示例：

```sh
Current Battery Service state:
  AC powered: false
  USB powered: true
  Wireless powered: false
  status: 2
  health: 2
  present: true
  level: 44
  scale: 100
  voltage: 3872
  temperature: 280
  technology: Li-poly
```

其中 `scale` 代表最大电量，`level` 代表当前电量。上面的输出表示还剩下 44% 的电量。

### 屏幕分辨率

命令：

```sh
adb shell wm size
```

输出示例：

```sh
Physical size: 1080x1920
```

该设备屏幕分辨率为 1080px * 1920px。

如果使用命令修改过，那输出可能是：

```sh
Physical size: 1080x1920
Override size: 480x1024
```

表明设备的屏幕分辨率原本是 1080px * 1920px，当前被修改为 480px * 1024px。

### 屏幕密度

命令：

```sh
adb shell wm density
```

输出示例：

```sh
Physical density: 420
```

该设备屏幕密度为 420dpi。

如果使用命令修改过，那输出可能是：

```sh
Physical density: 480
Override density: 160
```

表明设备的屏幕密度原来是 480dpi，当前被修改为 160dpi。

### 显示屏参数

命令：

```sh
adb shell dumpsys window displays
```

输出示例：

```sh
WINDOW MANAGER DISPLAY CONTENTS (dumpsys window displays)
  Display: mDisplayId=0
    init=1080x1920 420dpi cur=1080x1920 app=1080x1794 rng=1080x1017-1810x1731
    deferred=false layoutNeeded=false
```

其中 `mDisplayId` 为 显示屏编号，`init` 是初始分辨率和屏幕密度，`app` 的高度比 `init` 里的要小，表示屏幕底部有虚拟按键，高度为 1920 - 1794 = 126px 合 42dp。

### android_id

命令：

```sh
adb shell settings get secure android_id
```

输出示例：

```sh
51b6be48bac8c569
```

### IMEI

在 Android 4.4 及以下版本可通过如下命令获取 IMEI：

```sh
adb shell dumpsys iphonesubinfo
```

输出示例：

```sh
Phone Subscriber Info:
  Phone Type = GSM
  Device ID = 860955027785041
```

其中的 `Device ID` 就是 IMEI。

而在 Android 5.0 及以上版本里这个命令输出为空，得通过其它方式获取了（需要 root 权限）：

```sh
adb shell
su
service call iphonesubinfo 1
```

输出示例：

```sh
Result: Parcel(
  0x00000000: 00000000 0000000f 00360038 00390030 '........8.6.0.9.'
  0x00000010: 00350035 00320030 00370037 00350038 '5.5.0.2.7.7.8.5.'
  0x00000020: 00340030 00000031                   '0.4.1...        ')
```

把里面的有效内容提取出来就是 IMEI 了，比如这里的是 `860955027785041`。

参考：[adb shell dumpsys iphonesubinfo not working since Android 5.0 Lollipop](http://stackoverflow.com/questions/27002663/adb-shell-dumpsys-iphonesubinfo-not-working-since-android-5-0-lollipop)

### Android 系统版本

命令：

```sh
adb shell getprop ro.build.version.release
```

输出示例：

```sh
5.0.2
```

### IP 地址

每次想知道设备的 IP 地址的时候都得「设置」-「关于手机」-「状态信息」-「IP地址」很烦对不对？通过 adb 可以方便地查看。

命令：

```sh
adb shell ifconfig | grep Mask
```

输出示例：

```sh
inet addr:10.130.245.230  Mask:255.255.255.252
inet addr:127.0.0.1  Mask:255.0.0.0
```

那么 `10.130.245.230` 就是设备 IP 地址。

在有的设备上这个命令没有输出，如果设备连着 WiFi，可以使用如下命令来查看局域网 IP：

```sh
adb shell ifconfig wlan0
```

输出示例：

```sh
wlan0: ip 10.129.160.99 mask 255.255.240.0 flags [up broadcast running multicast]
```

或

```sh
wlan0     Link encap:UNSPEC
          inet addr:10.129.168.57  Bcast:10.129.175.255  Mask:255.255.240.0
          inet6 addr: fe80::66cc:2eff:fe68:b6b6/64 Scope: Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:496520 errors:0 dropped:0 overruns:0 frame:0
          TX packets:68215 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:3000
          RX bytes:116266821 TX bytes:8311736
```

如果以上命令仍然不能得到期望的信息，那可以试试以下命令（部分系统版本里可用）：

```sh
adb shell netcfg
```

输出示例：

```sh
wlan0    UP                               10.129.160.99/20  0x00001043 f8:a9:d0:17:42:4d
lo       UP                                   127.0.0.1/8   0x00000049 00:00:00:00:00:00
p2p0     UP                                     0.0.0.0/0   0x00001003 fa:a9:d0:17:42:4d
sit0     DOWN                                   0.0.0.0/0   0x00000080 00:00:00:00:00:00
rmnet0   DOWN                                   0.0.0.0/0   0x00000000 00:00:00:00:00:00
rmnet1   DOWN                                   0.0.0.0/0   0x00000000 00:00:00:00:00:00
rmnet3   DOWN                                   0.0.0.0/0   0x00000000 00:00:00:00:00:00
rmnet2   DOWN                                   0.0.0.0/0   0x00000000 00:00:00:00:00:00
rmnet4   DOWN                                   0.0.0.0/0   0x00000000 00:00:00:00:00:00
rmnet6   DOWN                                   0.0.0.0/0   0x00000000 00:00:00:00:00:00
rmnet5   DOWN                                   0.0.0.0/0   0x00000000 00:00:00:00:00:00
rmnet7   DOWN                                   0.0.0.0/0   0x00000000 00:00:00:00:00:00
rev_rmnet3 DOWN                                   0.0.0.0/0   0x00001002 4e:b7:e4:2e:17:58
rev_rmnet2 DOWN                                   0.0.0.0/0   0x00001002 4e:f0:c8:bf:7a:cf
rev_rmnet4 DOWN                                   0.0.0.0/0   0x00001002 a6:c0:3b:6b:c4:1f
rev_rmnet6 DOWN                                   0.0.0.0/0   0x00001002 66:bb:5d:64:2e:e9
rev_rmnet5 DOWN                                   0.0.0.0/0   0x00001002 0e:1b:eb:b9:23:a0
rev_rmnet7 DOWN                                   0.0.0.0/0   0x00001002 7a:d9:f6:81:40:5a
rev_rmnet8 DOWN                                   0.0.0.0/0   0x00001002 4e:e2:a9:bb:d0:1b
rev_rmnet0 DOWN                                   0.0.0.0/0   0x00001002 fe:65:d0:ca:82:a9
rev_rmnet1 DOWN                                   0.0.0.0/0   0x00001002 da:d8:e8:4f:2e:fe
```

可以看到网络连接名称、启用状态、IP 地址和 Mac 地址等信息。

### Mac 地址

命令：

```sh
adb shell cat /sys/class/net/wlan0/address
```

输出示例：

```sh
f8:a9:d0:17:42:4d
```

这查看的是局域网 Mac 地址，移动网络或其它连接的信息可以通过前面的小节「IP 地址」里提到的 `adb shell netcfg` 命令来查看。

### CPU 信息

命令：

```sh
adb shell cat /proc/cpuinfo
```

输出示例：

```sh
Processor       : ARMv7 Processor rev 0 (v7l)
processor       : 0
BogoMIPS        : 38.40

processor       : 1
BogoMIPS        : 38.40

processor       : 2
BogoMIPS        : 38.40

processor       : 3
BogoMIPS        : 38.40

Features        : swp half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt
CPU implementer : 0x51
CPU architecture: 7
CPU variant     : 0x2
CPU part        : 0x06f
CPU revision    : 0

Hardware        : Qualcomm MSM 8974 HAMMERHEAD (Flattened Device Tree)
Revision        : 000b
Serial          : 0000000000000000
```

这是 Nexus 5 的 CPU 信息，我们从输出里可以看到使用的硬件是 `Qualcomm MSM 8974`，processor 的编号是 0 到 3，所以它是四核的，采用的架构是 `ARMv7 Processor rev 0 (v71)`。

### 内存信息

命令：

```sh
adb shell cat /proc/meminfo
```

输出示例：

```sh
MemTotal:        1027424 kB
MemFree:          486564 kB
Buffers:           15224 kB
Cached:            72464 kB
SwapCached:        24152 kB
Active:           110572 kB
Inactive:         259060 kB
Active(anon):      79176 kB
Inactive(anon):   207736 kB
Active(file):      31396 kB
Inactive(file):    51324 kB
Unevictable:        3948 kB
Mlocked:               0 kB
HighTotal:        409600 kB
HighFree:         132612 kB
LowTotal:         617824 kB
LowFree:          353952 kB
SwapTotal:        262140 kB
SwapFree:         207572 kB
Dirty:                 0 kB
Writeback:             0 kB
AnonPages:        265324 kB
Mapped:            47072 kB
Shmem:              1020 kB
Slab:              57372 kB
SReclaimable:       7692 kB
SUnreclaim:        49680 kB
KernelStack:        4512 kB
PageTables:         5912 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:      775852 kB
Committed_AS:   13520632 kB
VmallocTotal:     385024 kB
VmallocUsed:       61004 kB
VmallocChunk:     209668 kB
```

其中，`MemTotal` 就是设备的总内存，`MemFree` 是当前空闲内存。

### 更多硬件与系统属性

设备的更多硬件与系统属性可以通过如下命令查看：

```sh
adb shell cat /system/build.prop
```

这会输出很多信息，包括前面几个小节提到的「型号」和「Android 系统版本」等。

输出里还包括一些其它有用的信息，它们也可通过 `adb shell getprop <属性名>` 命令单独查看，列举一部分属性如下：

| 属性名                          | 含义                          |
| ------------------------------- | ----------------------------- |
| ro.build.version.sdk            | SDK 版本                      |
| ro.build.version.release        | Android 系统版本              |
| ro.build.version.security_patch | Android 安全补丁程序级别      |
| ro.product.model                | 型号                          |
| ro.product.brand                | 品牌                          |
| ro.product.name                 | 设备名                        |
| ro.product.board                | 处理器型号                    |
| ro.product.cpu.abilist          | CPU 支持的 abi 列表[*节注一*] |
| persist.sys.isUsbOtgEnabled     | 是否支持 OTG                  |
| dalvik.vm.heapsize              | 每个应用程序的内存上限        |
| ro.sf.lcd_density               | 屏幕密度                      |

*节注一：*

一些小厂定制的 ROM 可能修改过 CPU 支持的 abi 列表的属性名，如果用 `ro.product.cpu.abilist` 属性名查找不到，可以这样试试：

```sh
adb shell cat /system/build.prop | grep ro.product.cpu.abi
```

示例输出：

```sh
ro.product.cpu.abi=armeabi-v7a
ro.product.cpu.abi2=armeabi
```