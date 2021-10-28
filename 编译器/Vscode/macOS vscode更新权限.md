# macOS vscode更新权限

```shell
sudo chown -R $USER ~/Library/Caches/com.microsoft.VSCode.ShipIt
xattr -dr com.apple.quarantine /Applications/Visual\ Studio\ Code.app
```

