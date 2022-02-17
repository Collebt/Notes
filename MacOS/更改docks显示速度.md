## 改变docks的动画

加快dock的动画速度，更改-float后面的数字来调整，如果要取消动画，则改变-int后面的数字。



```bash
defaults write com.apple.dock autohide-time-modifier -int 0;killall Dock
```

```
defaults write com.apple.dock autohide-time-modifier -float 0.12;killall Dock
```



恢复默认：

```
defaults delete com.apple.dock autohide-time-modifier;killall Dock
```



