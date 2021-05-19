

Channels last memory format is an alternative way of ordering NCHW tensors in memory preserving dimensions ordering. Channels last tensors ordered in such a way that channels become the densest dimension (aka storing images pixel-per-pixel).



只有4Dtensor才可以使用channels_last，其他使用is_contiguous(memory_format=torch.channels_last)判断为False。



转换方式



```python
to(memory_format=torch.channels_last)#recommend
contiguous(memory_format=torch.channels_last)
```

