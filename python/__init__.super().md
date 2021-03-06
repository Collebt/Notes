# \_\_init\_\_中的super()

因为Python中存在多重继承，在新式类中，要查找或调用一个方法或属性时，使用的是广度优先搜索算法；而在经典类中则使用深度优先搜索算法。

 

用super来调用\_\_init\_\_的方式,设计得当的话,可以使得每个类的\_\_init\_\_恰好被调用一次，supr()方式中,最重要的是_\_init_\_参数传递的问题

 

Python中的**super()**方法设计目的是用来解决多重继承时父类的查找问题，所以在单重继承中用不用 super 都没关系；但是，**使用 super() 是一个好的习惯**。一般我们在子类中需要调用父类的方法时才会这么用。

 

这样做的好处就是：如果你要改变子类继承的父类（由A改为B），你只需要修改一行代码（class C(A): -> class C(B)）即可，而不需要在class C的大量代码中去查找、修改基类名，另外一方面代码的可移植性和重用性也更高。