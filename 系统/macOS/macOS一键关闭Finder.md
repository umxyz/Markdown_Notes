# macOS一键关闭Finder

启用退出Finder的菜单项，终端输入

```bash
defaults write com.apple.finder QuitMenuItem -bool YES && killall Finder
```

打开任意一个Finder窗口，点击“访达”，或使用APP退出的通用快捷键“command + Q”，即可关闭全部的Finder窗口。

注：启用后仍然可以打开Finder窗口，但Finder窗口不会再一个一个地占用Docer栏。可以右键Finder APP，调出需要的窗口。

恢复

```bash
defaults write com.apple.finder QuitMenuItem -bool NO && killall Finder
```

