# 光速入门 C++

*文章来自 Cherno C++ 视频教程+网络搜索*

## enum 枚举

**枚举类型的定义：**枚举类型(enumeration)是 C++ 中的一种派生数据类型，它是由用户定义的若干枚举常量的集合。

定义格式：枚举类型的定义格式为：

```cpp
enum <类型名> {<枚举常量表>};
```


**应用举例：**

```cpp
enum color_set1 {RED, BLUE, WHITE, BLACK}; // 定义枚举类型color_set1
enum week {Sun, Mon, Tue, Wed, Thu, Fri, Sat}; // 定义枚举类型week
```

**enum class** 是C++11之后出来的新特性，然而使用的人不多。enum 在这之后称为不限定范围的枚举，enum class称之为限定范围的枚举。就这范围的事情使用方式就大相径庭。

```cpp
enum MyEnum
{
    ME_FIRST,
    ME_SECOND
}
enum MyEnum2
{
    ME_FIRST, ///错误 ,  不限定范围的enum不允许这么做
}
```

```cpp
enum class MyEnum
{
    ME_FIRST,
    ME_SECOND
}

enum class MyEnum2
{
    ME_FIRST,
    ME_SECOND /// 编译通过
}
```

```c++
enum fruit_set {apple, orange, banana=1, peach, grape}
//枚举常量apple=0,orange=1, banana=1,peach=2,grape=3。
enum week {Sun=7, Mon=1, Tue, Wed, Thu, Fri, Sat};
//枚举常量Sun,Mon,Tue,Wed,Thu,Fri,Sat的值分别为7、1、2、3、4、5、6。
```

自定义枚举的数据类型

```cpp
enum whatever : char
{
    A, B, C
};
```

## & 引用

引用变量是一个别名，也就是说，它是某个已存在变量的另一个名字。一旦把引用初始化为某个变量，就可以使用该引用名称或变量名称来指向变量。

引用很容易与指针混淆，它们之间有三个主要的不同：

- 不存在空引用。引用必须连接到一块合法的内存。
- **一旦引用被初始化为一个对象，就不能被指向到另一个对象**。指针可以在任何时候指向到另一个对象。
- 引用必须在创建时被初始化。指针可以在任何时间被初始化。

在变量类型后加&表示按引用传参

```cpp
int GetValue(CustomObj& obj) 
{
    return obj.whatever();
};
```

```cpp
void swap(int& x, int& y)
{
   int temp;
   temp = x; /* 保存地址 x 的值 */
   x = y;    /* 把 y 赋值给 x */
   y = temp; /* 把 x 赋值给 y  */
  
   return;
}
 
int main ()
{
   // 局部变量声明
   int a = 100;
   int b = 200;
 
   cout << "交换前，a 的值：" << a << endl;
   cout << "交换前，b 的值：" << b << endl;
 
   /* 调用函数来交换值 */
   swap(a, b);
 
   cout << "交换后，a 的值：" << a << endl;
   cout << "交换后，b 的值：" << b << endl;
 
   return 0;
}
```

## 指针数组

可能有一种情况，我们想要让数组存储指向 int 或 char 或其他数据类型的指针。下面是一个指向整数的指针数组的声明：

```
int *ptr[MAX];
```

在这里，把 **ptr** 声明为一个数组，由 MAX 个整数指针组成。因此，ptr 中的每个元素，都是一个指向 int 值的指针。下面的实例用到了三个整数，它们将存储在一个指针数组中，如下所示：

```cpp
int  var[MAX] = {10, 100, 200};
int *ptr[MAX];

for (int i = 0; i < MAX; i++)
{
    ptr[i] = &var[i]; // 赋值为整数的地址
}
for (int i = 0; i < MAX; i++)
{
    cout << "Value of var[" << i << "] = ";
    cout << *ptr[i] << endl;
}
return 0;
```

当上面的代码被编译和执行时，它会产生下列结果：

```
Value of var[0] = 10
Value of var[1] = 100
Value of var[2] = 200
```

## class 类和对象

类定义是以关键字 **class** 开头，后跟类的名称。类的主体是包含在一对花括号中。类定义后必须跟着一个分号或一个声明列表。

```cpp
class Box
{
   public:
      double length;   // 盒子的长度
      double breadth;  // 盒子的宽度
      double height;   // 盒子的高度
};
```

类中的成员默认都是private，结构体中默认都是public。

结构体在cpp中存在的意义是向前兼容c

```cpp
Box Box1;          // 声明 Box1，类型为 Box
Box Box2;          // 声明 Box2，类型为 Box
```

