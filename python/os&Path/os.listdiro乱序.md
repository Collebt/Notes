# os.listdir乱序问题

使用该函数获得目录中文件是乱序的，需要重新排序，排序的依据是文件的数字索引。

==关键在于如何取出数字字符==

```python
filenames = ['frame_0.png', 'frame_1.png', 'frame_10.png', 'frame_11.png', 'frame_12.png', 'frame_13.png', ...]

filenames.sort(key=lambda x: int(x.split(".")[0].split("_")[1]))  #

print(filenames)

\#输出['frame_0.png', 'frame_1.png', 'frame_2.png', 'frame_3.png', 'frame_4.png', 'frame_5.png', ...
```



