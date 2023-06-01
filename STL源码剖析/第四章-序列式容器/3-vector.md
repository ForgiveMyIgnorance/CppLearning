# vector概述
vector与array十分相似（线性连续空间）。唯一的区别就是空间运用的灵活性，array是静态空间，vector是动态空间。

# 成员函数
```C++
begin()
end()
size()
capacity()//返回可用空间的容量
empty()
operator[]//通过下标访问元素

vector()//空
vector(n, value)

front()//第一个元素
back()//最后一个元素

insert(pos, n, y)
push_back(x)//将元素插入至最末尾
pop_back()//最末尾元素删除
erase(ite)//清除某位置上的元素 后续元素向前移动
erase(x,y)//删除[x, y)的元素

resize(x, x)//重新分配大小

clear()//清除所有元素
```
**vector的迭代器不支持 it < v1.end() 写法，因此循环条件只能用 it != vi.end()**
# vector的迭代器
**在常用STL容器中，只有在vector和string中，才允许使用vi.begin()+3这种迭代器加上整数的写法**
普通指针都可以作为vector的迭代器而满足所有必要条件。
vector容量永远大于等于容器大小。
当增加新元素时，容量会扩充为当前的两倍。
**对vector的任何操作，一旦引起空间重新配置，指向原vector的迭代器就都失效了。**

# 常用函数
## pop_back()
把尾端元素拿掉，并调整大小
## erase(first,last)
清除\[first,last)的所有元素
## erase(pos)
## insert(pos,n,x)
在pos前插入n个元素x
