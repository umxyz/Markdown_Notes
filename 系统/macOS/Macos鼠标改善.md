# Macos鼠标改善

## 禁用鼠标加速

您可以从终端更改一个隐藏的首选项。读取其当前值类型

```shell
defaults read .GlobalPreferences com.apple.mouse.scaling
```


在终端提示下。正常值为0〜3，可以通过移动“系统偏好设置”的“鼠标”面板中的“跟踪速度”滑块来设置。因此，值0〜3不会禁用加速。

但是，如果通过键入将其设置为-1

```shell
defaults write .GlobalPreferences com.apple.mouse.scaling -1
```


在终端中，这似乎禁用了加速功能，并将鼠标跟踪速度设置为无法更改的恒定预定义值。

我发现我必须注销然后重新登录才能生效。在那之后，`pixels pointer moves / meters mouse moved`比率是恒定的，但是不幸的是无法调节。

### 如何撤消更改

要恢复为Apple的默认设置，只需打开“系统偏好设置”的“鼠标”面板并将“跟踪速度”更改为任何值，然后退出“系统偏好设置”。

鼠标≠触控板

Mac OS X独立存储鼠标和触控板设置。如果要禁用触控板而不是鼠标的加速，说明是相同的，只要在上面看到`com.apple.trackpad.scaling`的任何地方都替换为`com.apple.mouse.scaling`(显然，请使用“系统偏好设置”的触控板 Pane 而不是“鼠标” Pane )。
