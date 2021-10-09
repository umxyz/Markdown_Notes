# macOS Dock栏全屏弹出慢

终端输入

```bash
defaults write com.apple.Dock autohide-delay -float 0 && killall Dock
```

恢复

```bash
defaults delete com.apple.Dock autohide-delay && killall Dock       
```

> 注：使用快捷键**command + ->|** 切换APP更地道，如果习惯像Windows那样在任务栏切APP可参考这个。

