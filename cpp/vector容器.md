# Vector容器

引用头文件 #include \<Vector\>

Vector是一种类模板，不是一种数据类型和。

 

几种定义和初始化方法

```c++
Vector\<int\> v1;

Vector\<int\> v2(v1); //v2是v1的一个副本

Vector\<int\> v3(n, i); //v3包含n个值为1的元素

Vector\<int\> v4(n); //v4包含n个值为0的元素
```

 

常用的几种操作：

```c++
push_back(t); //在最后添加值为t的数据

pop_back(); // 在数组的最后移除最后一个数据

clear(); //清空

size(); //返回元素的数量

erase(t); //删除指定元素t

empty(); //判断数组是否为空
```

