

# 计算微分方程

使用scipy的integrate函数



odeint用于计算偏微分方程:

输入

```
sol = odeint(func, y0, c, args=(b, c))
```

其中`func`为函数

```
def fim(y, x, b, c)
```

x为自变量,y为因变量, bc是常数



例子:

- 二阶方程

$$
\theta''(t) + b\theta'(t) + c\sin(\theta(t)) = 0
$$

变换为一阶多元函数
$$
\left\{
        {\theta'(t) = \omega(t) \atop
        \omega'(t) = -b\omega(t) - c\sin(\theta(t))}
	\right.
$$


```python
def pend(y, t, b, c):
    theta, omega = y
    dydt = [omega, -b*omega - c*np.sin(theta)]
  	return dydt

y0 = [np.pi - 0.1, 0.0]#定义初始值
t = np.linspace(0, 10, 101) #变量的上下区间和微分单元
b = 0.25#常数项
c = 5.0
sol = odeint(pend, y0, t, args=(b, c))
```



- 多元一介方程
  $$
  \frac{ds}{dt} = -R0(s(t), i(t))s(t)i(t),\\
  \frac{di}{dt} = R0(s(t), i(t))s(t)i(t) - i(t),
  $$
  

```python
y0 = [s, i]

    def func(y, t):
        s, i = y
        dsdt = -R0(s,i) * s * i
        didt = (R0(s, i) * s * i) - i
        dydt = [dsdt, didt]
        return dydt

    t_ode = np.linspace(0, t, n)
    sol = integrate.odeint(func, y0, t_ode)
```

