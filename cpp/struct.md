# Struct

```cpp
struct A{
};
struct B : public A{
};
```

默认的继承访问权限：struct是public的，class是private的.

是public继承还是private继承，取决于子类而不是基类.

struct可以继承class，同样class也可以继承struct，那么默认的继承访问权限是看子类到底是用的struct还是class.

```
    struct A{};
    class B: A{};  // private继承
    struct C: B{}; // public继承
```

