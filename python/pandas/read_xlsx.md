# read data from xlsx



data_frame = pd.read_xlsx('data.xlsx', sheet_name='sheetname', )



- Read data  from xlsx and transfer to `np.ndarray`

```
data_frame = pd.read_excel('data.xlsx', header=0, sheet_name='fill')  

paths = []
for header in list(data_frame):
    if 'x' in header:
        x = np.array(data_frame[header])
        x = x[~np.isnan(x)]
    elif 'y' in header:
        y = np.array(data_frame[header])
        y = y[~np.isnan(y)]
        ps = np.stack([x,y])
        paths.append(ps)
```

