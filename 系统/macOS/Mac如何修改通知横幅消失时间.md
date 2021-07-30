# [Mac如何修改通知横幅消失时间](https://blog.keepchen.com/a/mac-notification-hide-duration.html)

首先打开`终端`，然后运行以下命令：

```shell
defaults write com.apple.notificationcenterui bannerTime -int {多少秒后消失}
# 如 defaults write com.apple.notificationcenterui bannerTime -int 2
```

然后**重启电脑**。

重启后设置生效。

想要手动触发通知来测试一下，可以打开`终端`运行以下命令：

```shell
osascript -e 'display notification "test notification!"'
```

如果想还原回系统默认的状态，可以删除配置，打开`终端`运行以下命令：

```shell
defaults delete com.apple.notificationcenterui bannerTime
```

**重启系统**后生效。

