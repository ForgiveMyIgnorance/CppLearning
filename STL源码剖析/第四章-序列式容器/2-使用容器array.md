# 数组
**必须声明数组大小**
## 概述
STL array数组容器是为了替代内置数组而设计，表示长度固定的数组，并提供了多个STL方法（但是不包括push_back()，insert()），是属于序列容器。
## array的数组结构
**array数组容器元素固定，在内存中是线性结构，内存连续，各元素间连续。**
# 数组容器测试
## 辅助函数
```C++
//辅助测试程序
#include <iostream> 
using namespace std;
#include <string>
using std::string;
#include <cstdlib> //RAND_MAX 0~32767
#include <cstdio>  //_snprintf()
const long ASIZE = 250000L;
long get_a_target_long();
string get_a_target_string();
int compareLongs(const void* a, const void* b);
int compareStrings(const void* a, const void* b);
 
long get_a_target_long()
{
	long target = 0L;
	cout << "target (0~" << RAND_MAX << "): ";
	cin >> target;
	return target;
}
 
string get_a_target_string()
{
	long target = 0L;
	char buf[10];
	cout << "target (0~" << RAND_MAX << "): ";
	cin >> target;
	_snprintf(buf, 10, "%d", target);  //VS中的用法
	return string(buf);
}
 
int compareLongs(const void* a, const void* b)
{
	return (*(long*)a) - (*(long*)b);
}
 
int compareStrings(const void* a, const void* b)
{
	if (*(string*)a > *(string*)b)
		return 1;
	else if (*(string*)a < *(string*)b)
		return -1;
	else
		return 0;
}
```
上面四个函数是为了进行容器设置而编写。
## 主程序实现
```C++
#include "STLTest.h" //辅助函数
//容器array
#include <array>
#include <iostream>
#include <ctime>
#include <cstdlib> //qsort,bsearch, NULL,abort
using namespace std;
 
int _tmain(int argc, _TCHAR* argv[])
{
	cout << "test_array()......................\n";
	array<long, ASIZE> c;
  //声明一个计时变量timeStart，通过程序运行前后的时间差来计算耗时clock() - timeStart，头文件时<ctime>
	clock_t timeStart = clock();
	srand((unsigned)time(NULL)); //种子，产生随机
	for (long i = 0; i < ASIZE; ++i)
	{
		try
		{
      //使用随机数函数rand()生成long类型值，在遍历的过程中放置容器中。
      //注意在rand()前要有时间种子，才能时程序每次产生不同的随机数
			c[i] = rand();
		}
		catch (exception* p)
		{
			cout << "i = " << i << " " << p->what() << endl;
			abort();
		}
	}
	cout << "front: " << c[0] << endl;  //第一个array容器中的数值
	cout << "milli-seconds: " << (clock() - timeStart) << endl;  //存放25000个数需要的时间
	cout << "array.size() = " << c.size() << endl;//array的大小
	cout << "array.front() =  " << c.front() << endl; //第一个array容器中的数值
	cout << "array.back() = " << c.back() << endl;  //最后一个array容器中的数值
	cout << "array.data() = " << c.data() << endl; //array容器的地址
	long target = get_a_target_long();
	timeStart = clock();
  //程序中使用c语言的排序方法qsort()和查找bsearch()，在查找前必须先排序
	::qsort(c.data(), ASIZE, sizeof(long), compareLongs);  //c排序方法
	long* pItem = (long*)::bsearch(&target, c.data(), ASIZE, sizeof(long), compareLongs); //c查找的方法
	cout << "qsort() + bsearch(), milli-seconds: " << (clock() - timeStart) << endl;
	if (pItem != NULL)
		cout << "found, " << *pItem << endl;
	else
		cout << "not found!" << endl;
	return 0;
}
/*输出：
	test_array()......................
	front: 5283
	milli-seconds: 16
	array.size() = 250000
	array.front() =  5283
	array.back() = 9689
	array.data() = 002CB6B0
	target (0~32767): 1200
	qsort() + bsearch(), milli-seconds: 187
	found, 1200
*/
```