## friend 友元

类的友元函数是定义在类外部，但有权访问类的所有私有（private）成员和保护（protected）成员。尽管友元函数的原型有在类的定义中出现过，但是友元函数并不是成员函数。

友元可以是一个函数，该函数被称为友元函数；友元也可以是一个类，该类被称为友元类，在这种情况下，整个类及其所有成员都是友元。

如果要声明函数为一个类的友元，需要在类定义中该函数原型前使用关键字 **friend**，如下所示：

```c++
class Box
{
   double width;
public:
   double length;
   friend void printWidth( Box box );
   void setWidth( double wid );
};
```

## virtual 虚函数

```c++
class Base
{
    public:
    virtual void f(){cout<<"Base::f"<<endl;}
    virtual void g(){cout<<"Base::g"<<endl;}
    virtual void h(){cout<<"Base::h"<<endl;}
};
```

继承类

```c++
class Derived:public Base
{
	public:
    virtual void f(){cout<<"Derived::f"<<endl;}
    virtual void g1(){cout<<"Derived::g1"<<endl;}
    virtual void h1(){cout<<"Derived::h1"<<endl;}
}
```

虚函数确保调用子类方法时不会意外调用父类的方法。使用 `virtual void funcA() override; ` 来让编译器进行**静态检查**，确保 override 的方法在父类中已经实现。

## 纯虚函数（接口）

C++中没有interface，接口就是一个包含一个or多个纯虚函数的类

强制要求子类实现父类的方法

```cpp
// 仍然需要 virtual
// =0 表示必须在子类中 override
// 该类不能够实例化
public:
virtual std::string GetName() = 0;
```

<font color="red" style="font-size:30px">下面是大名鼎鼎的 STL 教程！</font>

**STL中六大组件**：

容器（Container），是一种数据结构，如list，vector，和deques ，以模板类的方法提供。为了访问容器中的数据，可以使用由容器类输出的迭代器；

迭代器（Iterator），提供了访问容器中对象的方法。例如，可以使用一对迭代器指定list或vector中的一定范围的对象。迭代器就如同一个指针。事实上，C++的指针也是一种迭代器。但是，迭代器也可以是那些定义了operator*()以及其他类似于指针的操作符地方法的类对象；

算法（Algorithm），是用来操作容器中的数据的模板函数。例如，STL用sort()来对一个vector中的数据进行排序，用find()来搜索一个list中的对象，函数本身与他们操作的数据的结构和类型无关，因此他们可以在从简单数组到高度复杂容器的任何数据结构上使用；

仿函数（Functor）

适配器（Adaptor）

<algorithm>是所有STL头文件中最大的一个（尽管它很好理解），它是由一大堆模版函数组成的，可以认为每个函数在很大程度上都是独立的，其中常用到的功能范围涉及到比较、交换、查找、遍历操作、复制、修改、移除、反转、排序、合并等等。

<numeric>体积很小，只包括几个在序列上面进行简单数学运算的模板函数，包括加法和乘法在序列上的一些操作。

<functional>中则定义了一些模板类，用以声明函数对象。

## std::string

字符串相加：

```cpp
std::string name = std::string("test") + "fsdfd";
// or, in C++11
using namespace std::string_literals;
// s 是一个函数，返回标准字符串对象
std::string name = "Cherno"s + "Hello";

std::u32string name = U"Cherno"s + U".....";
```

原始字符串

```c++
const char* example = R"..........";

const char* example = R".........
    line2
    line3
    line4
    ";
```

## std::tuple

```c++
#include <iostream>
#include <tuple>

static std::tuple<std::string, int> GetTuple()
{
	return std::make_tuple("Hello", 42);
}

int main()
{ 
	std::tuple<std::string, int> t = GetTuple();
    std::get<0>(t) = "World";
}
```

## std::array

```c++
#include <array>

// an array with 5 ints
std::array<int, 5> data;
data[0] = 2;
// ask the size of it
data.size();
// if you want to get the size in a function, consider template.
// std::array has bound checkings.
```

> you should use this std::array **anywhere**, because it has **bound checks** and other...


## std::sort

`std::sort` 复杂度是 `Nlog(N)`

```c++
#include <iostream>
#include <vector>
#include <algorithm>

int main()
{
	std::vector<int> v = { 4,6,2,8,4,7,8,3,1,46,12,68 };
    // lambda函数决定 a 和 b 中的哪一个要排在前面
    // true a在b前
	std::sort(v.begin(), v.end(), [](int a, int b) { return a > b; });

	for (int a : v)
	{
		std::cout << a << std::endl;
	}
	std::cin.get();
}
```

