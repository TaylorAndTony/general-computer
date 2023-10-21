# C++ STL 光速入门

*全文来自[知乎](https://zhuanlan.zhihu.com/p/582795495)*

## 算法合集

### 查找算法

adjacent_find: 在iterator对标识元素范围内，查找一对相邻重复元素，找到则返回指向这对元素的第一个元素的 ForwardIterator。否则返回last。重载版本使用输入的二元操作符代替相等的判断。

binary_search: 在有序序列中查找value，找到返回true。重载的版本实用指定的比较函数对象或函数指针来判断相等。

count: 利用等于操作符，把标志范围内的元素与输入值比较，返回相等元素个数。

count_if: 利用输入的操作符，对标志范围内的元素进行操作，返回结果为true的个数。

equal_range: 功能类似equal，返回一对iterator，第一个表示lower_bound，第二个表示upper_bound。

find: 利用底层元素的等于操作符，对指定范围内的元素与输入值进行比较。当匹配时，结束搜索，返回该元素的 一个InputIterator。

find_end: 在指定范围内查找"由输入的另外一对iterator标志的第二个序列"的最后一次出现。找到则返回最后一对的第一 个ForwardIterator，否则返回输入的"另外一对"的第一个ForwardIterator。重载版本使用用户输入的操作符代 替等于操作。

find_first_of: 在指定范围内查找"由输入的另外一对iterator标志的第二个序列"中任意一个元素的第一次出现。重载版本中使 用了用户自定义操作符。

find_if: 使用输入的函数代替等于操作符执行find。

lower_bound: 返回一个ForwardIterator，指向在有序序列范围内的可以插入指定值而不破坏容器顺序的第一个位置。重载函 数使用自定义比较操作。

upper_bound: 返回一个ForwardIterator，指向在有序序列范围内插入value而不破坏容器顺序的最后一个位置，该位置标志 一个大于value的值。重载函数使用自定义比较操作。

search: 给出两个范围，返回一个ForwardIterator，查找成功指向第一个范围内第一次出现子序列(第二个范围)的位 置，查找失败指向last1。重载版本使用自定义的比较操作。

search_n: 在指定范围内查找val出现n次的子序列。重载版本使用自定义的比较操作。

### 排序算法

inplace_merge: 合并两个有序序列，结果序列覆盖两端范围。重载版本使用输入的操作进行排序。

merge: 合并两个有序序列，存放到另一个序列。重载版本使用自定义的比较。

nth_element: 将范围内的序列重新排序，使所有小于第n个元素的元素都出现在它前面，而大于它的都出现在后面。重 载版本使用自定义的比较操作。

partial_sort: 对序列做部分排序，被排序元素个数正好可以被放到范围内。重载版本使用自定义的比较操作。

partial_sort_copy: 与partial_sort类似，不过将经过排序的序列复制到另一个容器。

partition: 对指定范围内元素重新排序，使用输入的函数，把结果为true的元素放在结果为false的元素之前。

random_shuffle: 对指定范围内的元素随机调整次序。重载版本输入一个随机数产生操作。

reverse: 将指定范围内元素重新反序排序。

reverse_copy: 与reverse类似，不过将结果写入另一个容器。

rotate: 将指定范围内元素移到容器末尾，由middle指向的元素成为容器第一个元素。

rotate_copy: 与rotate类似，不过将结果写入另一个容器。

sort: 以升序重新排列指定范围内的元素。重载版本使用自定义的比较操作。

stable_sort: 与sort类似，不过保留相等元素之间的顺序关系。

stable_partition: 与partition类似，不过不保证保留容器中的相对顺序。

### 删除和替换算法

copy: 复制序列

copy_backward: 与copy相同，不过元素是以相反顺序被拷贝。

iter_swap: 交换两个ForwardIterator的值。

remove: 删除指定范围内所有等于指定元素的元素。注意，该函数不是真正删除函数。内置函数不适合使用remove和 remove_if函数。

remove_copy: 将所有不匹配元素复制到一个制定容器，返回OutputIterator指向被拷贝的末元素的下一个位置。

remove_if: 删除指定范围内输入操作结果为true的所有元素。

remove_copy_if: 将所有不匹配元素拷贝到一个指定容器。

replace: 将指定范围内所有等于vold的元素都用vnew代替。

replace_copy: 与replace类似，不过将结果写入另一个容器。

replace_if: 将指定范围内所有操作结果为true的元素用新值代替。

replace_copy_if: 与replace_if，不过将结果写入另一个容器。

swap: 交换存储在两个对象中的值。

swap_range: 将指定范围内的元素与另一个序列元素值进行交换。

unique: 清除序列中重复元素，和remove类似，它也不能真正删除元素。重载版本使用自定义比较操作。

unique_copy: 与unique类似，不过把结果输出到另一个容器。

### 排列组合算法

next_permutation: 取出当前范围内的排列，并重新排序为下一个排列。重载版本使用自定义的比较操作。

prev_permutation: 取出指定范围内的序列并将它重新排序为上一个序列。如果不存在上一个序列则返回false。重载版本使用 自定义的比较操作。

### 算术算法

accumulate: iterator对标识的序列段元素之和，加到一个由val指定的初始值上。重载版本不再做加法，而是传进来的 二元操作符被应用到元素上。

partial_sum: 创建一个新序列，其中每个元素值代表指定范围内该位置前所有元素之和。重载版本使用自定义操作代 替加法。

inner_product: 对两个序列做内积(对应元素相乘，再求和)并将内积加到一个输入的初始值上。重载版本使用用户定义 的操作。

adjacent_difference: 创建一个新序列，新序列中每个新值代表当前元素与上一个元素的差。重载版本用指定二元操作计算相 邻元素的差。

### 生成算法

fill: 将输入值赋给标志范围内的所有元素。

fill_n: 将输入值赋给first到first+n范围内的所有元素。

for_each: 用指定函数依次对指定范围内所有元素进行迭代访问，返回所指定的函数类型。该函数不得修改序列中的元素。

generate: 连续调用输入的函数来填充指定的范围。

generate_n: 与generate函数类似，填充从指定iterator开始的n个元素。

transform: 将输入的操作作用与指定范围内的每个元素，并产生一个新的序列。重载版本将操作作用在一对元素上，另外一 个元素来自输入的另外一个序列。结果输出到指定容器。

### 关系算法

equal: 如果两个序列在标志范围内元素都相等，返回true。重载版本使用输入的操作符代替默认的等于操 作符。

includes: 判断第一个指定范围内的所有元素是否都被第二个范围包含，使用底层元素的<操作符，成功返回 true。重载版本使用用户输入的函数。

lexicographical_compare: 比较两个序列。重载版本使用用户自定义比较操作。

max: 返回两个元素中较大一个。重载版本使用自定义比较操作。

max_element: 返回一个ForwardIterator，指出序列中最大的元素。重载版本使用自定义比较操作。

min: 返回两个元素中较小一个。重载版本使用自定义比较操作。

min_element: 返回一个ForwardIterator，指出序列中最小的元素。重载版本使用自定义比较操作。

mismatch: 并行比较两个序列，指出第一个不匹配的位置，返回一对iterator，标志第一个不匹配元素位置。 如果都匹配，返回每个容器的last。重载版本使用自定义的比较操作。

### 集合算法

set_union: 构造一个有序序列，包含两个序列中所有的不重复元素。重载版本使用自定义的比较操作。

set_intersection: 构造一个有序序列，其中元素在两个序列中都存在。重载版本使用自定义的比较操作。

set_difference: 构造一个有序序列，该序列仅保留第一个序列中存在的而第二个中不存在的元素。重载版本使用 自定义的比较操作。

set_symmetric_difference: 构造一个有序序列，该序列取两个序列的对称差集(并集-交集)。

### 堆算法

make_heap: 把指定范围内的元素生成一个堆。重载版本使用自定义比较操作。

pop_heap: 并不真正把最大元素从堆中弹出，而是重新排序堆。它把first和last-1交换，然后重新生成一个堆。可使用容器的 back来访问被"弹出"的元素或者使用pop_back进行真正的删除。重载版本使用自定义的比较操作。

push_heap: 假设first到last-1是一个有效堆，要被加入到堆的元素存放在位置last-1，重新生成堆。在指向该函数前，必须先把 元素插入容器后。重载版本使用指定的比较操作。

sort_heap: 对指定范围内的序列重新排序，它假设该序列是个有序堆。重载版本使用自定义比较操作。

## 仿函数

仿函数(functor)，就是使一个类的使用看上去象一个函数。**其实现就是类中实现一个operator()**，这个类就有了类似函数的行为，就是一个仿函数类了。

有些功能的的代码，会在不同的成员函数中用到，想复用这些代码。

1）公共的函数，可以，这是一个解决方法，不过函数用到的一些变量，就可能成为公共的全局变量，再说为了复用这么一片代码，就要单立出一个函数，也不是很好维护。

2）仿函数，写一个简单类，除了那些维护一个类的成员函数外，就只是实现一个operator()，在类实例化时，就将要用的，非参数的元素传入类中。

要使用STL内建的仿函数，必须包含`<functional>`头文件。而头文件中包含的仿函数分类包括

算术类仿函数

加：`plus<T>`

减：`minus<T>`

乘：`multiplies<T>`

除：`divides<T>`

模取：`modulus<T>`

否定：`negate<T>`

```cpp
#include <iostream>
#include <numeric>
#include <vector> 
#include <functional> 
using namespace std;
 
int main()
{
	int ia[] = { 1,2,3,4,5 };
	vector<int> iv(ia, ia + 5);
	//120
	cout << accumulate(iv.begin(), iv.end(), 1, multiplies<int>()) << endl;
	//15
	cout << multiplies<int>()(3, 5) << endl;
 
	modulus<int>  modulusObj;
	cout << modulusObj(3, 5) << endl; // 3 
	system("pause");
	return 0;
}
```

## 常用容器

### vector

1.构造函数

vector():创建一个空vector

vector(int nSize):创建一个vector,元素个数为nSize

vector(int nSize,const t& t):创建一个vector，元素个数为nSize,且值均为t

vector(const vector&):复制构造函数

vector(begin,end):复制`[begin,end)`区间内另一个数组的元素到vector中

2.增加函数

void push_back(const T& x):向量尾部增加一个元素X

iterator insert(iterator it,const T& x):向量中迭代器指向元素前增加一个元素x

iterator insert(iterator it,int n,const T& x):向量中迭代器指向元素前增加n个相同的元素x

iterator insert(iterator it,const_iterator first,const_iterator last):向量中迭代器指向元素前
插入另一个相同类型向量的`[first,last)`间的数据

3.删除函数

iterator erase(iterator it):删除向量中迭代器指向元素

iterator erase(iterator first,iterator last):删除向量中`[first,last)`中元素

void pop_back():删除向量中最后一个元素

void clear():清空向量中所有元素

4.遍历函数

reference at(int pos):返回pos位置元素的引用

reference front():返回首元素的引用

reference back():返回尾元素的引用

iterator begin():返回向量头指针，指向第一个元素

iterator end():返回向量尾指针，指向向量最后一个元素的下一个位置

reverse_iterator rbegin():反向迭代器，指向最后一个元素

reverse_iterator rend():反向迭代器，指向第一个元素之前的位置

5.判断函数

bool empty() const:判断向量是否为空，若为空，则向量中无元素
6.大小函数


int size() const:返回向量中元素的个数

int capacity() const:返回当前向量张红所能容纳的最大元素值

int max_size() const:返回最大可允许的vector元素数量值

7.其他函数


void swap(vector&):交换两个同类型向量的数据

void assign(int n,const T& x):设置向量中第n个元素的值为x

void assign(const_iterator first,const_iterator last):向量中`[first,last)`中元素设置成当前向量元素

8.看着清楚

1.push_back 在数组的最后添加一个数据

2.pop_back 去掉数组的最后一个数据

.at-Domain Parked 得到编号位置的数据

4.begin 得到数组头的指针

5.end 得到数组的最后一个单元+1的指针

6．front 得到数组头的引用

7.back 得到数组的最后一个单元的引用

8.max_size 得到vector最大可以是多大

9.capacity 当前vector分配的大小

10.size 当前使用数据的大小

11.resize 改变当前使用数据的大小，如果它比当前使用的大，者填充默认值

12.reserve 改变当前vecotr所分配空间的大小

13.erase 删除指针指向的数据项

14.clear 清空当前的vector

15.rbegin 将vector反转后的开始指针返回(其实就是原来的end-1)

16.rend 将vector反转构的结束指针返回(其实就是原来的begin-1)

17.empty 判断vector是否为空

18.swap 与另一个vector交换数据


### dequeue

所谓的deque是”double ended queue”的缩写，双端队列不论在尾部或头部插入元素，都十分迅速。而在中间插入元素则会比较费时，因为必须移动中间其他的元素。双端队列是一种随机访问的数据类型，提供了在序列两端快速插入和删除操作的功能，它可以在需要的时候改变自身大小，完成了标准的C++数据结构中队列的所有功能。

```cpp
#include<deque>  // 头文件
deque<type> deq;  // 声明一个元素类型为type的双端队列que
deque<type> deq(size);  // 声明一个类型为type、含有size个默认值初始化元素的的双端队列que
deque<type> deq(size, value);  // 声明一个元素类型为type、含有size个value元素的双端队列que
deque<type> deq(mydeque);  // deq是mydeque的一个副本
deque<type> deq(first, last);  // 使用迭代器first、last范围内的元素初始化deq
```

deq[ ]：用来访问双向队列中单个的元素。

deq.front()：返回第一个元素的引用。

deq.back()：返回最后一个元素的引用。

deq.push_front(x)：把元素x插入到双向队列的头部。

deq.pop_front()：弹出双向队列的第一个元素。

deq.push_back(x)：把元素x插入到双向队列的尾部。

deq.pop_back()：弹出双向队列的最后一个元素。

### list

List是stl实现的双向链表，与向量(vectors)相比, 它允许快速的插入和删除，但是随机访问却比较慢。使用时需要添加头文件

Lst1.assign() 给list赋值

Lst1.back() 返回最后一个元素

Lst1.begin() 返回指向第一个元素的迭代器

Lst1.clear() 删除所有元素

Lst1.empty() 如果list是空的则返回true

Lst1.end() 返回末尾的迭代器

Lst1.erase() 删除一个元素

Lst1.front() 返回第一个元素

Lst1.get_allocator() 返回list的配置器

Lst1.insert() 插入一个元素到list中

Lst1.max_size() 返回list能容纳的最大元素数量

Lst1.merge() 合并两个list

Lst1.pop_back() 删除最后一个元素

Lst1.pop_front() 删除第一个元素

Lst1.push_back() 在list的末尾添加一个元素

Lst1.push_front() 在list的头部添加一个元素

Lst1.rbegin() 返回指向第一个元素的逆向迭代器

Lst1.remove() 从list删除元素

Lst1.remove_if() 按指定条件删除元素

Lst1.rend() 指向list末尾的逆向迭代器

Lst1.resize() 改变list的大小

Lst1.reverse() 把list的元素倒转

Lst1.size() 返回list中的元素个数

Lst1.sort() 给list排序

Lst1.splice() 合并两个list

Lst1.swap() 交换两个list

Lst1.unique() 删除list中相邻重复的元素

### map/multimap

map和multimap都需要`#include<map>`，唯一的不同是，map的键值key不可重复，而multimap可以，也正是由于这种区别，map支持[ ]运算符，multimap不支持[ ]运算符。在用法上没什么区别。

C++中map提供的是一种键值对容器，里面的数据都是成对出现的,如下图：每一对中的第一个值称之为关键字(key)，每个关键字只能在map中出现一次；第二个称之为该关键字的对应值。

begin() 返回指向map头部的迭代器

clear(） 删除所有元素

count() 返回指定元素出现的次数

empty() 如果map为空则返回true

end() 返回指向map末尾的迭代器

equal_range() 返回特殊条目的迭代器对

erase() 删除一个元素

find() 查找一个元素

get_allocator() 返回map的配置器

insert() 插入元素

key_comp() 返回比较元素key的函数

lower_bound() 返回键值>=给定元素的第一个位置

max_size() 返回可以容纳的最大元素个数

rbegin() 返回一个指向map尾部的逆向迭代器

rend() 返回一个指向map头部的逆向迭代器

size() 返回map中元素的个数

swap() 交换两个map

upper_bound() 返回键值>给定元素的第一个位置

value_comp() 返回比较元素value的函数

```cpp
//头文件
#include<map>
 
map<int, string> ID_Name;
 
// 使用{}赋值是从c++11开始的，因此编译器版本过低时会报错，如visual studio 2012
map<int, string> ID_Name = {
                { 2015, "Jim" },
                { 2016, "Tom" },
                { 2017, "Bob" } };
```

### set

std::set 是关联容器，含有 Key 类型对象的已排序集。用比较函数compare进行排序。搜索、移除和插入拥有对数复杂度。 set 通常以红黑树实现。

set容器内的元素会被自动排序，set与map不同，set中的元素即是键值又是实值，set不允许两个元素有相同的键值。不能通过set的迭代器去修改set元素，原因是修改元素会破坏set组织。当对容器中的元素进行插入或者删除时，操作之前的所有迭代器在操作之后依然有效。

由于set元素是排好序的，且默认为升序，因此当set集合中的元素为结构体或自定义类时，该结构体或自定义类必须实现运算符‘<’的重载。

1. begin()--返回指向第一个元素的迭代器

2. clear()--清除所有元素

3. count()--返回某个值元素的个数

4. empty()--如果集合为空，返回true

5. end()--返回指向最后一个元素的迭代器

6. equal_range()--返回集合中与给定值相等的上下限的两个迭代器

7. erase()--删除集合中的元素

8. find()--返回一个指向被查找到元素的迭代器

9. get_allocator()--返回集合的分配器

10. insert()--在集合中插入元素

11. lower_bound()--返回指向大于（或等于）某值的第一个元素的迭代器

12. key_comp()--返回一个用于元素间值比较的函数

13. max_size()--返回集合能容纳的元素的最大限值

14. rbegin()--返回指向集合中最后一个元素的反向迭代器

15. rend()--返回指向集合中第一个元素的反向迭代器

16. size()--集合中元素的数目

17. swap()--交换两个集合变量

18. upper_bound()--返回大于某个值元素的迭代器

19. value_comp()--返回一个用于比较元素间的值的函数

### unordered_set

C++ 11中出现了两种新的关联容器:unordered_set和unordered_map，其内部实现与set和map大有不同，set和map内部实现是基于RB-Tree，而unordered_set和unordered_map内部实现是基于哈希表(hashtable)，由于unordered_set和unordered_map内部实现的公共接口大致相同，所以本文以unordered_set为例。

使用unordered_set需要包含`#include<unordered_set>`头文件，同unordered_map类似，用法没有什么太大的区别，参考set/multiset。

除此之外unordered_multiset也是一种可选的容器。