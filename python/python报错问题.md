# Ubuntu vscode无法画图

==最终方案==：使用`plt.savefig()`函数，直接保存图像，方便后期记录，也不占用显示资源。但是也会遭遇报错问题，用`export DISPLAY=:0.0`解决



---

在终端上跑程序可以画图，但在vscode里面无法出现窗口，无论是bokeh还是matplotlib都不行

**原因**：没有配置好环境变量

**解决方法**：

`ctrl+alt+T`打开终端

` echo $DISPLAY`:没东西显示，表示环境变量没有设置）

`export DISPLAY=:0.0`

 每次在vscode运行可能需要在下面terminal输入一次



**问题**：可能是框架程序使用了不画图的agg终端，要自己转换成画图的终端。

**解决方案**：`import matplotlib`,在画图前写一句`matplotlib.use('TKAgg')`

在代码首行添加是没用的,代码在运行过程中终端被修改了。

某些库import的过程中会修改matplotlib的终端类型,因此要在debug前面一句之前加入修改



或者在命令行输入，（当上面的命令无效的时候可以使用）

```
echo "backend: Agg" > ~/.config/matplotlib/matplotlibrc
```