或者用 `std::greater<int>()`

```c++
#include <functional>
std::vector<int> v = { 4,6,2,8,4,7,8,3,1,46,12,68 };
std::sort(v.begin(), v.end(), std::greater<int>());
```

## std::optional

```c++
#include <fstream>
#include <optional>

std::optional<std::string> ReadFile(const std::string& filePath)
{
	std::ifstream stream(filePath);
	if (!stream)
	{
		return {};
	}
	return "OK!";
}

int main()
{
	auto data = ReadFile("data.txt");
	if (data)
	{
		// do your things...
        // these can get the string
		std::string& value1 = *data;
		std::string& value2 = data.value();
	}
	// or
	if (data.has_value())
	{
		// ...
	}
	std::cin.get();
}
```


<font color="red" style="font-size:30px">下面是很难理解的内存管理！</font>

## 对象创建(堆or栈)

我们的类中有很多成员，它们需要存储在某地方

应用程序，会将内存主要分为两部分：栈和堆

栈有自动的生存期，他们的生存期实际上是由它声明的地方作用域决定的，变量超出作用域即释放内存，栈弹出。

一旦在堆中分配一个对象，实际上你已经在堆上创建了一个对象，又用户决定其生存周期

Allocate on stack

```c++
using String = std::string;


class Entity
{
private:
	String m_Name;
public:
	Entity() :m_Name("Default name") {}
	Entity(const String& name) :m_Name(name) {}
	
	const String& GetName() const { return m_Name; }
};

// call

// on stack
// 这是C++中最快的方法也是可以“管控”的方法，去初始化对象。
// call default constructor
Entity entity;
// or
Entity entity1("Cherno");
// or
Entity entity2 = Entity("Cherno");
entity.GetName();
// do the above everywhere if you can!
```

关于stack frame

```cpp
void Func()
{
	// 创建栈，包含了所有声明的局部变量，和对象，
	// 函数结束时，stack frame will be destructed.
	int a = 2;
	Entity e = Entity("3214");
}

Entity* e;
{
    Entity entity("Cherno");
    e = &entity;
}
// `entity` is gone.
```

stack is usually small, typically 1MB or 2MB.

Allocate on heap

```c++
Entity entity;

// on heap
// use the new keyword
// when call new, allocate mem on heap, 
// return the mem address to eneity
Entity* entity = new Entity("Cherno");
```

>  但是简单来说，就是性能问题，在堆上分配要比栈花费更长的时间，而且在堆上分配的话,需要手动释放内存。

```c++
Entity* entity = new Entity("Cherno");
// we need to release mem manually
delete entity;
```

Choosing between the two:

If the object is too big, or explicitly control the lifespan of the object, use heap.

On stack is faster.

## new 关键字

The new keyword is pretty deep.

> 你为什么要写C++？除非你特别需要**性能**或者你要**掌控一切**。
>
> Cherno

The main purpose of `new` is to allocate memory on heap.

When you call new, it takes time.

`new` basically **find a big memory block** and allocate it.

## 智能指针

:所以要访问所有这些智能指针你首先要做的是包括memory头文件

no `new` needed when using smart ptrs.

it will call `new` and memory will be released automatically.

**unique_ptr**: unique_ptr是作用域指针，是超出作用域时，它会被销毁然后调用delete

>  你不能复制一个unique_ptr，因为如果你复制一个unique_ptr，你会有两个指针，两个unique_ptr指向同一个内存块，如果一个死了，那块内存将被释放。也就是说，你指向同一块内存的第二个unique_ptr指向了已经被释放的内存

```c++
class Entity
{
public:
	Entity()
	{
		std::cout << "Created" << std::endl;
	}

	~Entity()
	{
		std::cout << "Destroyed" << std::endl;
	}
};

int main()
{
	{
		std::unique_ptr<Entity> entity(new Entity());
		// entity->DoSome();
	}
	End();
}
```

a better way

```c++
int main()
{
	{
		// a better way, for exception safety
		std::unique_ptr<Entity> entity = std::make_unique<Entity>();
		// entity->DoSome();
	}
	End();
}
```

**shared_ptr**

> shared_ptr实现的方式实际上取决于编译器和你在编译器中使用的标准库，大多数使用引用计数。

```cpp
std::shared_ptr<Entity> shared = std::make_shared<Entity>();
```

**weak_ptr**

```c++
// do not increase refrence count
std::weak_ptr<Entity> weak = shared;
```

`weak_pty` may point to an invalid object.