## Mac OS字体平滑设置

关闭：

```shell
defaults -currentHost write -globalDomain AppleFontSmoothing -int 0
```

1用于光线平滑，2用于中等平滑，3用于强平滑。

执行命令后，您需要重新加载Finder和所有其他打开的应用程序以查看有效的更改，您可以通过杀死它来重新加载Finder：

```shell
killall Finder
```

另一种选择是简单地重启Mac，或者注销并重新登录，因为重新启动Finder以及WindowServer和所有其他应用程序，以使字体平滑更改生效。

恢复：

```
defaults -currentHost delete -globalDomain AppleFontSmoothing
```

