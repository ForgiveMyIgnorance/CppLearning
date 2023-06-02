# 概述
list与vector是两个最常使用的容器。相比较于vector的连续线性空间，list在空间中更加复杂。
但是list的好处是每次插入或者删除一个元素，就配置或者释放一个空间，因此list对于空间的运用绝对的精准，一点也不浪费。
**对于任何位置的元素插入或者元素移除，list永远是常数时间。**
# 链表
链表是一种通过指针串联在一起的线性结构。
每一个节点（node）由两部分组成，一个是数据域，一个是指针域（存放指向下（或上）一个节点的指针），最后一个节点的指针域指向null（空指针的意思）。
链表的入口节点称为链表的头结点也就是head。
+ 节点
   + 指针域（pointer）
      + prev：上一节点的指针
      + next：下一节点的指针
   + 数据域（data）
# 链表的迭代器
list不再能像vector一样使用普通的指针作为迭代器。
list本身与节点是分开设计的。
list的迭代器必须能够有能力指向list的节点，并正确的
+ 递增：指向下一个节点
+ 递减：指向上一个节点
+ 取值：取出节点的数据值
+ 成员存取：取出节点的成员
**与vector不同的是，list的元素插入（insert）和接合（splice）操作都不会造成原有的list迭代器失效。**

## 成员函数
```C++
==
!=
*   //取出节点的数据值

->
ite++
++ite
ite--
--ite
```
## list的元素操作
```C++
push_front
push_back
erase
pop_front
pop_back
clear
remove(value)//将数值为value的所有元素移除
unique()//移除“连续而相同的元素”至剩余一个
//（不公开）
transfer(pos,first,last)//将[first, last)之间的所有元素移动至pos之前
//是下面函数的基础
splice(pos,list)//将某连续范围的元素从一个list移动到另一个的某个节点之前
splice(pos,list,ite)//将ite所指元素接合于pos之前，pos和i可指向同一个list
splice(pos,list,first,last)//将[first,last)内的所有元素接合于pos所指元素之前，pos和【first，last）可指向同一个list，但pos不能位于【first，last）之内
merge
reverse
sort
```
