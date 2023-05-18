```
a = torch.arange(0, 32, 2).reshape(4, 4)
d = (a>16).nonzero(as_tuple=True)
print(d)
print(a[d])
```





1. 要用tuple作为检索的组成

a是一个多维tensor，a.shape=[N, M]

通过检索的方式选择K个元素，

d = （tensor[i1, i2, i3, i4], tensor[j1,j2,j3,j4]), d.shape=[K，2]，**注意d是tuple**

a[d] =[ a_(i1,j1),  a_(i2,j2), ..., a(i4,j4)]

---

2. 直接用mask检索

a是一个多维tensor，a.shape=[N, M]

m是一个和a相同大小的tensor， m.shape=[N,M], m.type=bool

a[m] = [where (a == 1)]