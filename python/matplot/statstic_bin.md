```python
import matplotlib.pyplot as plt
import numpy as np

# create sample data
set1 = np.random.normal(50, 10, 100)
set2 = np.random.normal(60, 15, 100)

n1, bins1, patches1 = plt.hist(set1, bins=20, color='green', alpha=0.5, label='Set 1')
n2, bins2, patches2 = plt.hist(set2, bins=20, color='red', alpha=0.5, label='Set 2')

# set the x-axis and y-axis labels
plt.xlabel('Score')
plt.ylabel('Frequency')

n1 = n1 / np.sum(n1)
n2 = n2 / np.sum(n2)

# plot the normalized histograms as curves
plt.plot(bins1[:-1], n1, color='green')
plt.plot(bins2[:-1], n2, color='red')

# set the x-axis and y-axis labels
plt.xlabel('Score')
plt.ylabel('Normalized Frequency')

# add a legend to the plot
plt.legend()


# add a legend to the plot
plt.legend()


```





interpolate the curve

```
interp_func1 = interpolate.interp1d(bins1[:-1], n1, kind='cubic')
interp_func2 = interpolate.interp1d(bins2[:-1], n2, kind='cubic')

# create a new range of values for the x-axis to plot the smooth curves
xnew = np.linspace(min(bins1), max(bins2), num=100, endpoint=True)

# plot the smoothed curves
plt.plot(xnew, interp_func1(xnew), color='green', label='Set 1 (smooth)')
plt.plot(xnew, interp_func2(xnew), color='red', label='Set 2 (smooth)')
```



smooth the curve

```
# smooth the data using a Savitzky-Golay filter
window_size = 7
order = 3
n1_smoothed = savgol_filter(n1, window_size, order)
n2_smoothed = savgol_filter(n2, window_size, order)

# plot the smoothed curves
plt.plot(bins1[:-1], n1_smoothed, color='green', label='Set 1 (smooth)')
plt.plot(bins2[:-1], n2_smoothed, color='red', label='Set 2 (smooth)')

```

