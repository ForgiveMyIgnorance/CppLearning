# STL六大组件
**STL提供六大组件，彼此之间可以组合套用：**
1. **容器**（containers）。各种数据结构，如vector、list、deque、set、map等，用来存放数据。STL是一种class template。
2. **算法**（algorithms）。各种常用的算法，如sort、search、copy、erase......。STL算法是一种function template。
3. **迭代器**（iterators）。扮演容器与算法之间的胶合剂，是所谓的“泛型指针”。共有五种类型，以及其它衍生变化。迭代器是一种将operator*，operator->，operator++，operator--等指针相关操作予以重载的class template。所有STL容器都附带有自己专属的迭代器。原生指针（native pointer）也是一种迭代器。
4. **仿函数**（functors）。行为类似函数，可作为算法的某种策略（policy）。仿函数是一种重载了operator()的class或者class template。一般函数指针可视为狭义的的仿函数。
5. **配接器**（adapters）。一种用来修饰容器、仿函数、或迭代器接口的东西。配接器的实现技术必须逐一分析。
6. **配置器**（allocators）。负责空间配置与管理。配置器是一个实现了动态空间配置、空间管理、空间释放的class template。
# 六大组件的交互关系
Container通过Allocator取得数据储存空间，Algorithm通过Iterator存取Container内容，Functor可以协助Algorithm完成不同的策略变化，Adapter可以修饰或者套接Functor。
# 同时使用六大组件
```C++
#include<vector>
#include<algorithm>
#include<iostream>
#include<functional>

using namespace std;

//同时使用六大组件
//实现统计数组中不大于40的元素个数
int main()
{
	int ia[6] = { 27, 210, 12, 47, 109, 83 };

	//容器与空间配置器
	vector<int, allocator<int>> vi(ia, ia + 6);

	//使用了算法count_if()
	//less<int>()仿函数
	//函数适配器not1，bind2nd
	//迭代器vi.begin()，与vi.end()
	cout << count_if(vi.begin(), vi.end(), not1(bind2nd(less<int>(), 40)));

	return 0;
}
```
