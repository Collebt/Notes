# 设计gui的一些记录



## 切换界面

原界面执行文件: `main.m`

原界面UI文件:`main.fig`

切换界面文件: `swap.m`

切换界面UI文件: `swap.fig`



制作原界面切换按钮button_swap

对应的callback函数:

```matlab
function button_swap_Callback_fun(hObject)

%首先关闭当前界面
close gcf

%运行要进入的新界面
swap %这里是swap.m的函数名,需要将该文件放在路径中
```



## 在另外的窗口绘图

原界面执行文件: `main.m`

原界面UI文件:`main.fig`

绘图界面文件: `draw.m`

绘图界面UI文件: `draw.fig`



制作原界面切换按钮button_draw

对应的callback函数:

```matlab
function button_swap_Callback_fun(hObject)

%首先打开绘图窗口
open('draw.fig')

%运行要进入的新界面
h = guihandles; %将打开的gui的handles放入h变量中
axes(h.axes1) %设置对应的坐标轴
draw();%执行绘图函数
```

