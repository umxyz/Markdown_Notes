# [mac下软件意外退出或崩溃报错时弹窗的关闭方法](https://blog.csdn.net/qq_43827595/article/details/103178501)

关闭软件意外退出弹窗：软件意外崩溃让人烦心，重新打开后还会一遍遍弹出的问题报告

终端下运行

```shell
defaults write com.apple.CrashReporter DialogType none 关闭这个问题报告
defaults write com.apple.CrashReporter DialogType crashreport 恢复其显示错误报告
```

用这个方法可以解决Copytranslator退出是弹出意外窗口的问题

