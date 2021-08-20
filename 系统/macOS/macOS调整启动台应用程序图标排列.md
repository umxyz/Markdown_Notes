# macOS调整启动台应用程序图标排列

下面详细说说每一步是在干嘛：

```shell
1、调整每一列显示图标数量，8表示每一列显示8个（一般7、8就不错），比较不错，可根据个人喜好进行设置。 
defaults write com.apple.dock springboard-rows -int 8

2、调整多少行显示图标数量，这里我用的是7 
defaults write com.apple.dock springboard-rows -int 7

3、重置Launchpad
defaults write com.apple.dock ResetLaunchPad -bool TRUE

4、重启Dock
killall Dock
```

如果我们想回复成默认的排列呢！（默认的是5行7列）

```shell
defaults write com.apple.dock springboard-rows Default
defaults write com.apple.dock springboard-columns Default
defaults write com.apple.dock ResetLaunchPad -bool TRUE
killall Dock
```