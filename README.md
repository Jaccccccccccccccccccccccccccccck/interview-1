<div align="center">
📖 Github
&emsp;&emsp; | &emsp;&emsp;
<a href="https://interview.huihut.com">📚 Docsify</a>
</div> 
<br>

<div align="center">
简体中文
&emsp;&emsp; | &emsp;&emsp;
<a href="https://github.com/huihut/interview/blob/master/README_en.md">English</a>
</div> 
<br>

<b><details><summary>💡 关于</summary></b>


📚 本仓库是面向 C/C++ 技术方向校招求职者、初学者的基础知识总结，包括语言、程序库、数据结构、算法、系统、网络、链接装载库等知识及面试经验、招聘、内推等信息。

💡 侧边目录支持方式：[📚 Docsify 文档](https://interview.huihut.com)、[Github + TOC 导航](https://github.com/jawil/GayHub)（[TOC预览.png](https://gitee.com/huihut/interview/raw/master/images/TOC预览.png)）

📄 保存为 PDF 方式：使用 Chrome 浏览器打开 <a href="https://interview.huihut.com">📚 Docsify 文档</a> 页面，缩起左侧目录-右键 - 打印 - 选择目标打印机是另存为PDF - 保存（[打印预览.png](https://gitee.com/huihut/interview/raw/master/images/打印预览.png)）

🙏 仓库内容如有错误或改进欢迎 issue 或 pr，建议或讨论可在 [#12](https://github.com/huihut/interview/issues/12) 提出。由于本人水平有限，仓库中的知识点有来自本人原创、读书笔记、书籍、博文等，非原创均已标明出处，如有遗漏，请 issue 提出。本仓库遵循 [CC BY-NC-SA 4.0（署名 - 非商业性使用 - 相同方式共享）](https://github.com/huihut/interview/blob/master/LICENSE) 协议，转载请注明出处，不得用于商业目的。

</details>

## 📑 目录

* [➕ C/C++](#cc)
* [📦 STL](#stl)
* [〽️ 数据结构](#data-structure)
* [⚡️ 算法](#algorithm)
* [❓ Problems](#problems)
* [💻 操作系统](#os)
* [☁️ 计算机网络](#computer-network)
* [🌩 网络编程](#network-programming)
* [💾 数据库](#database)
* [📏 设计模式](#design-pattern)
* [⚙️ 链接装载库](#link-loading-library)
* [📚 书籍](#books)
* [🔱 C/C++ 发展方向](#cc-development-direction)
* [💯 复习刷题网站](#review-of-brush-questions-website)
* [📝 面试题目经验](#interview-questions-experience)
* [📆 招聘时间岗位](#recruitment-time-post)
* [👍 内推](#recommend)
* [👬 贡献者](#contributor)
* [🍭 支持赞助](#support-sponsor)
* [📜 License](#license)



<a id="cc"></a>

## ➕ C/C++

### c++最大的特点
1.面向对象思想：OOP封装继承多态
2.标准模板库STL
3.泛型编程
4.异常处理
5.操作符重载

### C++11新特性

* 右值引用、移动语义
* 智能指针
* lambda表达式
* constexpr, const说明某个值是常量，不能被修改；constexpr是告知编译器当前变量和函数是编译时就可以确定的常量，可以用常量优化我
* 无序容器
* 有作用域的enum
* auto decltype nullptr
* 范围for语句

### lambda表达式 6个组成部分
#### 语法 [capture list](param list) mutable throw() -> return type {function} 
1. capture list：用于声明函数当前定义域需要使用到的外部变量
   1. [&] 表示全部使用引用传参
   2. [=] 全部使用引用传参
   3. [&, a] 除a外全部使用引用传参
   4. [=, &a] 除a外全部使用值传参
   5. [&a, b] a使用引用传参，b使用值传参
2. param list：定义函数的参数列表
3. mutable：用来修改值捕获时不能修改副本值的情况
4. exception: 抛出异常
5. return type：返回类型定义
6. lambda体

why:定义匿名函数，使代码更简洁

### mutable关键字
- mutable定义的类成员可以被const成员函数修改
- 在lambda表达式中的mutable关键字可以使引入外部变量值传参的修改

### C++异步
std::async用于创建异步任务，实际上就是创建一个线程异步执行相应任务，它接受回调（即函数或函数对象）作为参数。

std::async就是异步编程的高级封装，相当于封装了std::promise、std::packaged_task加上std::thread，基本上可以代替std::thread的所有事情。
* thread库用来创建线程，promise和packaged_task绑定用于函数返回的future对象，promise仅是一个对象，packaged_task是一个异步任务对象，由函数初始化；
* 语法 future<string> res = async(launch::async, func, args);

### const

#### 作用

1. 修饰变量，说明该变量不可以被改变；
2. 修饰指针，分为指向常量的指针（pointer to const）和自身是常量的指针（常量指针，const pointer）；
3. 修饰引用，指向常量的引用（reference to const），用于形参类型，即避免了拷贝，又避免了函数对值的修改；
4. 修饰成员函数，说明该成员函数内不能修改成员变量。

#### const 的指针与引用

* 指针
    * 指向常量的指针（pointer to const）
    * 自身是常量的指针（常量指针，const pointer）
* 引用
    * 指向常量的引用（reference to const）
    * 没有 const reference，因为引用只是对象的别名，引用不是对象，不能用 const 修饰

> （为了方便记忆可以想成）被 const 修饰（在 const 后面）的值不可改变，如下文使用例子中的 `p2`、`p3`

#### 使用

const 使用

```cpp
// 类
class A
{
private:
    const int a;                // 常对象成员，可以使用初始化列表或者类内初始化

public:
    // 构造函数
    A() : a(0) { };
    A(int x) : a(x) { };        // 初始化列表

    // const可用于对重载函数的区分
    int getValue();             // 普通成员函数
    int getValue() const;       // 常成员函数，不得修改类中的任何数据成员的值
};

void function()
{
    // 对象
    A b;                        // 普通对象，可以调用全部成员函数
    const A a;                  // 常对象，只能调用常成员函数
    const A *p = &a;            // 指针变量，指向常对象
    const A &q = a;             // 指向常对象的引用

    // 指针
    char greeting[] = "Hello";
    char* p1 = greeting;                // 指针变量，指向字符数组变量
    const char* p2 = greeting;          // 指针变量，指向字符数组常量（const 后面是 char，说明指向的字符（char）不可改变）
    char* const p3 = greeting;          // 自身是常量的指针，指向字符数组变量（const 后面是 p3，说明 p3 指针自身不可改变）
    const char* const p4 = greeting;    // 自身是常量的指针，指向字符数组常量
}

// 函数
void function1(const int Var);           // 传递过来的参数在函数内不可变
void function2(const char* Var);         // 参数指针所指内容为常量
void function3(char* const Var);         // 参数指针为常量
void function4(const int& Var);          // 引用参数在函数内为常量

// 函数返回值
const int function5();      // 返回一个常数
const int* function6();     // 返回一个指向常量的指针变量，使用：const int *p = function6();
int* const function7();     // 返回一个指向变量的常指针，使用：int* const p = function7();
```

#### 宏定义 #define 和 const 常量 

宏定义 #define|const 常量
---|---
宏定义，相当于字符替换|常量声明
预处理器处理|编译器处理
无类型安全检查|有类型安全检查
不分配内存|要分配内存
存储在代码段|存储在数据段
可通过 `#undef` 取消|不可取消

### static

#### 作用

1. 修饰普通变量，修改变量的存储区域和生命周期，使变量存储在静态区，在 main 函数运行前就分配了空间，如果有初始值就用初始值初始化它，如果没有初始值系统用默认值初始化它。
2. 修饰普通函数，表明函数的作用范围，仅在定义该函数的文件内才能使用。在多人开发项目时，为了防止与他人命名空间里的函数重名，可以将函数定位为 static。
3. 修饰成员变量，修饰成员变量使所有的对象只保存一个该变量，而且不需要生成对象就可以访问该成员。
4. 修饰成员函数，修饰成员函数使得不需要生成对象就可以访问该函数，但是在 static 函数内不能访问非静态成员。

### this 指针

1. `this` 指针是一个隐含于每一个非静态成员函数中的特殊指针。它指向调用该成员函数的那个对象。
2. 当对一个对象调用成员函数时，编译程序先将对象的地址赋给 `this` 指针，然后调用成员函数，每次成员函数存取数据成员时，都隐式使用 `this` 指针。
3. 当一个成员函数被调用时，自动向它传递一个隐含的参数，该参数是一个指向这个成员函数所在的对象的指针。
4. `this` 指针被隐含地声明为: `ClassName *const this`，这意味着不能给 `this` 指针赋值；在 `ClassName` 类的 `const` 成员函数中，`this` 指针的类型为：`const ClassName* const`，这说明不能对 `this` 指针所指向的这种对象是不可修改的（即不能对这种对象的数据成员进行赋值操作）；
5. `this` 并不是一个常规变量，而是个右值，所以不能取得 `this` 的地址（不能 `&this`）。
6. 在以下场景中，经常需要显式引用 `this` 指针：
    1. 为实现对象的链式引用；
    2. 为避免对同一对象进行赋值操作；
    3. 在实现一些数据结构时，如 `list`。

### inline 内联函数

#### 特征

* 相当于把内联函数里面的内容写在调用内联函数处；
* 相当于不用执行进入函数的步骤，直接执行函数体；
* 相当于宏，却比宏多了类型检查，真正具有函数特性；
* 编译器一般不内联包含循环、递归、switch 等复杂操作的内联函数；
* 在类声明中定义的函数，除了虚函数的其他函数都会自动隐式地当成内联函数。

#### 使用

inline 使用

```cpp
// 声明1（加 inline，建议使用）
inline int functionName(int first, int second,...);

// 声明2（不加 inline）
int functionName(int first, int second,...);

// 定义
inline int functionName(int first, int second,...) {/****/};

// 类内定义，隐式内联
class A {
    int doA() { return 0; }         // 隐式内联
}

// 类外定义，需要显式内联
class A {
    int doA();
}
inline int A::doA() { return 0; }   // 需要显式内联
```

#### 编译器对 inline 函数的处理步骤

1. 将 inline 函数体复制到 inline 函数调用点处； 
2. 为所用 inline 函数中的局部变量分配内存空间； 
3. 将 inline 函数的的输入参数和返回值映射到调用方法的局部变量空间中； 
4. 如果 inline 函数有多个返回点，将其转变为 inline 函数代码块末尾的分支（使用 GOTO）。

#### 优缺点

优点

1. 内联函数同宏函数一样将在被调用处进行代码展开，省去了参数压栈、栈帧开辟与回收，结果返回等，从而提高程序运行速度。
2. 内联函数相比宏函数来说，在代码展开时，会做安全检查或自动类型转换（同普通函数），而宏定义则不会。 
3. 在类中声明同时定义的成员函数，自动转化为内联函数，因此内联函数可以访问类的成员变量，宏定义则不能。
4. 内联函数在运行时可调试，而宏定义不可以。

缺点

1. 代码膨胀。内联是以代码膨胀（复制）为代价，消除函数调用带来的开销。如果执行函数体内代码的时间，相比于函数调用的开销较大，那么效率的收获会很少。另一方面，每一处内联函数的调用都要复制代码，将使程序的总代码量增大，消耗更多的内存空间。
2. inline 函数无法随着函数库升级而升级。inline函数的改变需要重新编译，不像 non-inline 可以直接链接。
3. 是否内联，程序员不可控。内联函数只是对编译器的建议，是否对函数内联，决定权在于编译器。

#### 虚函数（virtual）可以是内联函数（inline）吗？

> [Are "inline virtual" member functions ever actually "inlined"?](http://www.cs.technion.ac.il/users/yechiel/c++-faq/inline-virtuals.html)

* 虚函数可以是内联函数，内联是可以修饰虚函数的，但是当虚函数表现多态性的时候不能内联。
* 内联是在编译期建议编译器内联，而虚函数的多态性在运行期，编译器无法知道运行期调用哪个代码，因此虚函数表现为多态性时（运行期）不可以内联。
* `inline virtual` 唯一可以内联的时候是：编译器知道所调用的对象是哪个类（如 `Base::who()`），这只有在编译器具有实际对象而不是对象的指针或引用时才会发生。

虚函数内联使用

```cpp
#include <iostream>  
using namespace std;
class Base
{
public:
	inline virtual void who()
	{
		cout << "I am Base\n";
	}
	virtual ~Base() {}
};
class Derived : public Base
{
public:
	inline void who()  // 不写inline时隐式内联
	{
		cout << "I am Derived\n";
	}
};

int main()
{
	// 此处的虚函数 who()，是通过类（Base）的具体对象（b）来调用的，编译期间就能确定了，所以它可以是内联的，但最终是否内联取决于编译器。 
	Base b;
	b.who();

	// 此处的虚函数是通过指针调用的，呈现多态性，需要在运行时期间才能确定，所以不能为内联。  
	Base *ptr = new Derived();
	ptr->who();

	// 因为Base有虚析构函数（virtual ~Base() {}），所以 delete 时，会先调用派生类（Derived）析构函数，再调用基类（Base）析构函数，防止内存泄漏。
	delete ptr;
	ptr = nullptr;

	system("pause");
	return 0;
} 
```

### volatile

```cpp
volatile int i = 10; 
```

* volatile 关键字是一种类型修饰符，用它声明的类型变量表示可以被某些编译器未知的因素（操作系统、硬件、其它线程等）更改。所以使用 volatile 告诉编译器不应对这样的对象进行优化。
* volatile 关键字声明的变量，每次访问时都必须从内存中取出值（没有被 volatile 修饰的变量，可能由于编译器的优化，从 CPU 寄存器中取值）
* const 可以是 volatile （如只读的状态寄存器）
* 指针可以是 volatile

### assert()

断言，是宏，而非函数。assert 宏的原型定义在 `<assert.h>`（C）、`<cassert>`（C++）中，其作用是如果它的条件返回错误，则终止程序执行。可以通过定义 `NDEBUG` 来关闭 assert，但是需要在源代码的开头，`include <assert.h>` 之前。

assert() 使用

```cpp
#define NDEBUG          // 加上这行，则 assert 不可用
#include <assert.h>

assert( p != NULL );    // assert 不可用
```

### sizeof()

* sizeof 对数组，得到整个数组所占空间大小。
* sizeof 对指针，得到指针本身所占空间大小。


#### 数组 vs 指针
数组和指针关联紧密的原因是：编译器会把数组的行为转换成指针行为
- 区别
  - **概念上两者不同**，类型不同，相对应的赋值**操作**，取值操作都不一样
  - sizeof(指针)得到指针本身大小  sizeof(数组)得到数组整体大小
- 数组作为函数参数时，会退化为指向数组收个元素的地址的指针

### 引用 vs 指针
<!-- 引用和指针和引用 -->
指针从本质上讲就是存放变量地址的一个变量，在逻辑上是独立的，它可以被改变，包括其所指向的地址的改变和其指向的地址中所存放的数据的改变。
而引用是一个别名，它在逻辑上不是独立的，它的存在具有依附性，所以引用必须在一开始就被初始化，而且其引用的对象在其整个生命周期中是不能被改变的。
引用是C++提供的语法糖，在编译器看来引用其实是一个常量指针。
编译器来保证这样的一个常量指针保持引用的约束。
指针本身是一个数值，所以可以++,--等操作

### #pragma pack(n)

设定结构体、联合以及类成员变量以 n 字节方式对齐

#pragma pack(n) 使用

```cpp
#pragma pack(push)  // 保存对齐状态
#pragma pack(4)     // 设定为 4 字节对齐

struct test
{
    char m1;
    double m4;
    int m3;
};

#pragma pack(pop)   // 恢复对齐状态
```

#### 对齐
- 结构体内成员按照声明顺序存储，第一个成员地址和整个结构体地址相同。
- 未特殊说明时，**按结构体中size最大的成员对齐**（若有double成员，按8字节对齐。）
- 可以用alignas改变默认行为，**若alignas小于自然对齐的最小单位，则失效**

### 位域

```cpp
Bit mode: 2;    // mode 占 2 位
```

类可以将其（非静态）数据成员定义为位域（bit-field），在一个位域中含有一定数量的二进制位。当一个程序需要向其他程序或硬件设备传递二进制数据时，通常会用到位域。

* 位域在内存中的布局是与机器有关的
* 位域的类型必须是整型或枚举类型，带符号类型中的位域的行为将因具体实现而定
* 取地址运算符（&）不能作用于位域，任何指针都无法指向类的位域

### 声明和定义
- 为什么要区分两者：因为变量只能定义一次，而其他文件使用时不能定义，只能声明。
- 定义为变量分配存储空间
- 定义是声明

```
int a; // 定义也声明
/* 另外一个文件也需要使用a的时候，但不能直接使用，需要声明 */
extern int a; // 仅声明

/* 在一个文件中使用extern关键字，且进行了初始化，此时是定义 */
extern int a = 5; // 定义
```

### extern "C"

* 被 extern 限定的函数或变量是 extern 类型的
* 被 `extern "C"` 修饰的变量和函数是按照 C 语言方式编译和链接的

`extern "C"` 的作用是让 C++ 编译器将 `extern "C"` 声明的代码当作 C 语言代码处理，可以避免 C++ 因符号修饰导致代码不能和C语言库中的符号进行链接的问题。

extern "C" 使用

```cpp
#ifdef __cplusplus
extern "C" {
#endif

void *memset(void *, int, size_t);

#ifdef __cplusplus
}
#endif
```

### struct 和 typedef struct

#### C 中

```c
// c
typedef struct Student {
    int age; 
} S;
```

等价于

```c
// c
struct Student { 
    int age; 
};

typedef struct Student S;
```

此时 `S` 等价于 `struct Student`，但两个标识符名称空间不相同。

另外还可以定义与 `struct Student` 不冲突的 `void Student() {}`。

#### C++ 中

由于编译器定位符号的规则（搜索规则）改变，导致不同于C语言。

一、如果在类标识符空间定义了 `struct Student {...};`，使用 `Student me;` 时，编译器将搜索全局标识符表，`Student` 未找到，则在类标识符内搜索。

即表现为可以使用 `Student` 也可以使用 `struct Student`，如下：

```cpp
// cpp
struct Student { 
    int age; 
};

void f( Student me );       // 正确，"struct" 关键字可省略
```

二、若定义了与 `Student` 同名函数之后，则 `Student` 只代表函数，不代表结构体，如下：

```cpp
typedef struct Student { 
    int age; 
} S;

void Student() {}           // 正确，定义后 "Student" 只代表此函数

//void S() {}               // 错误，符号 "S" 已经被定义为一个 "struct Student" 的别名

int main() {
    Student(); 
    struct Student me;      // 或者 "S me";
    return 0;
}
```

### C++ 中 struct 和 class

总的来说，struct 更适合看成是一个数据结构的实现体，class 更适合看成是一个对象的实现体。

#### 区别

* 最本质的一个区别就是默认的访问控制
    1. 默认的继承访问权限。struct 是 public 的，class 是 private 的。  
    2. struct 作为数据结构的实现体，它默认的数据访问控制是 public 的，而 class 作为对象的实现体，它默认的成员变量访问控制是 private 的。

### union 联合

联合（union）是一种节省空间的特殊的类，一个 union 可以有多个数据成员，但是在任意时刻只有一个数据成员可以有值。当某个成员被赋值后其他成员变为未定义状态。联合有如下特点：

* 默认访问控制符为 public
* 可以含有构造函数、析构函数
* 不能含有引用类型的成员
* 不能继承自其他类，不能作为基类
* 不能含有虚函数
* 匿名 union 在定义所在作用域可直接访问 union 成员
* 匿名 union 不能包含 protected 成员或 private 成员
* 全局匿名联合必须是静态（static）的

union 使用

```cpp
#include<iostream>

union UnionTest {
    UnionTest() : i(10) {};
    int i;
    double d;
};

static union {
    int i;
    double d;
};

int main() {
    UnionTest u;

    union {
        int i;
        double d;
    };

    std::cout << u.i << std::endl;  // 输出 UnionTest 联合的 10

    ::i = 20;
    std::cout << ::i << std::endl;  // 输出全局静态匿名联合的 20

    i = 30;
    std::cout << i << std::endl;    // 输出局部匿名联合的 30

    return 0;
}
```

### C 实现 C++ 类

C 实现 C++ 的面向对象特性（封装、继承、多态）

* 封装：使用函数指针把属性与方法封装到结构体中
* 继承：结构体嵌套
* 多态：父类与子类方法的函数指针不同

> [Can you write object-oriented code in C? [closed]](https://stackoverflow.com/a/351745)

### explicit（显式）关键字

* explicit 修饰构造函数时，可以防止隐式转换和复制初始化
* explicit 修饰转换函数时，可以防止隐式转换，但 [按语境转换](https://zh.cppreference.com/w/cpp/language/implicit_conversion) 除外

explicit 使用

```cpp
struct A
{
	A(int) { }
	operator bool() const { return true; }
};

struct B
{
	explicit B(int) {}
	explicit operator bool() const { return true; }
};

void doA(A a) {}

void doB(B b) {}

int main()
{
	A a1(1);		// OK：直接初始化
	A a2 = 1;		// OK：复制初始化
	A a3{ 1 };		// OK：直接列表初始化
	A a4 = { 1 };		// OK：复制列表初始化
	A a5 = (A)1;		// OK：允许 static_cast 的显式转换 
	doA(1);			// OK：允许从 int 到 A 的隐式转换
	if (a1);		// OK：使用转换函数 A::operator bool() 的从 A 到 bool 的隐式转换
	bool a6(a1);		// OK：使用转换函数 A::operator bool() 的从 A 到 bool 的隐式转换
	bool a7 = a1;		// OK：使用转换函数 A::operator bool() 的从 A 到 bool 的隐式转换
	bool a8 = static_cast<bool>(a1);  // OK ：static_cast 进行直接初始化

	B b1(1);		// OK：直接初始化
	B b2 = 1;		// 错误：被 explicit 修饰构造函数的对象不可以复制初始化
	B b3{ 1 };		// OK：直接列表初始化
	B b4 = { 1 };		// 错误：被 explicit 修饰构造函数的对象不可以复制列表初始化
	B b5 = (B)1;		// OK：允许 static_cast 的显式转换
	doB(1);			// 错误：被 explicit 修饰构造函数的对象不可以从 int 到 B 的隐式转换
	if (b1);		// OK：被 explicit 修饰转换函数 B::operator bool() 的对象可以从 B 到 bool 的按语境转换
	bool b6(b1);		// OK：被 explicit 修饰转换函数 B::operator bool() 的对象可以从 B 到 bool 的按语境转换
	bool b7 = b1;		// 错误：被 explicit 修饰转换函数 B::operator bool() 的对象不可以隐式转换
	bool b8 = static_cast<bool>(b1);  // OK：static_cast 进行直接初始化

	return 0;
}
```

### friend 友元类和友元函数

* 能访问私有成员  
* 破坏封装性
* 友元关系不可传递
* 友元关系的单向性
* 友元声明的形式及数量不受限制

### using

#### using 声明

一条 `using 声明` 语句一次只引入命名空间的一个成员。它使得我们可以清楚知道程序中所引用的到底是哪个名字。如：

```cpp
using namespace_name::name;
```

#### 构造函数的 using 声明

在 C++11 中，派生类能够重用其直接基类定义的构造函数。

```cpp
class Derived : Base {
public:
    using Base::Base;
    /* ... */
};
```

如上 using 声明，对于基类的每个构造函数，编译器都生成一个与之对应（形参列表完全相同）的派生类构造函数。生成如下类型构造函数：

```cpp
Derived(parms) : Base(args) { }
```

#### using 指示

`using 指示` 使得某个特定命名空间中所有名字都可见，这样我们就无需再为它们添加任何前缀限定符了。如：

```cpp
using namespace_name name;
```

#### 尽量少使用 `using 指示` 污染命名空间

> 一般说来，使用 using 命令比使用 using 编译命令更安全，这是由于它**只导入了指定的名称**。如果该名称与局部名称发生冲突，编译器将**发出指示**。using编译命令导入所有的名称，包括可能并不需要的名称。如果与局部名称发生冲突，则**局部名称将覆盖名称空间版本**，而编译器**并不会发出警告**。另外，名称空间的开放性意味着名称空间的名称可能分散在多个地方，这使得难以准确知道添加了哪些名称。

using 使用

尽量少使用 `using 指示`

```cpp
using namespace std;
```

应该多使用 `using 声明`

```cpp
int x;
std::cin >> x ;
std::cout << x << std::endl;
```

或者

```cpp
using std::cin;
using std::cout;
using std::endl;
int x;
cin >> x;
cout << x << endl;
```

### :: 范围解析运算符

#### 分类

1. 全局作用域符（`::name`）：用于类型名称（类、类成员、成员函数、变量等）前，表示作用域为全局命名空间
2. 类作用域符（`class::name`）：用于表示指定类型的作用域范围是具体某个类的
3. 命名空间作用域符（`namespace::name`）:用于表示指定类型的作用域范围是具体某个命名空间的

:: 使用

```cpp
int count = 11;         // 全局（::）的 count

class A {
public:
	static int count;   // 类 A 的 count（A::count）
};
int A::count = 21;

void fun()
{
	int count = 31;     // 初始化局部的 count 为 31
	count = 32;         // 设置局部的 count 的值为 32
}

int main() {
	::count = 12;       // 测试 1：设置全局的 count 的值为 12

	A::count = 22;      // 测试 2：设置类 A 的 count 为 22

	fun();		        // 测试 3

	return 0;
}
```

### enum 枚举类型

#### 限定作用域的枚举类型

```cpp
enum class open_modes { input, output, append };
```

#### 不限定作用域的枚举类型

```cpp
enum color { red, yellow, green };
enum { floatPrec = 6, doublePrec = 10 };
```

### decltype

decltype 关键字用于检查实体的声明类型或表达式的类型及值分类。语法：

```cpp
decltype ( expression )
```

decltype 使用

```cpp
// 尾置返回允许我们在参数列表之后声明返回类型
template <typename It>
auto fcn(It beg, It end) -> decltype(*beg)
{
    // 处理序列
    return *beg;    // 返回序列中一个元素的引用
}
// 为了使用模板参数成员，必须用 typename
template <typename It>
auto fcn2(It beg, It end) -> typename remove_reference<decltype(*beg)>::type
{
    // 处理序列
    return *beg;    // 返回序列中一个元素的拷贝
}
```

### 引用

#### 左值引用

常规引用，一般表示对象的身份。

#### 右值引用

右值引用就是必须绑定到右值（一个临时对象、将要销毁的对象）的引用，一般表示对象的值。

右值引用可实现转移语义（Move Sementics）和精确传递（Perfect Forwarding），它的主要目的有两个方面：

* 消除两个对象交互时不必要的对象拷贝，节省运算存储资源，提高效率。
* 能够更简洁明确地定义泛型函数。

#### 引用折叠

* `X& &`、`X& &&`、`X&& &` 可折叠成 `X&`
* `X&& &&` 可折叠成 `X&&`

### 宏

* 宏定义可以实现类似于函数的功能，但是它终归不是函数，而宏定义中括弧中的“参数”也不是真的参数，在宏展开的时候对 “参数” 进行的是一对一的替换。

### 成员初始化列表（构造函数初始化列表）

好处

* 更高效：少了一次成员变量调用默认构造函数的过程。
* 有些场合必须要用初始化列表：
  1. 常量成员，因为常量只能初始化不能赋值，所以必须放在初始化列表里面
  2. 引用类型，引用必须在定义的时候初始化，并且不能重新赋值，所以也要写在初始化列表里面
  3. 类中成员变量没有默认构造函数，因为使用初始化列表可以不必调用默认构造函数来初始化

### initializer_list 列表初始化

用花括号初始化器列表初始化一个对象，其中对应构造函数接受一个 `std::initializer_list` 参数.

initializer_list 使用

```cpp
#include <iostream>
#include <vector>
#include <initializer_list>
 
template <class T>
struct S {
    std::vector<T> v;
    S(std::initializer_list<T> l) : v(l) {
         std::cout << "constructed with a " << l.size() << "-element list\n";
    }
    void append(std::initializer_list<T> l) {
        v.insert(v.end(), l.begin(), l.end());
    }
    std::pair<const T*, std::size_t> c_arr() const {
        return {&v[0], v.size()};  // 在 return 语句中复制列表初始化
                                   // 这不使用 std::initializer_list
    }
};
 
template <typename T>
void templated_fn(T) {}
 
int main()
{
    S<int> s = {1, 2, 3, 4, 5}; // 复制初始化
    s.append({6, 7, 8});      // 函数调用中的列表初始化
 
    std::cout << "The vector size is now " << s.c_arr().second << " ints:\n";
 
    for (auto n : s.v)
        std::cout << n << ' ';
    std::cout << '\n';
 
    std::cout << "Range-for over brace-init-list: \n";
 
    for (int x : {-1, -2, -3}) // auto 的规则令此带范围 for 工作
        std::cout << x << ' ';
    std::cout << '\n';
 
    auto al = {10, 11, 12};   // auto 的特殊规则
 
    std::cout << "The list bound to auto has size() = " << al.size() << '\n';
 
//    templated_fn({1, 2, 3}); // 编译错误！“ {1, 2, 3} ”不是表达式，
                             // 它无类型，故 T 无法推导
    templated_fn<std::initializer_list<int>>({1, 2, 3}); // OK
    templated_fn<std::vector<int>>({1, 2, 3});           // 也 OK
}
```

### 面向对象

面向对象程序设计（Object-oriented programming，OOP）是种具有对象概念的程序编程典范，同时也是一种程序开发的抽象方针。

![面向对象特征](https://gitee.com/huihut/interview/raw/master/images/面向对象基本特征.png)

面向对象三大特征 —— 封装、继承、多态

### 封装

把客观事物封装成抽象的类，并且类可以把自己的数据和方法只让可信的类或者对象操作，对不可信的进行信息隐藏。关键字：public, protected, private。不写默认为 private。

* `public` 成员：可以被任意实体访问
* `protected` 成员：只允许被子类及本类的成员函数访问
* `private` 成员：只允许被本类的成员函数、友元类或友元函数访问

### 继承

* 基类（父类）——&gt; 派生类（子类）

### 多态

* 多态，即多种状态（形态）。简单来说，我们可以将多态定义为消息以多种形式显示的能力。
* 多态是以封装和继承为基础的。
* C++ 多态分类及实现：
    1. 重载多态（Ad-hoc Polymorphism，编译期）：函数重载、运算符重载
    2. 子类型多态（Subtype Polymorphism，运行期）：虚函数
    3. 参数多态性（Parametric Polymorphism，编译期）：类模板、函数模板
    4. 强制多态（Coercion Polymorphism，编译期/运行期）：基本类型转换、自定义类型转换

> [The Four Polymorphisms in C++](https://catonmat.net/cpp-polymorphism)

### 类的大小
分为几个部分：
- 基类的大小
- 类中的普通成员变量大小
- 基类没有虚函数，而本类有虚函数，加一个指针大小
- 虚继承的情况，增加一个指针大小，本指针指向虚基类表

#### 静态多态（编译期/早绑定）

函数重载

```cpp
class A
{
public:
    void do(int a);
    void do(int a, int b);
};
```

#### 动态多态（运行期期/晚绑定）
* 虚函数：用 virtual 修饰成员函数，使其成为虚函数
* 动态绑定：当使用基类的引用或指针调用一个虚函数时将发生动态绑定

**注意：**

* 可以将派生类的对象赋值给基类的指针或引用，反之不可
* 普通函数（非类成员函数）不能是虚函数
* 静态函数（static）不能是虚函数
* 构造函数不能是虚函数（因为在调用构造函数时，虚表指针并没有在对象的内存空间中，必须要构造函数调用完成后才会形成虚表指针）
* 内联函数不能是表现多态性时的虚函数，解释见：[虚函数（virtual）可以是内联函数（inline）吗？](https://github.com/huihut/interview#%E8%99%9A%E5%87%BD%E6%95%B0virtual%E5%8F%AF%E4%BB%A5%E6%98%AF%E5%86%85%E8%81%94%E5%87%BD%E6%95%B0inline%E5%90%97)

动态多态使用

```cpp
class Shape                     // 形状类
{
public:
    virtual double calcArea()
    {
        ...
    }
    virtual ~Shape();
};
class Circle : public Shape     // 圆形类
{
public:
    virtual double calcArea();
    ...
};
class Rect : public Shape       // 矩形类
{
public:
    virtual double calcArea();
    ...
};
int main()
{
    Shape * shape1 = new Circle(4.0);
    Shape * shape2 = new Rect(5.0, 6.0);
    shape1->calcArea();         // 调用圆形类里面的方法
    shape2->calcArea();         // 调用矩形类里面的方法
    delete shape1;
    shape1 = nullptr;
    delete shape2;
    shape2 = nullptr;
    return 0;
}
```

### 虚析构函数

虚析构函数是为了解决基类的指针指向派生类对象，并用基类的指针删除派生类对象。

虚析构函数使用

```cpp
class Shape
{
public:
    Shape();                    // 构造函数不能是虚函数
    virtual double calcArea();
    virtual ~Shape();           // 虚析构函数
};
class Circle : public Shape     // 圆形类
{
public:
    virtual double calcArea();
    ...
};
int main()
{
    Shape * shape1 = new Circle(4.0);
    shape1->calcArea();    
    delete shape1;  // 因为Shape有虚析构函数，所以delete释放内存时，先调用子类析构函数，再调用基类析构函数，防止内存泄漏。
    shape1 = NULL;
    return 0；
}
```

### 纯虚函数

纯虚函数是一种特殊的虚函数，在基类中不能对虚函数给出有意义的实现，而把它声明为纯虚函数，它的实现留给该基类的派生类去做。

```cpp
virtual int A() = 0;
```

### 虚函数、纯虚函数

* 类里如果声明了虚函数，这个函数是实现的，哪怕是空实现，它的作用就是为了能让这个函数在它的子类里面可以被覆盖（override），这样的话，编译器就可以使用后期绑定来达到多态了。纯虚函数只是一个接口，是个函数的声明而已，它要留到子类里去实现。 
* 虚函数在子类里面可以不重写；但纯虚函数必须在子类实现才可以实例化子类。
* 虚函数的类用于 “实作继承”，继承接口的同时也继承了父类的实现。纯虚函数关注的是接口的统一性，实现由子类完成。 
* 带纯虚函数的类叫抽象类，这种类不能直接生成对象，而只有被继承，并重写其虚函数后，才能使用。抽象类被继承后，子类可以继续是抽象类，也可以是普通类。
* 虚基类是虚继承中的基类，具体见下文虚继承。

> [CSDN . C++ 中的虚函数、纯虚函数区别和联系](https://blog.csdn.net/u012260238/article/details/53610462)

### 虚函数指针、虚函数表

- 当类内定义了虚函数或集成了有虚函数的类时，类对象里就会存在一个虚函数指针，指向虚函数表
  - 虚函数表存在于只读数据段，存放着虚函数指针，每个类，而不是每个对象都会有一个虚函数表，如果派生类定义了基类的某个虚函数，则会修改对应虚函数表中的虚函数指针
- 在继承关系中，会把父类的虚函数表内容继承到派生类，复用父类虚函数表指针
- 在单继承关系中，如果子类重写了父类的虚函数，则虚函数表的对应虚函数指针项会被修改为子类的函数地址
- 如果在多继承关系中，会继承多个父类的虚函数指针，如果重写就覆盖，如果新增就把新增的虚函数指针添加到第一个有虚函数的类的虚函数表中。

> [C++中的虚函数(表)实现机制以及用C语言对其进行的模拟实现](https://blog.twofei.com/496/)

### 虚继承

虚继承用于解决多继承条件下的菱形继承问题（浪费存储空间、存在二义性）。
### 虚继承用来解决菱形继承问题
在继承的时候使用关键字virtual
class c : virtual public a, virtual public b {}
菱形继承会带了命名冲突和空间浪费问题，使用虚继承来解决两个问题
具体实现是在类对象中存储一个虚基类指针，虚基类指针指向虚基类表，虚基类表中存储着虚基类和本类的地址偏移量


底层实现原理与编译器相关，一般通过**虚基类指针**和**虚基类表**实现，每个虚继承的子类都有一个虚基类指针（占用一个指针的存储空间，4字节）和虚基类表（不占用类对象的存储空间）（需要强调的是，虚基类依旧会在子类里面存在拷贝，只是仅仅最多存在一份而已，并不是不在子类里面了）；当虚继承的子类被当做父类继承时，虚基类指针也会被继承。

实际上，vbptr 指的是虚基类表指针（virtual base table pointer），该指针指向了一个虚基类表（virtual table），虚表中记录了虚基类与本类的偏移地址；通过偏移地址，这样就找到了虚基类成员，而虚继承也不用像普通多继承那样维持着公共基类（虚基类）的两份同样的拷贝，节省了存储空间。

### 虚继承、虚函数

* 相同之处：都利用了虚指针（均占用类的存储空间）和虚表（均不占用类的存储空间）
* 不同之处：
    * 虚继承
        * 虚基类依旧存在继承类中，只占用存储空间
        * 虚基类表存储的是虚基类相对直接继承类的偏移
    * 虚函数
        * 虚函数不占用存储空间
        * 虚函数表存储的是虚函数地址

### 模板类、成员模板、虚函数

* 模板类中可以使用虚函数
* 一个类（无论是普通类还是类模板）的成员模板（本身是模板的成员函数）不能是虚函数

### 抽象类、接口类、聚合类

* 抽象类：含有纯虚函数的类
* 接口类：仅含有纯虚函数的抽象类
* 聚合类：用户可以直接访问其成员，并且具有特殊的初始化语法形式。**纯粹的数据类型**满足如下特点：
    * 所有成员都是 public
    * 没有定义任何构造函数
    * 没有类内初始化
    * 没有基类，也没有 virtual 函数

### 内存分配和管理

#### C++是静态、弱类型类型
静态与动态类型的区别是：编译时期是否确定变量的类型，能确定->静态；不能确定->动态
弱类型与强类型的区别是：不允许隐式类型转换的是强类型，允许隐式类型转换的是弱类型

C++在编译期间即可确定变量类型，so 静态类型
C++允许隐式的类型转换，so 弱类型类型

#### malloc、calloc、realloc、alloca

1. malloc：申请指定字节数的内存。申请到的内存中的初始值不确定。
2. calloc：为指定长度的对象，分配能容纳其指定个数的内存。申请到的内存的每一位（bit）都初始化为 0。
3. realloc：更改以前分配的内存长度（增加或减少）。当增加长度时，可能需将以前分配区的内容移到另一个足够大的区域，而新增区域内的初始值则不确定。
4. alloca：在栈上申请内存。程序在出栈的时候，会自动释放内存。但是需要注意的是，alloca 不具可移植性, 而且在没有传统堆栈的机器上很难实现。alloca 不宜使用在必须广泛移植的程序中。C99 中支持变长数组 (VLA)，可以用来替代 alloca。

#### malloc、free

用于分配、释放内存

malloc、free 使用

申请内存，确认是否申请成功

```cpp
char *str = (char*) malloc(100);
assert(str != nullptr);
```

释放内存后指针置空

```cpp
free(p); 
p = nullptr;
```

#### new、delete

1. new / new[]：完成两件事，先底层调用 malloc 分配了内存，然后调用构造函数（创建对象）。
2. delete/delete[]：也完成两件事，先调用析构函数（清理资源），然后底层调用 free 释放空间。
3. new 在申请内存时会自动计算所需字节数，而 malloc 则需我们自己输入申请内存空间的字节数。
**使用自定义类型的数组进行整体释放时必须使用delete[],否则只会释放数组的第一个**
new、delete 使用

申请内存，确认是否申请成功

```cpp
int main()
{
    T* t = new T();     // 先内存分配 ，再构造函数
    delete t;           // 先析构函数，再内存释放
    return 0;
}
```

#### 定位 new

定位 new（placement new）允许我们向 new 传递额外的地址参数，从而在预先指定的内存区域创建对象。

```cpp
new (place_address) type
new (place_address) type (initializers)
new (place_address) type [size]
new (place_address) type [size] { braced initializer list }
```

* `place_address` 是个指针
* `initializers` 提供一个（可能为空的）以逗号分隔的初始值列表

### delete this 合法吗？

> [Is it legal (and moral) for a member function to say delete this?](https://isocpp.org/wiki/faq/freestore-mgmt#delete-this)

合法，但：

1. 必须保证 this 对象是通过 `new`（不是 `new[]`、不是 placement new、不是栈上、不是全局、不是其他对象成员）分配的
2. 必须保证调用 `delete this` 的成员函数是最后一个调用 this 的成员函数
3. 必须保证成员函数的 `delete this ` 后面没有调用 this 了
4. 必须保证 `delete this` 后没有人使用了

### 如何定义一个只能在堆上（栈上）生成对象的类？

> [如何定义一个只能在堆上（栈上）生成对象的类?](https://www.nowcoder.com/questionTerminal/0a584aa13f804f3ea72b442a065a7618)

#### 只能在堆上

方法：将析构函数设置为私有

原因：C++ 是静态绑定语言，编译器管理栈上对象的生命周期，编译器在为类对象分配栈空间时，会先检查类的析构函数的访问性。若析构函数不可访问，则不能在栈上创建对象。

#### 只能在栈上

方法：将 new 和 delete 重载为私有

原因：在堆上生成对象，使用 new 关键词操作，其过程分为两阶段：第一阶段，使用 new 在堆上寻找可用内存，分配给对象；第二阶段，调用构造函数生成对象。将 new 操作设置为私有，那么第一阶段就无法完成，就不能够在堆上生成对象。

### 智能指针

#### C++ 标准库（STL）中

头文件：`#include <memory>`

#### C++ 98

```cpp
std::auto_ptr<std::string> ps (new std::string(str))；
```

#### C++ 11

1. shared_ptr
2. unique_ptr
3. weak_ptr
4. auto_ptr（被 C++11 弃用）

* Class shared_ptr 实现共享式拥有（shared ownership）概念。多个智能指针指向相同对象，该对象和其相关资源会在 “最后一个 reference 被销毁” 时被释放。为了在结构较复杂的情景中执行上述工作，标准库提供 weak_ptr、bad_weak_ptr 和 enable_shared_from_this 等辅助类。
* Class unique_ptr 实现独占式拥有（exclusive ownership）或严格拥有（strict ownership）概念，保证同一时间内只有一个智能指针可以指向该对象。你可以移交拥有权。它对于避免内存泄漏（resource leak）——如 new 后忘记 delete ——特别有用。

##### shared_ptr

多个智能指针可以共享同一个对象，对象的最末一个拥有着有责任销毁对象，并清理与该对象相关的所有资源。

* 支持定制型删除器（custom deleter），可防范 Cross-DLL 问题（对象在动态链接库（DLL）中被 new 创建，却在另一个 DLL 内被 delete 销毁）、自动解除互斥锁

##### weak_ptr

weak_ptr 允许你共享但不拥有某对象，一旦最末一个拥有该对象的智能指针失去了所有权，任何 weak_ptr 都会自动成空（empty）。因此，在 default 和 copy 构造函数之外，weak_ptr 只提供 “接受一个 shared_ptr” 的构造函数。

* 可打破环状引用（cycles of references，两个其实已经没有被使用的对象彼此互指，使之看似还在 “被使用” 的状态）的问题

##### unique_ptr

unique_ptr 是 C++11 才开始提供的类型，是一种在异常时可以帮助避免资源泄漏的智能指针。采用独占式拥有，意味着可以确保一个对象和其相应的资源同一时间只被一个 pointer 拥有。一旦拥有着被销毁或编程 empty，或开始拥有另一个对象，先前拥有的那个对象就会被销毁，其任何相应资源亦会被释放。

* unique_ptr 用于取代 auto_ptr

##### auto_ptr

被 c++11 弃用，原因是缺乏语言特性如 “针对构造和赋值” 的 `std::move` 语义，以及其他瑕疵。

##### auto_ptr 与 unique_ptr 比较

* auto_ptr 可以赋值拷贝，复制拷贝后所有权转移；unqiue_ptr 无拷贝赋值语义，但实现了`move` 语义；
* auto_ptr 对象不能管理数组（析构调用 `delete`），unique_ptr 可以管理数组（析构调用 `delete[]` ）；
  

#### 智能指针的实现
https://zhuanlan.zhihu.com/p/64543967

#### 智能指针线程安全吗
多个线程使用智能指针操作智能指针操作的对象是安全的，但对智能指针本身的操作不是线程安全的
* 同一个shared_ptr对象可以被多线程同时读取
* 不同的shared_ptr对象可以被多线程同时修改，即使这些shared_ptr对象管理着同一个对象的指针
* 如果多个线程同时读写同一个shared_ptr对象，那么需要加锁

### 强制类型转换运算符

> [MSDN . 强制转换运算符](https://msdn.microsoft.com/zh-CN/library/5f6c9f8h.aspx)

#### static_cast

* 用于非多态类型的转换
* 不执行运行时类型检查（转换安全性不如 dynamic_cast）
* 通常用于转换数值数据类型（如 float -> int）
* 可以在整个类层次结构中移动指针，子类转化为父类安全（向上转换），父类转化为子类不安全（因为子类可能有不在父类的字段或方法）

> 向上转换是一种隐式转换。

#### dynamic_cast

* 用于多态类型的转换
* 执行行运行时类型检查
* 只适用于指针或引用
* 对不明确的指针的转换将失败（返回 nullptr），但不引发异常
* 可以在整个类层次结构中移动指针，包括向上转换、向下转换

#### const_cast 

* 用于删除 const、volatile 和 __unaligned 特性（如将 const int 类型转换为 int 类型 ）

#### reinterpret_cast

* 用于位的简单重新解释
* 滥用 reinterpret_cast 运算符可能很容易带来风险。 除非所需转换本身是低级别的，否则应使用其他强制转换运算符之一。
* 允许将任何指针转换为任何其他指针类型（如 `char*` 到 `int*` 或 `One_class*` 到 `Unrelated_class*` 之类的转换，但其本身并不安全）
* 也允许将任何整数类型转换为任何指针类型以及反向转换。
* reinterpret_cast 运算符不能丢掉 const、volatile 或 __unaligned 特性。 
* reinterpret_cast 的一个实际用途是在哈希函数中，即，通过让两个不同的值几乎不以相同的索引结尾的方式将值映射到索引。

#### bad_cast

* 由于强制转换为引用类型失败，dynamic_cast 运算符引发 bad_cast 异常。

bad_cast 使用

```cpp
try {  
    Circle& ref_circle = dynamic_cast<Circle&>(ref_shape);   
}  
catch (bad_cast b) {  
    cout << "Caught: " << b.what();  
} 
```

### 运行时类型信息 (RTTI) 

#### dynamic_cast

* 用于多态类型的转换

#### typeid

* typeid 运算符允许在运行时确定对象的类型
* type\_id 返回一个 type\_info 对象的引用
* 如果想通过基类的指针获得派生类的数据类型，基类必须带有虚函数
* 只能获取对象的实际类型

#### type_info

* type_info 类描述编译器在程序中生成的类型信息。 此类的对象可以有效存储指向类型的名称的指针。 type_info 类还可存储适合比较两个类型是否相等或比较其排列顺序的编码值。 类型的编码规则和排列顺序是未指定的，并且可能因程序而异。
* 头文件：`typeinfo`

typeid、type_info 使用

```cpp
#include <iostream>
using namespace std;

class Flyable                       // 能飞的
{
public:
    virtual void takeoff() = 0;     // 起飞
    virtual void land() = 0;        // 降落
};
class Bird : public Flyable         // 鸟
{
public:
    void foraging() {...}           // 觅食
    virtual void takeoff() {...}
    virtual void land() {...}
    virtual ~Bird(){}
};
class Plane : public Flyable        // 飞机
{
public:
    void carry() {...}              // 运输
    virtual void takeoff() {...}
    virtual void land() {...}
};

class type_info
{
public:
    const char* name() const;
    bool operator == (const type_info & rhs) const;
    bool operator != (const type_info & rhs) const;
    int before(const type_info & rhs) const;
    virtual ~type_info();
private:
    ...
};

void doSomething(Flyable *obj)                 // 做些事情
{
    obj->takeoff();

    cout << typeid(*obj).name() << endl;        // 输出传入对象类型（"class Bird" or "class Plane"）

    if(typeid(*obj) == typeid(Bird))            // 判断对象类型
    {
        Bird *bird = dynamic_cast<Bird *>(obj); // 对象转化
        bird->foraging();
    }

    obj->land();
}

int main(){
	Bird *b = new Bird();
	doSomething(b);
	delete b;
	b = nullptr;
	return 0;
}
```

<a id="effective"></a>


### 其他

* [Bjarne Stroustrup 的常见问题](http://www.stroustrup.com/bs_faq.html)
* [Bjarne Stroustrup 的 C++ 风格和技巧常见问题](http://www.stroustrup.com/bs_faq2.html)

<a id="stl"></a>

## 📦 STL

### STL 索引

[STL 方法含义索引](https://github.com/huihut/interview/tree/master/STL)

### STL 容器

容器 | 底层数据结构 | 时间复杂度 | 有无序 | 可不可重复 | 其他
---|---|---|---|---|---
[array](https://github.com/huihut/interview/tree/master/STL#array)|数组|随机读改 O(1)|无序|可重复|支持随机访问
[vector](https://github.com/huihut/interview/tree/master/STL#vector)|数组|随机读改、尾部插入、尾部删除 O(1)<br/>头部插入、头部删除 O(n)|无序|可重复|支持随机访问
[deque](https://github.com/huihut/interview/tree/master/STL#deque)|双端队列|头尾插入、头尾删除 O(1)|无序|可重复|一个中央控制器 + 多个缓冲区，支持首尾快速增删，支持随机访问
[forward_list](https://github.com/huihut/interview/tree/master/STL#forward_list)|单向链表|插入、删除 O(1)|无序|可重复|不支持随机访问
[list](https://github.com/huihut/interview/tree/master/STL#list)|双向链表|插入、删除 O(1)|无序|可重复|不支持随机访问
[stack](https://github.com/huihut/interview/tree/master/STL#stack)|deque / list|顶部插入、顶部删除 O(1)|无序|可重复|deque 或 list 封闭头端开口，不用 vector 的原因应该是容量大小有限制，扩容耗时
[queue](https://github.com/huihut/interview/tree/master/STL#queue)|deque / list|尾部插入、头部删除 O(1)|无序|可重复|deque 或 list 封闭头端开口，不用 vector 的原因应该是容量大小有限制，扩容耗时
[priority_queue](https://github.com/huihut/interview/tree/master/STL#priority_queue)|vector + max-heap|插入、删除 O(log<sub>2</sub>n)|有序|可重复|vector容器+heap处理规则
[set](https://github.com/huihut/interview/tree/master/STL#set)|红黑树|插入、删除、查找 O(log<sub>2</sub>n)|有序|不可重复|
[multiset](https://github.com/huihut/interview/tree/master/STL#multiset)|红黑树|插入、删除、查找 O(log<sub>2</sub>n)|有序|可重复|
[map](https://github.com/huihut/interview/tree/master/STL#map)|红黑树|插入、删除、查找 O(log<sub>2</sub>n)|有序|不可重复|
[multimap](https://github.com/huihut/interview/tree/master/STL#multimap)|红黑树|插入、删除、查找 O(log<sub>2</sub>n)|有序|可重复|和map容器相比，multimap未提供at()成员方法，也没有重载[]运算符、
[unordered_set](https://github.com/huihut/interview/tree/master/STL#unordered_set)|哈希表|插入、删除、查找 O(1) 最差 O(n)|无序|不可重复|
[unordered_multiset](https://github.com/huihut/interview/tree/master/STL#unordered_multiset)|哈希表|插入、删除、查找 O(1) 最差 O(n)|无序|可重复|
[unordered_map](https://github.com/huihut/interview/tree/master/STL#unordered_map)|哈希表|插入、删除、查找 O(1) 最差 O(n)|无序|不可重复|
[unordered_multimap](https://github.com/huihut/interview/tree/master/STL#unordered_multimap)|哈希表|插入、删除、查找 O(1) 最差 O(n)|无序|可重复|

### STL 算法

算法 | 底层算法 | 时间复杂度 | 可不可重复
---|---|---|---
[find](http://www.cplusplus.com/reference/algorithm/find/)|顺序查找|O(n)|可重复
[sort](https://github.com/gcc-mirror/gcc/blob/master/libstdc++-v3/include/bits/stl_algo.h#L4808)|[内省排序](https://en.wikipedia.org/wiki/Introsort)|O(n*log<sub>2</sub>n)|可重复


<a id="data-structure"></a>

## 〽️ 数据结构

### 顺序结构

#### 顺序栈（Sequence Stack）

[SqStack.cpp](DataStructure/SqStack.cpp)

顺序栈数据结构和图片

```cpp
typedef struct {
	ElemType *elem;
	int top;
	int size;
	int increment;
} SqStack;
```

![](https://gitee.com/huihut/interview/raw/master/images/SqStack.png)

#### 队列（Sequence Queue）

队列数据结构

```cpp
typedef struct {
	ElemType * elem;
	int front;
	int rear;
	int maxSize;
}SqQueue;
```

##### 非循环队列

非循环队列图片

![](https://gitee.com/huihut/interview/raw/master/images/SqQueue.png)

`SqQueue.rear++`

##### 循环队列

循环队列图片

![](https://gitee.com/huihut/interview/raw/master/images/SqLoopStack.png)

`SqQueue.rear = (SqQueue.rear + 1) % SqQueue.maxSize`

#### 顺序表（Sequence List）

[SqList.cpp](DataStructure/SqList.cpp)

顺序表数据结构和图片

```cpp
typedef struct {
	ElemType *elem;
	int length;
	int size;
	int increment;
} SqList;
```

![](https://gitee.com/huihut/interview/raw/master/images/SqList.png)


### 链式结构

[LinkList.cpp](DataStructure/LinkList.cpp)

[LinkList_with_head.cpp](DataStructure/LinkList_with_head.cpp)

链式数据结构

```cpp
typedef struct LNode {
    ElemType data;
    struct LNode *next;
} LNode, *LinkList; 
```

#### 链队列（Link Queue）

链队列图片

![](https://gitee.com/huihut/interview/raw/master/images/LinkQueue.png)

#### 线性表的链式表示

##### 单链表（Link List）

单链表图片

![](https://gitee.com/huihut/interview/raw/master/images/LinkList.png)

##### 双向链表（Du-Link-List）

双向链表图片

![](https://gitee.com/huihut/interview/raw/master/images/DuLinkList.png)

##### 循环链表（Cir-Link-List）

循环链表图片

![](https://gitee.com/huihut/interview/raw/master/images/CirLinkList.png)

### 哈希表

[HashTable.cpp](DataStructure/HashTable.cpp)

#### 概念

哈希函数：`H(key): K -> D , key ∈ K`

#### 构造方法

* 直接定址法
* 除留余数法
* 数字分析法
* 折叠法
* 平方取中法

#### 冲突处理方法

* 链地址法：key 相同的用单链表链接
* 开放定址法
    * 线性探测法：key 相同 -> 放到 key 的下一个位置，`Hi = (H(key) + i) % m`
    * 二次探测法：key 相同 -> 放到 `Di = 1^2, -1^2, ..., ±（k)^2,(k<=m/2）`
    * 随机探测法：`H = (H(key) + 伪随机数) % m`

#### 线性探测的哈希表数据结构

线性探测的哈希表数据结构和图片

```cpp
typedef char KeyType;

typedef struct {
	KeyType key;
}RcdType;

typedef struct {
	RcdType *rcd;
	int size;
	int count;
	bool *tag;
}HashTable;
```

![](https://gitee.com/huihut/interview/raw/master/images/HashTable.png)

### 递归

#### 概念

函数直接或间接地调用自身

#### 递归与分治

* 分治法
    * 问题的分解
    * 问题规模的分解
* 折半查找（递归）
* 归并排序（递归）
* 快速排序（递归）

#### 递归与迭代

* 迭代：反复利用变量旧值推出新值
* 折半查找（迭代）
* 归并排序（迭代）

#### 广义表

##### 头尾链表存储表示

广义表的头尾链表存储表示和图片

```cpp
// 广义表的头尾链表存储表示
typedef enum {ATOM, LIST} ElemTag;
// ATOM==0：原子，LIST==1：子表
typedef struct GLNode {
    ElemTag tag;
    // 公共部分，用于区分原子结点和表结点
    union {
        // 原子结点和表结点的联合部分
        AtomType atom;
        // atom 是原子结点的值域，AtomType 由用户定义
        struct {
            struct GLNode *hp, *tp;
        } ptr;
        // ptr 是表结点的指针域，prt.hp 和 ptr.tp 分别指向表头和表尾
    } a;
} *GList, GLNode;
```

![](https://gitee.com/huihut/interview/raw/master/images/GeneralizedList1.png)

##### 扩展线性链表存储表示

扩展线性链表存储表示和图片

```cpp
// 广义表的扩展线性链表存储表示
typedef enum {ATOM, LIST} ElemTag;
// ATOM==0：原子，LIST==1：子表
typedef struct GLNode1 {
    ElemTag tag;
    // 公共部分，用于区分原子结点和表结点
    union {
        // 原子结点和表结点的联合部分
        AtomType atom; // 原子结点的值域
        struct GLNode1 *hp; // 表结点的表头指针
    } a;
    struct GLNode1 *tp;
    // 相当于线性链表的 next，指向下一个元素结点
} *GList1, GLNode1;
```

![](https://gitee.com/huihut/interview/raw/master/images/GeneralizedList2.png)

### 二叉树

[BinaryTree.cpp](DataStructure/BinaryTree.cpp)

#### 性质

1. 非空二叉树第 i 层最多 2<sup>(i-1)</sup> 个结点 （i >= 1）
2. 深度为 k 的二叉树最多 2<sup>k</sup> - 1 个结点 （k >= 1）
3. 度为 0 的结点数为 n<sub>0</sub>，度为 2 的结点数为 n<sub>2</sub>，则 n<sub>0</sub> = n<sub>2</sub> + 1
4. 有 n 个结点的完全二叉树深度 k = ⌊ log<sub>2</sub>(n) ⌋ + 1 
5. 对于含 n 个结点的完全二叉树中编号为 i （1 <= i <= n） 的结点
    1. 若 i = 1，为根，否则双亲为 ⌊ i / 2 ⌋
    2. 若 2i > n，则 i 结点没有左孩子，否则孩子编号为 2i
    3. 若 2i + 1 > n，则 i 结点没有右孩子，否则孩子编号为 2i + 1

#### 存储结构

二叉树数据结构

```cpp
typedef struct BiTNode
{
    TElemType data;
    struct BiTNode *lchild, *rchild;
}BiTNode, *BiTree;
```

##### 顺序存储

二叉树顺序存储图片

![](https://gitee.com/huihut/interview/raw/master/images/SqBinaryTree.png)

##### 链式存储

二叉树链式存储图片

![](https://gitee.com/huihut/interview/raw/master/images/LinkBinaryTree.png)

#### 遍历方式

* 先序遍历
* 中序遍历
* 后续遍历
* 层次遍历

#### 分类

* 满二叉树
* 完全二叉树（堆）
    * 大顶堆：根 >= 左 && 根 >= 右
    * 小顶堆：根 <= 左 && 根 <= 右
* 二叉查找树（二叉排序树）：左 < 根 < 右
* 平衡二叉树（AVL树）：| 左子树树高 - 右子树树高 | <= 1
* 最小失衡树：平衡二叉树插入新结点导致失衡的子树：调整：
    * LL型：根的左孩子右旋
    * RR型：根的右孩子左旋
    * LR型：根的左孩子左旋，再右旋
    * RL型：右孩子的左子树，先右旋，再左旋

### 其他树及森林

#### 树的存储结构

* 双亲表示法
* 双亲孩子表示法
* 孩子兄弟表示法

#### 并查集

一种不相交的子集所构成的集合 S = {S1, S2, ..., Sn}

#### 平衡二叉树（AVL树）

##### 性质

* | 左子树树高 - 右子树树高 | <= 1
* 平衡二叉树必定是二叉搜索树，反之则不一定
* 最小二叉平衡树的节点的公式：`F(n)=F(n-1)+F(n-2)+1` （1 是根节点，F(n-1) 是左子树的节点数量，F(n-2) 是右子树的节点数量）

平衡二叉树图片

![](https://gitee.com/huihut/interview/raw/master/images/Self-balancingBinarySearchTree.png)

##### 最小失衡树

平衡二叉树插入新结点导致失衡的子树

调整：

* LL 型：根的左孩子右旋
* RR 型：根的右孩子左旋
* LR 型：根的左孩子左旋，再右旋
* RL 型：右孩子的左子树，先右旋，再左旋

#### 红黑树

[RedBlackTree.cpp](DataStructure/RedBlackTree.cpp)

##### 红黑树的特征是什么？

1. 节点是红色或黑色。
2. 根是黑色。
3. 所有叶子都是黑色（叶子是 NIL 节点）。
4. 每个红色节点必须有两个黑色的子节点。（从每个叶子到根的所有路径上不能有两个连续的红色节点。）（新增节点的父节点必须相同）
5. 从任一节点到其每个叶子的所有简单路径都包含相同数目的黑色节点。（新增节点必须为红）

##### 调整

1. 变色
2. 左旋
3. 右旋

##### 应用

* 关联数组：如 STL 中的 map、set

##### 红黑树、B 树、B+ 树的区别？

* 红黑树的深度比较大，而 B 树和 B+ 树的深度则相对要小一些
* B+ 树则将数据都保存在叶子节点，同时通过链表的形式将他们连接在一起。

#### B 树（B-tree）、B+ 树（B+-tree）

B 树、B+ 树图片

![B 树（B-tree）、B+ 树（B+-tree）](https://i.stack.imgur.com/l6UyF.png)

##### 特点

* 一般化的二叉查找树（binary search tree）
* “矮胖”，内部（非叶子）节点可以拥有可变数量的子节点（数量范围预先定义好）

##### 应用

* 大部分文件系统、数据库系统都采用B树、B+树作为索引结构

##### 区别

* B+树中只有叶子节点会带有指向记录的指针（ROWID），而B树则所有节点都带有，在内部节点出现的索引项不会再出现在叶子节点中。
* B+树中所有叶子节点都是通过指针连接在一起，而B树不会。

##### B树的优点

对于在内部节点的数据，可直接得到，不必根据叶子节点来定位。

##### B+树的优点

* 非叶子节点不会带上 ROWID，这样，一个块中可以容纳更多的索引项，一是可以降低树的高度。二是一个内部节点可以定位更多的叶子节点。
* 叶子节点之间通过指针来连接，范围扫描将十分简单，而对于B树来说，则需要在叶子节点和内部节点不停的往返移动。

> B 树、B+ 树区别来自：[differences-between-b-trees-and-b-trees](https://stackoverflow.com/questions/870218/differences-between-b-trees-and-b-trees)、[B树和B+树的区别](https://www.cnblogs.com/ivictor/p/5849061.html)

#### 八叉树

八叉树图片

![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/35/Octree2.png/400px-Octree2.png)

八叉树（octree），或称八元树，是一种用于描述三维空间（划分空间）的树状数据结构。八叉树的每个节点表示一个正方体的体积元素，每个节点有八个子节点，这八个子节点所表示的体积元素加在一起就等于父节点的体积。一般中心点作为节点的分叉中心。

##### 用途

* 三维计算机图形
* 最邻近搜索

<a id="algorithm"></a>

## ⚡️ 算法

### 排序

排序算法 | 平均时间复杂度 | 最差时间复杂度 | 空间复杂度 | 数据对象稳定性
---|---|---|---|---
[冒泡排序](Algorithm/BubbleSort.h) | O(n<sup>2</sup>)|O(n<sup>2</sup>)|O(1)|稳定
[选择排序](Algorithm/SelectionSort.h) | O(n<sup>2</sup>)|O(n<sup>2</sup>)|O(1)|数组不稳定、链表稳定
[插入排序](Algorithm/InsertSort.h) | O(n<sup>2</sup>)|O(n<sup>2</sup>)|O(1)|稳定
[快速排序](Algorithm/QuickSort.h) | O(n*log<sub>2</sub>n) |  O(n<sup>2</sup>) | O(log<sub>2</sub>n) | 不稳定
[堆排序](Algorithm/HeapSort.cpp) | O(n*log<sub>2</sub>n)|O(n*log<sub>2</sub>n)|O(1)|不稳定
[归并排序](Algorithm/MergeSort.h) | O(n*log<sub>2</sub>n) | O(n*log<sub>2</sub>n)|O(n)|稳定
[希尔排序](Algorithm/ShellSort.h) | O(n*log<sup>2</sup>n)|O(n<sup>2</sup>)|O(1)|不稳定
[计数排序](Algorithm/CountSort.cpp) | O(n+m)|O(n+m)|O(n+m)|稳定
[桶排序](Algorithm/BucketSort.cpp) | O(n)|O(n)|O(m)|稳定
[基数排序](Algorithm/RadixSort.h) | O(k*n)|O(n<sup>2</sup>)| |稳定

> * 均按从小到大排列
> * k：代表数值中的 “数位” 个数
> * n：代表数据规模
> * m：代表数据的最大值减最小值
> * 来自：[wikipedia . 排序算法](https://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95)

### 查找

查找算法 | 平均时间复杂度 | 空间复杂度 | 查找条件
---|---|---|---
[顺序查找](Algorithm/SequentialSearch.h) | O(n) | O(1) | 无序或有序
[二分查找（折半查找）](Algorithm/BinarySearch.h) | O(log<sub>2</sub>n)| O(1) | 有序
[插值查找](Algorithm/InsertionSearch.h) | O(log<sub>2</sub>(log<sub>2</sub>n)) | O(1) | 有序
[斐波那契查找](Algorithm/FibonacciSearch.cpp) | O(log<sub>2</sub>n) | O(1) | 有序
[哈希查找](DataStructure/HashTable.cpp) | O(1) | O(n) | 无序或有序
[二叉查找树（二叉搜索树查找）](Algorithm/BSTSearch.h) |O(log<sub>2</sub>n) |   | 
[红黑树](DataStructure/RedBlackTree.cpp) |O(log<sub>2</sub>n) | |
2-3树 | O(log<sub>2</sub>n - log<sub>3</sub>n) |   | 
B树/B+树 |O(log<sub>2</sub>n) |   | 

### 图搜索算法

图搜索算法 |数据结构| 遍历时间复杂度 | 空间复杂度
---|---|---|---
[BFS广度优先搜索](https://zh.wikipedia.org/wiki/%E5%B9%BF%E5%BA%A6%E4%BC%98%E5%85%88%E6%90%9C%E7%B4%A2)|邻接矩阵<br/>邻接链表|O(\|v\|<sup>2</sup>)<br/>O(\|v\|+\|E\|)|O(\|v\|<sup>2</sup>)<br/>O(\|v\|+\|E\|)
[DFS深度优先搜索](https://zh.wikipedia.org/wiki/%E6%B7%B1%E5%BA%A6%E4%BC%98%E5%85%88%E6%90%9C%E7%B4%A2)|邻接矩阵<br/>邻接链表|O(\|v\|<sup>2</sup>)<br/>O(\|v\|+\|E\|)|O(\|v\|<sup>2</sup>)<br/>O(\|v\|+\|E\|)

### 其他算法

算法 |思想| 应用
---|---|---
[分治法](https://zh.wikipedia.org/wiki/%E5%88%86%E6%B2%BB%E6%B3%95)|把一个复杂的问题分成两个或更多的相同或相似的子问题，直到最后子问题可以简单的直接求解，原问题的解即子问题的解的合并|[循环赛日程安排问题](https://github.com/huihut/interview/tree/master/Problems/RoundRobinProblem)、排序算法（快速排序、归并排序）
[动态规划](https://zh.wikipedia.org/wiki/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92)|通过把原问题分解为相对简单的子问题的方式求解复杂问题的方法，适用于有重叠子问题和最优子结构性质的问题|[背包问题](https://github.com/huihut/interview/tree/master/Problems/KnapsackProblem)、斐波那契数列
[贪心法](https://zh.wikipedia.org/wiki/%E8%B4%AA%E5%BF%83%E6%B3%95)|一种在每一步选择中都采取在当前状态下最好或最优（即最有利）的选择，从而希望导致结果是最好或最优的算法|旅行推销员问题（最短路径问题）、最小生成树、哈夫曼编码

<a id="problems"></a>

## ❓ Problems

### Single Problem

* [Chessboard Coverage Problem（棋盘覆盖问题）](Problems/ChessboardCoverageProblem)
* [Knapsack Problem（背包问题）](Problems/KnapsackProblem)
* [Neumann Neighbor Problem（冯诺依曼邻居问题）](Problems/NeumannNeighborProblem)
* [Round Robin Problem（循环赛日程安排问题）](Problems/RoundRobinProblem)
* [Tubing Problem（输油管道问题）](Problems/TubingProblem)

### Leetcode Problems

* [Github . haoel/leetcode](https://github.com/haoel/leetcode)
* [Github . pezy/LeetCode](https://github.com/pezy/LeetCode)

### 剑指 Offer

* [Github . zhedahht/CodingInterviewChinese2](https://github.com/zhedahht/CodingInterviewChinese2)
* [Github . gatieme/CodingInterviews](https://github.com/gatieme/CodingInterviews)

### Cracking the Coding Interview 程序员面试金典

* [Github . careercup/ctci](https://github.com/careercup/ctci)
* [牛客网 . 程序员面试金典](https://www.nowcoder.com/ta/cracking-the-coding-interview)

### 牛客网

* [牛客网 . 在线编程专题](https://www.nowcoder.com/activity/oj)

<a id="os"></a>

## 💻 操作系统
操作系统的几个分块：
* 进程与线程与纤程
* 进程间通信
* 进程间同步
* 操作系统调度
* 内存管理
* 文件系统
* 中断处理
### 进程与线程

* 进程是资源分配的独立单位
* 线程是资源调度的独立单位

- 进程是一个运行程序的一个抽象。是资源分配的基本单元。
- 进程的调度开销较大，所以引入了进程内的单独执行单元，叫做线程
- 线程中单独维护的状态
  - 运行栈信息
  - pc
  - 寄存器状态
- 同一个进程中多个线程共享的资源
  - 虚拟内存空间
  - 打开的文件

- 进程内存空间布局
  - 内核部分独占空间
  - 用户栈
  - 代码库
  - 用户堆
  - 数据段
  - 代码段
- 进程包含了
  - 进程标识符pid
  - 进程状态：就绪、运行、阻塞
  - 虚拟内存状态：页表表示哪些空间已经被放到
  - 打开的文件：文件描述符表
  - 运行时上下文状态
    - pc
    - 寄存器状态

### 纤程
线程由操作系统对**线程工作内容无感知地**进行调度，用户级线程，即**纤程**（fiber），可以在更轻量级的创建和切换消耗下对工作在用户态进行调度。

### 线程池
// https://blog.csdn.net/wangmj_hdu/article/details/119778255
线程池用一个数组维护了一组线程，然后一直放着，如果没用，就用条件变量让它休眠，如果加入一个新的任务就唤醒其中一个去执行这个任务
* 为了减少创建与销毁线程所带来的时间消耗与资源消耗，因此采用线程池的策略：
* 在多并发任务中无法为每个任务都创建一个线程，那么任务可以进入线程池的任务队列，等有空闲的线程了再进行执行

#### 内核线程和用户线程


#### 线程池的实现
- 线程数组：每个线程都是一个循环，不断地从任务队列中拿任务执行
- 任务队
- 控制同步的锁，条件变量：条件变量在任务进入任务队列的时候通知一个线程来执行任务

#### 不同平台对纤程的支持
- **POSIX**（可移植操作系统接口，Portable Operating System Interface for uniX）中的**ucontext**对钎程进行了支持，其提供了如下几个接口对钎程提供服务
  - **getcontext**用于保存当前用户上下文到一个context变量，参数为需要保存到的context变量
  - **makecontext**用于修改一个存在的context，指定在此上下文中执行的函数，配合getcontext使用，参数为1.context 2.在当前上下文中需要执行的函数 3.传入的函数参数
  - **setcontext**用户切换到另一个上下文，接受一个context变量
- **Windows**也提供了与ucontext类似的接口，如**CreateFiber**，**SwitchToFiber**接口
- **很多程序语言**，如c++，ruby，Go，Lua也提供了对纤程的支持，一般将程序语言提供的纤程成为**协程**

#### 进程之间的通信方式以及优缺点

* 管道（PIPE）
    * 有名管道：一种半双工的通信方式，它允许无亲缘关系进程间的通信
        * 优点：可以实现任意关系的进程间的通信
        * 缺点：
            1. 长期存于系统中，使用不当容易出错
            2. 缓冲区有限
    * 无名管道：一种半双工的通信方式，只能在具有亲缘关系的进程间使用（父子进程）
        * 优点：简单方便
        * 缺点：
            1. 局限于单向通信 
            2. 只能创建在它的进程以及其有亲缘关系的进程之间 
            3. 缓冲区有限 
* 信号量（Semaphore）：一个计数器，可以用来控制多个线程对共享资源的访问
    * 优点：可以同步进程
    * 缺点：信号量有限
    * c中信号量的写法
      * #include<semaphore.h> 
      * sem_t sem1; 
      * sem_init(&sem1, 0, 0);  // 第二个参数0表示是线程间通信，大于0表示进程间通信 ，第三个参数是指信号量的初始值
      * sem_wait(&sem1); // p操作
      * sem_post(&sem1) // v操作
* 信号（Signal）：一种比较复杂的通信方式，用于通知接收进程某个事件已经发生
* 消息队列（Message Queue）：是消息的链表，存放在内核中并由消息队列标识符标识
    * 优点：可以实现任意进程间的通信，并通过系统调用函数来实现消息发送和接收之间的同步，无需考虑同步问题，方便
    * 缺点：信息的复制需要额外消耗 CPU 的时间，不适宜于信息量大或操作频繁的场合
* 共享内存（Shared Memory）：映射一段能被其他进程所访问的内存，这段共享内存由一个进程创建，但多个进程都可以访问
    * 优点：无须复制，快捷，信息量大
    * 缺点：
        1. 通信是通过将共享空间缓冲区直接附加到进程的虚拟地址空间中来实现的，因此进程间的读写操作的同步问题
        2. 利用内存缓冲区直接交换信息，内存的实体存在于计算机中，只能同一个计算机系统中的诸多进程共享，不方便网络通信
* 套接字（Socket）：可用于不同计算机间的进程通信
    * 优点：
        1. 传输数据为字节级，传输数据可自定义，数据量小效率高
        2. 传输数据时间短，性能高
        3. 适合于客户端和服务器端之间信息实时交互
        4. 可以加密,数据安全性强
    * 缺点：需对传输的数据进行解析，转化成应用级的数据。

#### 线程之间的同步方式

* 锁机制：包括互斥锁/量（mutex）、读写锁（reader-writer lock）、自旋锁（spin lock）、条件变量（condition）
    * 互斥锁/量（mutex）：提供了以排他方式防止数据结构被并发修改的方法。
    * 读写锁（reader-writer lock）：允许多个线程同时读共享数据，而对写操作是互斥的。
    * 自旋锁（spin lock）与互斥锁类似，都是为了保护共享资源。互斥锁是当资源被占用，申请者进入睡眠状态；而自旋锁则循环检测保持者是否已经释放锁。
    * 条件变量（condition）：可以以原子的方式阻塞进程，直到某个特定条件为真为止。对条件的测试是在互斥锁的保护下进行的。条件变量始终与互斥锁一起使用。
* 信号量机制(Semaphore)
    * 无名线程信号量
    * 命名线程信号量
* 信号机制(Signal)：类似进程间的信号处理
* 屏障（barrier）：屏障允许每个线程等待，直到所有的合作线程都达到某一点，然后从该点继续执行。

线程间的通信目的主要是用于线程同步，所以线程没有像进程通信中的用于数据交换的通信机制  

> 进程之间的通信方式以及优缺点来源于：[进程线程面试题总结](http://blog.csdn.net/wujiafei_njgcxy/article/details/77098977)

#### 进程同步方法
- 互斥锁：最常见的线程同步方式，在使用一个共享资源前加锁，使用后解锁
  - 分类：使用CAS实现的自旋锁，使用FAA实现的排号自旋锁
  - 优点：使用简单
  - 缺点：自旋锁不能保证获得锁的顺序，即**不公平**，排号自旋锁解决了这一问题；在获取锁的时候会进行忙等待
  - **在Pthread库中mutex不是互斥锁，在没有获得锁的时候不会忙等待，会把当前线程进入睡眠**
- 条件变量：为了解决获取互斥锁后，某些条件没有满足导致线程拿到锁依旧在等待某些条件导致**忙等待**的问题，条件变量提供了**挂起/唤醒**机制，且必须**与互斥锁一起使用**
  - https://stackoverflow.com/questions/4742196/advantages-of-using-condition-variables-over-mutex
  - 优点：解决了互斥锁在访问共享资源的时候的条件不满足引起的忙等待（busy looping）
  - 提供了两个接口，**cond_wait**用来挂起当前已经拿到锁但没有满足条件的线程,**cond_signal**用于唤醒等待该条件变量的线程
- 信号量：使用计数器表示可以使用的共享资源数量，与互斥锁仅能一个线程进入临界区不同，信号量可以允许多个线程进入临界区
- 读写锁：当一些线程仅需要读取而非修改共享资源时，多个读线程不需要互斥性。与互斥锁相比，在多个读线程时有更好的性能。针对读线程与写线程分别提供了不同的lock和unlock操作；设想一种情况：已经有一个读线程在临界区，此时有一个写线程和一个读线程同时申请进入临界区，在选择的偏好中分为**偏向读者的读写锁**和**偏向写者的读写锁**

#### 进程之间私有和共享的资源

* 私有：地址空间、堆、全局变量、栈、寄存器
* 共享：代码段，公共数据，进程目录，进程 ID

#### 线程之间私有和共享的资源

* 私有：线程栈，寄存器，程序计数器
* 共享：堆，地址空间，全局变量，静态变量

### 僵尸进程，孤儿进程
博客 https://www.cnblogs.com/Anker/p/3271773.html
进程终止时，操作系统会释放其资源，包括打开的资源、占用的内存。但进程表中的条目还是存在的，直到父进程的调用wait()函数；
* 僵尸进程：进程终止后，还未被父进程wait()回收进程表条目，这样的进程叫做僵尸进程，每个进程终止时都会过渡到这一状态。如果僵尸进程过多会导致进程号被占用，而操作系统的进程号是有限的，会影响产生新的进程。
* 如果父进程还没调用wait()前就退出了，子进程就变成了孤儿进程，内核会把init进程作为孤儿进程的父进程。init进程会定期调用wait()函数收集孤儿进程的退出状态，释放掉子进程的进程标识符和进程表条目

子进程退出后，**父进程默认调用wiat函数还是可以自由选择？**，如果是后者父进程不主动调用wait,而子进程很多且运行速度更快就会出很多僵尸进程？？？
* 如何处理僵尸进程：
  * 将把那个生产出大量僵尸进程的父进程kill掉，僵尸进程就可以被init进程收养然后被定时释放，
  * 修改里面的逻辑让它及时地调用wait函数！！

### kill命令 -9 -15
信号是单向通知进程事件发生的方式
信号是使用kill系统调用发送的
常见的操作是ctrl+c发送一个信号给当前shell前台进程，或者kill pid
* kill -15 -9区别

| kill - 15 | kill - 9|
|  ----  |  ----  |
|优雅地终止一个进程 | 粗暴地终止一个进程|
|这个信号可以被自定义的handler重新定义行为|不能被重新定义|
|不杀死子进程 | 杀死子进程|

kill-15(SIGTERM)与kill-9（SIGKILL）与kill-2（SIGINT，由ctrl+c触发），若没有修改默认的handler，其行为没有差别，kill-3(SIGQUIT)在退出时会保存一个coredump
SIGINT 的默认操作与 SIGTERM 的默认操作和 SIGKILL 的不可更改操作是相同类型的进程终止； SIGQUIT 的默认操作也是进程终止，但可能会发生其他实现定义的操作，例如生成核心转储。如果需要，进程可以捕获或忽略其中之一。

### cpu调度
#### 调度算法
* 先到先服务调度
* 优先级调度
* 短任务优先调度
* 截止时间优先调度
* 时间片轮询调度
* 两级调度：为了减少任务在不同CPU上的调度开销，每个CPU都维护自己的任务队列，在单个CPU中使用自己的调度算法
* 多级反馈队列调度
#### linux当前使用的是**完全公平调度算法**
  * 引入了时间片调度、优先级调度、两级调度等思想
  * 实现上使用了：优先级动态决定时间片大小，引入虚拟运行时间进行调度，维护这个运行队列使用了红黑树，以虚拟时间为key，调度虚拟运行时间最小的任务

#### 多进程与多线程间的对比、优劣与选择

### socket
socket用于本机进程间或不同计算机进程间的消息传递。
一个socket就是网络上进行进程通信的一个端点，在程序的角度来看角度看一个socket就是一个有相应描述符的文件。
socket提供了
* 服务端和客户端初始化 socket，得到文件描述符；
* 服务端调用 bind，将文件描述符绑定在 IP 地址和端口;
* 服务端调用 listen，进行监听；(socket函数默认返回一个主动套接字的描述符，使用listen把它修改成服务端)
* 服务端调用 accept，等待客户端连接；
* 客户端调用 connect，向服务器端的地址和端口发起连接请求；
* 服务端 accept 返回用于传输的 socket 的文件描述符；
* 客户端调用 write 写入数据；
* 服务端调用 read 读取数据；
* 客户端断开连接时，会调用 close，那么服务端 read 读取数据的时候，就会读取到了 EOF，待处理完数据后，服务端调用 close，表示连接关闭。

#### 缓存io
缓存io又叫做标准io，是应用程序对文件的访问需要先拷贝到内核空间buffer中，然后内核空间buffer再copy到应用程序的地址空间。

### IO多路复用
传统的网络IO模型一个进程或线程去建立一个网络连接，性能开销大，效率低
IO多路复用是实现一个线程可以监视多个文件描述符，这个线程会把所有的文件描述符都传给内核，然后由内核返回产生了事件的连接
内核提供了IO多路复用的三种系统调用：
* select 把一个文件描述符集合全部copy到内核，让内核检查是否有网络事件发生，然后标记每个文件描述符是否可读写，然后把文件描述符集合copy到用户态。select缺点是（1）需要两次文件描述符集合的copy，（2）select参数的默认为1024个
* poll把select数组的存储方式更换成了链表，打破了2014的最大监听数量限制
* epoll解决了select和poll没有解决的问题
  * 每次都需要把所有的文件描述符都进行copy问题：epoll在内核中维护了所有待检测的文件描述符，使用一个红黑树进行管理，使用log（n）的复杂度进行对树操作
  * epoll使用了**事件驱动**机制，内核中维护了一个链表记录就绪的事件，当某个文件描述符有事件发生，就通过**回调函数**把这个就绪事件返回。
    * epoll 支持两种事件触发模式，分别是边缘触发（edge-triggered，ET）和水平触发（level-triggered，LT）。
    * 使用边缘触发模式时，当被监控的 Socket 描述符上有可读事件发生时，服务器端只会从 epoll_wait 中苏醒一次，即使进程没有调用 read 函数从内核读取数据，也依然只苏醒一次，因此我们程序要保证一次性将内核缓冲区的数据读取完；
    * 使用水平触发模式时，当被监控的 Socket 上有可读事件发生时，服务器端不断地从 epoll_wait 中苏醒，直到内核缓冲区数据被 read 函数读完才结束，目的是告诉我们有数据需要读取；


### 内存管理
* 虚拟地址和物理地址
  * 叙事方式 虚拟地址空间引入增加了程序开发的便捷性 -> 引入了虚拟地址到物理地址的转换 -> 引入分页机制来做地址映射 -> 页表替换策略、tlb快表
* 虚拟地址分配
  * 用户态需要新的地址空间时需要使用malloc接口申请虚拟地址空间 -> 大的虚拟地址空间使用mmap，小的brk
* 物理分配算法
  * 内部碎片和外部碎片
  * 伙伴系统
  * SLAB分配器
  * 用户态的一些空闲链表
#### 虚拟地址空间
1、每个进程都有独立的虚拟地址空间，进程访问的虚拟地址并不是真正的物理地址； 
2、虚拟地址可通过每个进程上的页表(在每个进程的内核虚拟地址空间)与物理地址进行映射，获得真正物理地址； 
3、如果虚拟地址对应物理地址不在物理内存中，则产生缺页中断，真正分配物理地址，同时更新进程的页表；如果此时物理内存已耗尽，则根据内存替换算法淘汰部分页面至物理磁盘中

#### 虚拟地址到物理地址的转换
1. MMU和TLB负责虚拟地址空间到物理地址的转换
2. 根据翻译机制可以分为分段机制和分页机制
* 分段机制
  * 虚拟地址分为两个部分，一个是段号，一个是段偏移量
  * mmu使用段表和段号通过寻找到段的物理地址，然后加上偏移量即为虚拟地址对应的物理地址
  * 操作系统以段的方式管理物理内存。进程中的虚拟内存空间以若干个大小不同的段组成。
* 分页机制
  * 把虚拟地址空间和物理地址空间都分成连续、大小相同的页
  * 把虚拟地址分成两个部分，一个是虚拟页号，一个是页内偏移
  * mmu使用页表找到虚拟页表的物理地址，然后根据偏移量算出虚拟地址对应的物理地址
3. 每个进程都会拥有自己的页表，记录着虚拟页号到物理页号的转换
4. 如果虚拟地址对应物理地址不在物理内存中，则产生缺页中断，真正分配物理地址，同时更新进程的页表；如果此时物理内存已耗尽，则根据内存替换算法淘汰部分页面至物理磁盘中
5. 使用多级页表来减少页表内存占用
6. 使用大页（比4k更大）使虚拟地址到物理地址转换项更小，用来提升TLB命中率，增加效率

#### 多级页表
为了解决虚拟地址空间过大，而实际使用的虚拟地址空间小，导致的页表项
#### 虚拟地址分配（malloc）
malloc内存分配使用了两个系统调用，在申请地址空间空间比较小的时候使用brk，申请空间比较大时实用mmap
brk会把堆指针往高地址推，然后把这块虚拟地址空间返回
mmap会在用户堆和栈中间的一段映射区地址空间返回
* brk会产生很多内存碎片，free掉的空间可能不会被释放，而是被回收
两种分配方式都只会分配虚拟地址空间，不会分配真正的物理地址空间。第一次读写时触发缺页中断，操作系统才给分配物理空间，然后在页表中维护虚拟地址到物理地址的映射。

#### 物理内存分配算法
* 首次适应算法（可不谈）
* 最佳适应算法（可不谈）
* 最差适应算法（可不谈）
* 伙伴系统算法
  * 把内存划分为连续的块，最小分配单元是一个物理页（4KB），所有块的大小都是4kB的2次幂,以块为基本单位进行分配。用于大的物理地址分配。实现上维护了不同大小的块空闲链表，分配内存时找到合适的大小块进行分配，如果没有合适的，把一个更大的块拆分成两块用，释放内存时，可以直接找到他的兄弟节点试图合并，放到更大的空闲链表中
* slab分配器
  * 伙伴系统最小分配时4kB，但大多数情况下不需要这么大的空间，会出现大量的内部碎片。所以有了一种面向小内存分配的slab分配器：slab分配器从伙伴系统中申请到一定大小的物理内存，并将这个物理内存作为一个slab。slab内部会划分成等长的小块内存，内部的空闲小块内存会被组织称空闲链表进行使用。

私有匿名映射:通常用于内存分配，堆，栈
共享匿名映射:通常用于进程间共享内存，在内存文件系统中创建/dev/zero设备
私有文件映射:通常用于加载动态库，代码段，数据段
共享文件映射:通常用于文件读写和进程间通信

### 文件系统
文件是一个具有名称的字符序列，内容包括文件数据和元数据（包含文件大小，修改时间，文件权限，文件链接数）；文件系统用来管理这些文件。
文件系统把存储设备抽象为块设备，块设备存储单位被分成了块，一般为512字节或4KB，每个块都有自己的地址，叫块号。
操作系统里面的文件分类有：普通文件，目录文件，符号链接文件，FIFO文件，socket文件、字符设备文件、块设备文件
#### 基于inode的文件系统
一个inode用来存储一个文件，inode的内容包括：
* 文件元数据
* 指向所有文件内容存储块的指针，这样的指针分为直接指针，间接指针，二级指针
#### 特殊文件
* 目录文件：引入了文件名称，目录文件保存了记录了从文件名到inode的映射，每一个映射都是目录项
* 符号链接文件：
  * 硬链接：在目录文件的目录项中新创建一个目录项，保存了文件名称和inode号，与原有的文件地位相同，inode的引用数+1
  * 软连接：在文件内容中保存的是一个文件路径，在进行访问时，通过间接引用指针方式找到**目标文件**进行访问

### 中断、中断控制器
* 原因：在没有中断之前，CPU与设备进行交互是使用1）mmap将设备的存储空间映射到内存空间2）轮询查看设备地址空间内的状态寄存器看是否新的事件发生；这种轮询效率很低
* 中断可以让设备主动通知CPU一个外部事件发生了
* 操作系统在内部实现了一套处理逻辑，即中断处理函数
* 中断处理流程：
  * 保存上下文，中断返回地址，当前PC或者下一条指令PC，通用寄存器，压入到内核栈里
    * x86将上下文放在内核栈（csapp3），ARM将上下文放在寄存器中（陈海波 操作系统）
  * 陷入内核，根据异常类型在异常表中选择对应的异常处理函数，执行完后
  * 恢复上下文，跳转到返回地址
* 中断处理的上半部分和下半部分
  * 上半部分：完成一些必要但轻量级的工作，（中断处理函数，中断处理例程）
    * 在上半部分中关闭中断，在上半部分处理完成后，CPU马上通知中断处理器该中断处理完毕，并打开中断；
    * 上半部分处理中，会向内核注册一个新的处理任务，作为下半部分执行函数。会被CPU进行调度。
  * 下半部分：完成一些复杂的、耗时的工作：
    * 三种实现方式：软中断、tasklet、工作队列、并发可管理工作队列
      * 软中断：最基本的下半部分实现，
        * 产生后并不是马上执行，需要进行内核调度
        * 软中断不会被自己打断，被硬中断打断
        * 同一类型的软中断可以在多个CPU上并行运行，所以必须设计为可重入（避免使用全局变量，使用的时候上锁）
      * tasklet：是基于软中断的，本身是软中断的一种
        * tasklet不允许单个类型的tasklet任务多个CPU上的并行处理，所以不需要考虑可重入问题（开发简单与性能的平衡）
        * 软中断是静态分配的，在内核编译好之后，就不能改变。但tasklet就灵活许多，可以在运行时改变
      * 工作队列：为了解决tasklet和软中断都运行在中断上下文中，不能睡眠和被抢占，单个实例任务时间过长会导致系统实时性下降
        * 把需要推迟的下半部任务放在内核线程的上下文中执行，可以进行睡眠和调度，增强实时性

### DMA


##### 对比

对比维度 | 多进程 | 多线程 | 总结
---|---|---|---
数据共享、同步|数据共享复杂，需要用 IPC；数据是分开的，同步简单|因为共享进程数据，数据共享简单，但也是因为这个原因导致同步复杂|各有优势
内存、CPU|占用内存多，切换复杂，CPU 利用率低|占用内存少，切换简单，CPU 利用率高|线程占优
创建销毁、切换|创建销毁、切换复杂，速度慢|创建销毁、切换简单，速度很快|线程占优
编程、调试|编程简单，调试简单|编程复杂，调试复杂|进程占优
可靠性|进程间不会互相影响|一个线程挂掉将导致整个进程挂掉|进程占优
分布式|适应于多核、多机分布式；如果一台机器不够，扩展到多台机器比较简单|适应于多核分布式|进程占优

##### 优劣

优劣|多进程|多线程
---|---|---
优点|编程、调试简单，可靠性较高|创建、销毁、切换速度快，内存、资源占用小
缺点|创建、销毁、切换速度慢，内存、资源占用大|编程、调试复杂，可靠性较差

##### 选择

* 需要频繁创建销毁的优先用线程
* 需要进行大量计算的优先使用线程
* 强相关的处理用线程，弱相关的处理用进程
* 可能要扩展到多机分布的用进程，多核分布的用线程
* 都满足需求的情况下，用你最熟悉、最拿手的方式

> 多进程与多线程间的对比、优劣与选择来自：[多线程还是多进程的选择及区别](https://blog.csdn.net/lishenglong666/article/details/8557215)

### Linux 内核的同步方式

#### 原因

在现代操作系统里，同一时间可能有多个内核执行流在执行，因此内核其实像多进程多线程编程一样也需要一些同步机制来同步各执行单元对共享数据的访问。尤其是在多处理器系统上，更需要一些同步机制来同步不同处理器上的执行单元对共享的数据的访问。

#### 同步方式

* 原子操作
* 信号量（semaphore）
* 读写信号量（rw_semaphore）
* 自旋锁（spinlock）
* 大内核锁（BKL，Big Kernel Lock）
* 读写锁（rwlock）
* 大读者锁（brlock-Big Reader Lock）
* 读-拷贝修改(RCU，Read-Copy Update)
* 顺序锁（seqlock）

> 来自：[Linux 内核的同步机制，第 1 部分](https://www.ibm.com/developerworks/cn/linux/l-synch/part1/)、[Linux 内核的同步机制，第 2 部分](https://www.ibm.com/developerworks/cn/linux/l-synch/part2/)

### 死锁
定义：一组线程都在等在组内其他线程释放资源从而造成的无限等待
死锁产生的原因：
- 互斥访问
- 持有并等待
- 资源非抢占
- 循环等待
还有一种产生死锁的特殊情况是：**中断处理流程中使用互斥锁**，产生的情况分为以下两种
- 中断上下文中使用到了其他线程已经锁定的互斥锁
- 中断嵌套中两个中断互相持有锁，并等待对方的锁释放

#### 死锁的解决

**死锁预防是从源头设计避免死锁出现；死锁避免是运行时动态检查，避免死锁的出现**

**死锁预防**：
- 避免互斥访问：避免互斥访问的一个例子为：所有对临界区访问都通过一个代理线程来访问，缺点为大部分应用程序不容易修改成此模式
- 不允许持有并等待：要求线程在进入临界区前，一次性申请所有的资源，缺点是资源竞争程度高时，进入申请-释放的循环，造成资源利用率低，甚至饥饿情况
- 允许资源被强占：线程已经获取的锁可以被抢占掉，缺点是需要回滚拿到部分锁之后进行的操作，并在锁释放掉后进行恢复
- 避免循环等待：要求线程必须按照一定顺序来获取资源。

**死锁避免**
系统运行时，任意线程需要新的资源都必须向系统提出申请。而系统根据其分配后所处**安全或非安全状态**，判断是否能够将资源分配给线程

系统的两个状态：
- 安全状态：系统中至少存在一个安全序列，按照这个序列调度线程执行，即可避免资源不足的情况发生
- 非安全状态：如果系统中不存在一个安全序列，一定找不到一种分配资源的顺序让所有线程得到满足，因此必定会产生死锁

**银行家算法**：避免死锁算法的实现，其中定义的数据结构和算法如下：
- 保存当前资源的状态的数据结构：
  - 全局可利用资源:Available[M]，该数组代表某时刻系统中每类资源的可用个数
  - 每个线程的最大需求量:Max[N][M]，该矩阵包含所有N个线程对M类资源的最大需求量
  - 已分配资源数量: Allocation[N][M]，该矩阵包含已经分配给所有N个线程的M类资源数量。
  - 还需要的资源数量: Need[N][M].该矩阵包含所有N个线程对M类资源还需要的资源数量。
- 分配算法：
  - 首先对申请资源的线程**模拟分配**，计算出下一阶段的状态
  - 在下一状态中，找到当前剩余资源可以满足的一个线程，将资源分配给此线程，假设线程在拥有资源后短时间内执行完成，并收回所有的资源；并一直循环此动作，若所有的线程都可以运行完成则系统处于安全状态；允许分配
  - 若当前剩余资源不能满足任一线程条件，当前状态为不安全状态，不允许分配

### 文件系统

* Windows：FCB 表 + FAT + 位图
* Unix：inode + 混合索引 + 成组链接

#### 文件描述符 todo

### 主机字节序与网络字节序

#### 主机字节序（CPU 字节序）

##### 概念

主机字节序又叫 CPU 字节序，其不是由操作系统决定的，而是由 CPU 指令集架构决定的。主机字节序分为两种：

* 大端字节序（Big Endian）：高序字节存储在低位地址，低序字节存储在高位地址
* 小端字节序（Little Endian）：高序字节存储在高位地址，低序字节存储在低位地址

##### 存储方式

32 位整数 `0x12345678` 是从起始位置为 `0x00` 的地址开始存放，则：

内存地址 | 0x00 | 0x01 | 0x02 | 0x03
---|---|---|---|---
大端|12|34|56|78
小端|78|56|34|12

大端小端图片

![大端序](https://gitee.com/huihut/interview/raw/master/images/CPU-Big-Endian.svg.png)
![小端序](https://gitee.com/huihut/interview/raw/master/images/CPU-Little-Endian.svg.png)

##### 判断大端小端

判断大端小端

可以这样判断自己 CPU 字节序是大端还是小端：

```cpp
#include <iostream>
using namespace std;

int main()
{
	int i = 0x12345678;

	if (*((char*)&i) == 0x12)
		cout << "大端" << endl;
	else	
		cout << "小端" << endl;

	return 0;
}
```

##### 各架构处理器的字节序

* x86（Intel、AMD）、MOS Technology 6502、Z80、VAX、PDP-11 等处理器为小端序；
* Motorola 6800、Motorola 68000、PowerPC 970、System/370、SPARC（除 V9 外）等处理器为大端序；
* ARM（默认小端序）、PowerPC（除 PowerPC 970 外）、DEC Alpha、SPARC V9、MIPS、PA-RISC 及 IA64 的字节序是可配置的。

#### 网络字节序

网络字节顺序是 TCP/IP 中规定好的一种数据表示格式，它与具体的 CPU 类型、操作系统等无关，从而可以保证数据在不同主机之间传输时能够被正确解释。

网络字节顺序采用：大端（Big Endian）排列方式。

### 页面置换算法

在地址映射过程中，若在页面中发现所要访问的页面不在内存中，则产生缺页中断。当发生缺页中断时，如果操作系统内存中没有空闲页面，则操作系统必须在内存选择一个页面将其移出内存，以便为即将调入的页面让出空间。而用来选择淘汰哪一页的规则叫做页面置换算法。

#### 分类

* 全局置换：在整个内存空间置换
* 局部置换：在本进程中进行置换

#### 算法

全局：
* 工作集算法
* 缺页率置换算法

局部：
* 最佳置换算法（OPT）
* 先进先出置换算法（FIFO）
* 最近最久未使用（LRU）算法
* 时钟（Clock）置换算法

<a id="computer-network"></a>

## ☁️ 计算机网络

> 本节部分知识点来自《计算机网络（第 7 版）》

计算机网络体系结构：

![计算机网络体系结构](https://gitee.com/huihut/interview/raw/master/images/计算机网络体系结构.png)

### 各层作用及协议

分层 | 作用 | 协议
---|---|---
物理层 | 通过媒介传输比特，确定机械及电气规范（比特 Bit） | RJ45、CLOCK、IEEE802.3（中继器，集线器）
数据链路层|将比特组装成帧和点到点的传递（帧 Frame）| PPP、FR、HDLC、VLAN、MAC（网桥，交换机）
网络层|负责数据包从源到宿的传递和网际互连（包 Packet）|IP、ICMP、ARP、RARP、OSPF、IPX、RIP、IGRP（路由器）
运输层|提供端到端的可靠报文传递和错误恢复（ 段Segment）|TCP、UDP、SPX
会话层|建立、管理和终止会话（会话协议数据单元 SPDU）|NFS、SQL、NETBIOS、RPC
表示层|对数据进行翻译、加密和压缩（表示协议数据单元 PPDU）|JPEG、MPEG、ASII
应用层|允许访问OSI环境的手段（应用协议数据单元 APDU）|FTP、DNS、Telnet、SMTP、HTTP、WWW、NFS

### 五层小简介
// https://www.bilibili.com/video/BV19W4y1Q7sx
应用层：对应用程序的通信提供服务，支持各种网络应用。http ftp smtp pop3
运输层：提供端到端的传输服务，负责两台主机进程之间的通信，提供**可靠的**数据传输服务。提供流量控制和错误恢复 （提供复用分用） TCP UDP
网络层：负责数据包从源到目的端的传递和网络互联，**通信服务**，路由选择、流量控制、堵塞控制、差错控制 IP
数据链路层：把网络层传来的ip数据包**组装成帧**，在数据前后添加首部和尾部，功能：差错控制、流量控制
物理层：定义物理特性，机械电气规范

#### TCP

* TCP（Transmission Control Protocol，传输控制协议）是一种面向连接的、可靠的、基于字节流的传输层通信协议，其传输的单位是报文段。

特征：
* 面向连接
* 只能点对点（一对一）通信
* 可靠交互
* 全双工通信
* 面向字节流

TCP 如何保证可靠传输：
* 确认和超时重传
* 数据合理分片和排序
* 流量控制
* 拥塞控制
* 数据校验

TCP 如何保证可靠传输：
重传机制
流量控制
拥塞控制
数据校验

TCP 报文结构

![TCP 报文](https://gitee.com/huihut/interview/raw/master/images/TCP报文.png)

TCP 首部

![TCP 首部](https://gitee.com/huihut/interview/raw/master/images/TCP首部.png)

TCP：状态控制码（Code，Control Flag），占 6 比特，含义如下：
* URG：紧急比特（urgent），当 `URG＝1` 时，表明紧急指针字段有效，代表该封包为紧急封包。它告诉系统此报文段中有紧急数据，应尽快传送(相当于高优先级的数据)， 且上图中的 Urgent Pointer 字段也会被启用。
* ACK：确认比特（Acknowledge）。只有当 `ACK＝1` 时确认号字段才有效，代表这个封包为确认封包。当 `ACK＝0` 时，确认号无效。
* PSH：（Push function）若为 1 时，代表要求对方立即传送缓冲区内的其他对应封包，而无需等缓冲满了才送。
* RST：复位比特(Reset)，当 `RST＝1` 时，表明 TCP 连接中出现严重差错（如由于主机崩溃或其他原因），必须释放连接，然后再重新建立运输连接。
* SYN：同步比特(Synchronous)，SYN 置为 1，就表示这是一个连接请求或连接接受报文，通常带有 SYN 标志的封包表示『主动』要连接到对方的意思。
* FIN：终止比特(Final)，用来释放一个连接。当 `FIN＝1` 时，表明此报文段的发送端的数据已发送完毕，并要求释放运输连接。

#### UDP

* UDP（User Datagram Protocol，用户数据报协议）是 OSI（Open System Interconnection 开放式系统互联） 参考模型中一种无连接的传输层协议，提供面向事务的简单不可靠信息传送服务，其传输的单位是用户数据报。

特征：
* 无连接
* 尽最大努力交付
* 面向报文
* 没有拥塞控制
* 支持一对一、一对多、多对一、多对多的交互通信
* 首部开销小

#### TCP 与 UDP 的区别

1. TCP 面向连接，UDP 是无连接的；
2. TCP 提供可靠的服务，也就是说，通过 TCP 连接传送的数据，无差错，不丢失，不重复，且按序到达；UDP 尽最大努力交付，即不保证可靠交付
3. TCP 的逻辑通信信道是全双工的可靠信道；UDP 则是不可靠信道
5. 每一条 TCP 连接只能是点到点的；UDP 支持一对一，一对多，多对一和多对多的交互通信
6. TCP 面向字节流（可能出现黏包问题），实际上是 TCP 把数据看成一连串无结构的字节流；UDP 是面向报文的（不会出现黏包问题）
7. UDP 没有拥塞控制，因此网络出现拥塞不会使源主机的发送速率降低（对实时应用很有用，如 IP 电话，实时视频会议等）
8. TCP 首部开销20字节；UDP 的首部开销小，只有 8 个字节

#### TCP 黏包问题

##### 原因

TCP 是一个基于字节流的传输服务（UDP 基于报文的），“流” 意味着 TCP 所传输的数据是没有边界的。所以可能会出现两个数据包黏在一起的情况。

##### 解决

* 发送定长包。如果每个消息的大小都是一样的，那么在接收对等方只要累计接收数据，直到数据等于一个定长的数值就将它作为一个消息。
* 包头加上包体长度。包头是定长的 4 个字节，说明了包体的长度。接收对等方先接收包头长度，依据包头长度来接收包体。
* 在数据包之间设置边界，如添加特殊符号 `\r\n` 标记。FTP 协议正是这么做的。但问题在于如果数据正文中也含有 `\r\n`，则会误判为消息的边界。
* 使用更加复杂的应用层协议。

#### TCP 流量控制

##### 概念

流量控制（flow control）就是让发送方的发送速率不要太快，要让接收方来得及接收。

##### 方法

利用可变窗口进行流量控制

![](https://gitee.com/huihut/interview/raw/master/images/利用可变窗口进行流量控制举例.png)

#### TCP 拥塞控制

##### 概念

拥塞控制就是防止过多的数据注入到网络中，这样可以使网络中的路由器或链路不致过载。

##### 方法

* 慢开始( slow-start )
* 拥塞避免( congestion avoidance )
* 快重传( fast retransmit )
* 快恢复( fast recovery )

TCP的拥塞控制图

![](https://gitee.com/huihut/interview/raw/master/images/TCP拥塞窗口cwnd在拥塞控制时的变化情况.png)
![](https://gitee.com/huihut/interview/raw/master/images/快重传示意图.png)
![](https://gitee.com/huihut/interview/raw/master/images/TCP的拥塞控制流程图.png)

#### TCP 传输连接管理

> 因为 TCP 三次握手建立连接、四次挥手释放连接很重要，所以附上《计算机网络（第 7 版）-谢希仁》书中对此章的详细描述：<https://gitee.com/huihut/interview/raw/master/images/TCP-transport-connection-management.png>

##### TCP 三次握手建立连接

![UDP 报文](https://gitee.com/huihut/interview/raw/master/images/TCP三次握手建立连接.png)

【TCP 建立连接全过程解释】

1. 客户端发送 SYN 给服务器，说明客户端请求建立连接；
2. 服务端收到客户端发的 SYN，并回复 SYN+ACK 给客户端（同意建立连接）；
3. 客户端收到服务端的 SYN+ACK 后，回复 ACK 给服务端（表示客户端收到了服务端发的同意报文）；
4. 服务端收到客户端的 ACK，连接已建立，可以数据传输。

##### TCP 为什么要进行三次握手？

【答案一】因为信道不可靠，而 TCP 想在不可靠信道上建立可靠地传输，那么三次通信是理论上的最小值。（而 UDP 则不需建立可靠传输，因此 UDP 不需要三次握手。）

> [Google Groups . TCP 建立连接为什么是三次握手？{技术}{网络通信}](https://groups.google.com/forum/#!msg/pongba/kF6O7-MFxM0/5S7zIJ4yqKUJ)

【答案二】因为双方都需要确认对方收到了自己发送的序列号，确认过程最少要进行三次通信。

> [知乎 . TCP 为什么是三次握手，而不是两次或四次？](https://www.zhihu.com/question/24853633/answer/115173386)

【答案三】为了防止已失效的连接请求报文段突然又传送到了服务端，因而产生错误。

> [《计算机网络（第 7 版）-谢希仁》](https://gitee.com/huihut/interview/raw/master/images/TCP-transport-connection-management.png)

##### TCP 四次挥手释放连接

![UDP 报文](https://gitee.com/huihut/interview/raw/master/images/TCP四次挥手释放连接.png)

【TCP 释放连接全过程解释】

1. 客户端发送 FIN 给服务器，说明客户端不必发送数据给服务器了（请求释放从客户端到服务器的连接）；
2. 服务器接收到客户端发的 FIN，并回复 ACK 给客户端（同意释放从客户端到服务器的连接）；
3. 客户端收到服务端回复的 ACK，此时从客户端到服务器的连接已释放（但服务端到客户端的连接还未释放，并且客户端还可以接收数据）；
4. 服务端继续发送之前没发完的数据给客户端；
5. 服务端发送 FIN+ACK 给客户端，说明服务端发送完了数据（请求释放从服务端到客户端的连接，就算没收到客户端的回复，过段时间也会自动释放）；
6. 客户端收到服务端的 FIN+ACK，并回复 ACK 给服务端（同意释放从服务端到客户端的连接）；
7. 服务端收到客户端的 ACK 后，释放从服务端到客户端的连接。

##### TCP 为什么要进行四次挥手？

【问题一】TCP 为什么要进行四次挥手？ / 为什么 TCP 建立连接需要三次，而释放连接则需要四次？

【答案一】因为 TCP 是全双工模式，客户端请求关闭连接后，客户端向服务端的连接关闭（一二次挥手），服务端继续传输之前没传完的数据给客户端（数据传输），服务端向客户端的连接关闭（三四次挥手）。所以 TCP 释放连接时服务器的 ACK 和 FIN 是分开发送的（中间隔着数据传输），而 TCP 建立连接时服务器的 ACK 和 SYN 是一起发送的（第二次握手），所以 TCP 建立连接需要三次，而释放连接则需要四次。

【问题二】为什么 TCP 连接时可以 ACK 和 SYN 一起发送，而释放时则 ACK 和 FIN 分开发送呢？（ACK 和 FIN 分开是指第二次和第三次挥手）

【答案二】因为客户端请求释放时，服务器可能还有数据需要传输给客户端，因此服务端要先响应客户端 FIN 请求（服务端发送 ACK），然后数据传输，传输完成后，服务端再提出 FIN 请求（服务端发送 FIN）；而连接时则没有中间的数据传输，因此连接时可以 ACK 和 SYN 一起发送。

【问题三】为什么客户端释放最后需要 TIME-WAIT 等待 2MSL 呢？

【答案三】

1. 为了保证客户端发送的最后一个 ACK 报文能够到达服务端。若未成功到达，则服务端超时重传 FIN+ACK 报文段，客户端再重传 ACK，并重新计时。
2. 防止已失效的连接请求报文段出现在本连接中。TIME-WAIT 持续 2MSL 可使本连接持续的时间内所产生的所有报文段都从网络中消失，这样可使下次连接中不会出现旧的连接报文段。

### 既然 IP 层会分片，为什么 TCP 层还需要 MSS 呢？
引入两个概念
MTU（Maximum Transmission Unit）：链路层定义的最大网络传输数据包的大小
MSS（Maximum Segment Size）：TCP协议定义的一个报文段能承载的最大单位

如果IP层有一个数据报要传，而且数据帧的长度比链路层的MTU还大，那么IP层就需要进行分片( fragmentation)，即把数据报分成干片，这样每一片就都小于MTU，目标端需要对数据包进行重新组装。因为**IP层是没有超时重传机制**，当一个包出现丢包的情况下，会重发所有的包，所以**IP层提供的分片并不好用**

为了能达到最佳的传输效果，TCP协议中在建立连接的时候就会根据链路层的MTU进行协商MSS值（MSS = MTU - IP报头 - TCP报头），当TCP层发现数据超过MSS后，就在TCP层进行分片，在TCP进行的分片丢失后，可以进行单个分片重传


### 应用层

#### DNS

* DNS（Domain Name System，域名系统）是互联网的一项服务。它作为将域名和 IP 地址相互映射的一个分布式数据库，能够使人更方便地访问互联网。DNS 使用 TCP 和 UDP 端口 53。当前，对于每一级域名长度的限制是 63 个字符，域名总长度则不能超过 253 个字符。

域名：
* `域名 ::= {<三级域名>.<二级域名>.<顶级域名>}`，如：`blog.huihut.com`

#### FTP

* FTP（File Transfer Protocol，文件传输协议）是用于在网络上进行文件传输的一套标准协议，使用客户/服务器模式，使用 TCP 数据报，提供交互式访问，双向传输。
* TFTP（Trivial File Transfer Protocol，简单文件传输协议）一个小且易实现的文件传输协议，也使用客户-服务器方式，使用UDP数据报，只支持文件传输而不支持交互，没有列目录，不能对用户进行身份鉴定

#### TELNET

* TELNET 协议是 TCP/IP 协议族中的一员，是 Internet 远程登陆服务的标准协议和主要方式。它为用户提供了在本地计算机上完成远程主机工作的能力。

* HTTP（HyperText Transfer Protocol，超文本传输协议）是用于从 WWW（World Wide Web，万维网）服务器传输超文本到本地浏览器的传送协议。

* SMTP（Simple Mail Transfer Protocol，简单邮件传输协议）是一组用于由源地址到目的地址传送邮件的规则，由它来控制信件的中转方式。SMTP 协议属于 TCP/IP 协议簇，它帮助每台计算机在发送或中转信件时找到下一个目的地。
* Socket 建立网络通信连接至少要一对端口号（Socket）。Socket 本质是编程接口（API），对 TCP/IP 的封装，TCP/IP 也要提供可供程序员做网络开发所用的接口，这就是 Socket 编程接口。

#### WWW

* WWW（World Wide Web，环球信息网，万维网）是一个由许多互相链接的超文本组成的系统，通过互联网访问

##### URL

* URL（Uniform Resource Locator，统一资源定位符）是因特网上标准的资源的地址（Address）

标准格式：

* `协议类型:[//服务器地址[:端口号]][/资源层级UNIX文件路径]文件名[?查询][#片段ID]`
    
完整格式：

* `协议类型:[//[访问资源需要的凭证信息@]服务器地址[:端口号]][/资源层级UNIX文件路径]文件名[?查询][#片段ID]`

> 其中【访问凭证信息@；:端口号；?查询；#片段ID】都属于选填项  
> 如：`https://github.com/huihut/interview#cc`

##### HTTP

HTTP（HyperText Transfer Protocol，超文本传输协议）是一种用于分布式、协作式和超媒体信息系统的应用层协议。HTTP 是万维网的数据通信的基础。

请求方法

方法 | 意义
--- | ---
OPTIONS | 请求一些选项信息，允许客户端查看服务器的性能
GET | 请求指定的页面信息，并返回实体主体
HEAD | 类似于 get 请求，只不过返回的响应中没有具体的内容，用于获取报头
POST | 向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST请求可能会导致新的资源的建立和/或已有资源的修改
PUT | 从客户端向服务器传送的数据取代指定的文档的内容
DELETE | 请求服务器删除指定的页面
TRACE | 回显服务器收到的请求，主要用于测试或诊断

状态码（Status-Code）

* 1xx：表示通知信息，如请求收到了或正在进行处理
    * 100 Continue：继续，客户端应继续其请求
    * 101 Switching Protocols 切换协议。服务器根据客户端的请求切换协议。只能切换到更高级的协议，例如，切换到 HTTP 的新版本协议
* 2xx：表示成功，如接收或知道了
    * 200 OK: 请求成功
* 3xx：表示重定向，如要完成请求还必须采取进一步的行动
    * 301 Moved Permanently: 永久移动。请求的资源已被永久的移动到新 URL，返回信息会包括新的 URL，浏览器会自动定向到新 URL。今后任何新的请求都应使用新的 URL 代替
* 4xx：表示客户的差错，如请求中有错误的语法或不能完成
    * 400 Bad Request: 客户端请求的语法错误，服务器无法理解
    * 401 Unauthorized: 请求要求用户的身份认证
    * 403 Forbidden: 服务器理解请求客户端的请求，但是拒绝执行此请求（权限不够）
    * 404 Not Found: 服务器无法根据客户端的请求找到资源（网页）。通过此代码，网站设计人员可设置 “您所请求的资源无法找到” 的个性页面
    * 408 Request Timeout: 服务器等待客户端发送的请求时间过长，超时
* 5xx：表示服务器的差错，如服务器失效无法完成请求
    * 500 Internal Server Error: 服务器内部错误，无法完成请求
    * 503 Service Unavailable: 由于超载或系统维护，服务器暂时的无法处理客户端的请求。延时的长度可包含在服务器的 Retry-After 头信息中
    * 504 Gateway Timeout: 充当网关或代理的服务器，未及时从远端服务器获取请求

> 更多状态码：[菜鸟教程 . HTTP状态码](http://www.runoob.com/http/http-status-codes.html)

##### 其他协议

* SMTP（Simple Main Transfer Protocol，简单邮件传输协议）是在 Internet 传输 Email 的标准，是一个相对简单的基于文本的协议。在其之上指定了一条消息的一个或多个接收者（在大多数情况下被确认是存在的），然后消息文本会被传输。可以很简单地通过 Telnet 程序来测试一个 SMTP 服务器。SMTP 使用 TCP 端口 25。
* DHCP（Dynamic Host Configuration Protocol，动态主机设置协议）是一个局域网的网络协议，使用 UDP 协议工作，主要有两个用途：
    * 用于内部网络或网络服务供应商自动分配 IP 地址给用户
    * 用于内部网络管理员作为对所有电脑作中央管理的手段
* SNMP（Simple Network Management Protocol，简单网络管理协议）构成了互联网工程工作小组（IETF，Internet Engineering Task Force）定义的 Internet 协议族的一部分。该协议能够支持网络管理系统，用以监测连接到网络上的设备是否有任何引起管理上关注的情况。


#### http和https

HTTPS 在 HTTP 与 TCP 层之间加入了 SSL/TLS 协议，可以很好的解决了上述的风险：

* 信息加密：交互信息无法被窃取，但你的号会因为「自身忘记」账号而没。
* 校验机制：无法篡改通信内容，篡改了就不能正常显示，但百度「竞价排名」依然可以搜索垃圾广告。
* 身份证书：证明淘宝是真的淘宝网，但你的钱还是会因为「剁手」而没

HTTP 与 HTTPS 有哪些区别？
* HTTP 是超文本传输协议，信息是明文传输，存在安全风险的问题。HTTPS 则解决 HTTP 不安全的缺陷，在 TCP 和 HTTP 网络层之间加入了 SSL/TLS 安全协议，使得报文能够加密传输。

* HTTP 连接建立相对简单， TCP 三次握手之后便可进行 HTTP 的报文传输。而 HTTPS 在 TCP 三次握手之后，还需进行 SSL/TLS 的握手过程，才可进入加密报文传输。

* 两者的默认端口不一样，HTTP 默认端口号是 80，HTTPS 默认端口号是 443。

* HTTPS 协议需要向 CA（证书权威机构）申请数字证书，来保证服务器的身份是可信的。

#

<a id="network-programming"></a>

## 🌩 网络编程

### Socket

> [Linux Socket 编程（不限 Linux）](https://www.cnblogs.com/skynet/archive/2010/12/12/1903949.html)

![Socket 客户端服务器通讯](https://gitee.com/huihut/interview/raw/master/images/socket客户端服务器通讯.jpg)


#### Socket 中的 read()、write() 函数

```cpp
ssize_t read(int fd, void *buf, size_t count);
ssize_t write(int fd, const void *buf, size_t count);
```

##### read()

* read 函数是负责从 fd 中读取内容。
* 当读成功时，read 返回实际所读的字节数。
* 如果返回的值是 0 表示已经读到文件的结束了，小于 0 表示出现了错误。
* 如果错误为 EINTR 说明读是由中断引起的；如果是 ECONNREST 表示网络连接出了问题。

##### write()

* write 函数将 buf 中的 nbytes 字节内容写入文件描述符 fd。
* 成功时返回写的字节数。失败时返回 -1，并设置 errno 变量。
* 在网络程序中，当我们向套接字文件描述符写时有俩种可能。
* （1）write 的返回值大于 0，表示写了部分或者是全部的数据。
* （2）返回的值小于 0，此时出现了错误。
* 如果错误为 EINTR 表示在写的时候出现了中断错误；如果为 EPIPE 表示网络连接出现了问题（对方已经关闭了连接）。

#### Socket 中 TCP 的三次握手建立连接

我们知道 TCP 建立连接要进行 “三次握手”，即交换三个分组。大致流程如下：

1. 客户端向服务器发送一个 SYN J
2. 服务器向客户端响应一个 SYN K，并对 SYN J 进行确认 ACK J+1
3. 客户端再想服务器发一个确认 ACK K+1

只有就完了三次握手，但是这个三次握手发生在 Socket 的那几个函数中呢？请看下图：

![socket 中发送的 TCP 三次握手](http://images.cnblogs.com/cnblogs_com/skynet/201012/201012122157467258.png)

从图中可以看出：
1. 当客户端调用 connect 时，触发了连接请求，向服务器发送了 SYN J 包，这时 connect 进入阻塞状态；  
2. 服务器监听到连接请求，即收到 SYN J 包，调用 accept 函数接收请求向客户端发送 SYN K ，ACK J+1，这时 accept 进入阻塞状态；  
3. 客户端收到服务器的 SYN K ，ACK J+1 之后，这时 connect 返回，并对 SYN K 进行确认；  
4. 服务器收到 ACK K+1 时，accept 返回，至此三次握手完毕，连接建立。

#### Socket 中 TCP 的四次握手释放连接

上面介绍了 socket 中 TCP 的三次握手建立过程，及其涉及的 socket 函数。现在我们介绍 socket 中的四次握手释放连接的过程，请看下图：

![socket 中发送的 TCP 四次握手](http://images.cnblogs.com/cnblogs_com/skynet/201012/201012122157487616.png)

图示过程如下：

1. 某个应用进程首先调用 close 主动关闭连接，这时 TCP 发送一个 FIN M；
2. 另一端接收到 FIN M 之后，执行被动关闭，对这个 FIN 进行确认。它的接收也作为文件结束符传递给应用进程，因为 FIN 的接收意味着应用进程在相应的连接上再也接收不到额外数据；
3. 一段时间之后，接收到文件结束符的应用进程调用 close 关闭它的 socket。这导致它的 TCP 也发送一个 FIN N；
4. 接收到这个 FIN 的源发送端 TCP 对它进行确认。

这样每个方向上都有一个 FIN 和 ACK。

<a id="database"></a>



<a id="design-pattern"></a>

## 📏 设计模式

> 各大设计模式例子参考：[CSDN专栏 . C++ 设计模式](https://blog.csdn.net/liang19890820/article/details/66974516) 系列博文

[设计模式工程目录](DesignPattern)

### 单例模式
让你能够保证一个类只有一个实例， 并提供一个访问该实例的方法。
使用案例：服务器的配置放在一个文件中，配置类可以设计为单例模式，所有的其他服务通过单例模式访问到这个单一实体上
使用local static变量
[单例模式例子](DesignPattern/SingletonPattern)

### 工厂模式
工厂模式提供了一种将对象的实例化过程封装在工厂类中的方式。通过使用工厂模式，可以将对象的创建与使用代码分离，提供一种统一的接口来创建不同类型的对象。

### 抽象工厂模式
让你能创建一系列相关的对象， 而无需指定其具体类。
[抽象工厂模式例子](DesignPattern/AbstractFactoryPattern)

### 适配器模式
适配器模式能使接口不兼容的对象能够相互合作。
举例：读卡器是作为内存卡和笔记本之间的适配器。
[适配器模式例子](DesignPattern/AdapterPattern)

### 桥接模式
可将一个大类或一系列紧密相关的类拆分为抽象和实现两个独立的层次结构， 从而能在开发时分别使用。
[桥接模式例子](DesignPattern/BridgePattern)

### 装饰器模式
允许你通过将对象放入包含行为的特殊封装对象中来为原对象绑定新的行为。

### 观察者模式
观察者模式定义了一种订阅机制，允许在对象事件发生时通知多个“观察”该对象的其他对象
[观察者模式例子](DesignPattern/ObserverPattern)

### 设计模式的六大原则

* 单一职责原则（SRP，Single Responsibility Principle）
* 里氏替换原则（LSP，Liskov Substitution Principle）
* 依赖倒置原则（DIP，Dependence Inversion Principle）
* 接口隔离原则（ISP，Interface Segregation Principle）
* 迪米特法则（LoD，Law of Demeter）
* 开放封闭原则（OCP，Open Close Principle）

## docker
docker使用linux的命名空间来隔离每个进程，使进程间不可互见，减少影响
对于每个进程会提供一个虚拟的文件系统，防止对真实的其他进程进行控制
Linux的cgroup负责资源的管理

我们使用docker一个最大优点是可以提供不同的运行环境，比如不同版本的
然后环境隔离，
备份、测试

<a id="link-loading-library"></a>

## ⚙️ 链接装载库

> 本节部分知识点来自《程序员的自我修养——链接装载库》

### 内存、栈、堆

一般应用程序内存空间有如下区域：

* 栈：由操作系统自动分配释放，存放函数的参数值、局部变量等的值，用于维护函数调用的上下文
* 堆：一般由程序员分配释放，若程序员不释放，程序结束时可能由操作系统回收，用来容纳应用程序动态分配的内存区域
* 可执行文件映像：存储着可执行文件在内存中的映像，由装载器装载是将可执行文件的内存读取或映射到这里
* 保留区：保留区并不是一个单一的内存区域，而是对内存中受到保护而禁止访问的内存区域的总称，如通常 C 语言讲无效指针赋值为 0（NULL），因此 0 地址正常情况下不可能有效的访问数据

#### 栈

栈保存了一个函数调用所需要的维护信息，常被称为堆栈帧（Stack Frame）或活动记录（Activate Record），一般包含以下几方面：

* 函数的返回地址和参数
* 临时变量：包括函数的非静态局部变量以及编译器自动生成的其他临时变量
* 保存上下文：包括函数调用前后需要保持不变的寄存器

#### 堆

堆分配算法：

* 空闲链表（Free List）
* 位图（Bitmap）
* 对象池

#### “段错误（segment fault）” 或 “非法操作，该内存地址不能 read/write”

典型的非法指针解引用造成的错误。当指针指向一个不允许读写的内存地址，而程序却试图利用指针来读或写该地址时，会出现这个错误。

普遍原因：

* 将指针初始化为 NULL，之后没有给它一个合理的值就开始使用指针
* 没用初始化栈中的指针，指针的值一般会是随机数，之后就直接开始使用指针

### 编译链接

#### 各平台文件格式

平台 | 可执行文件 | 目标文件 | 动态库/共享对象 | 静态库
---|---|---|---|---
Windows|exe|obj|dll|lib
Unix/Linux|ELF、out|o|so|a
Mac|Mach-O|o|dylib、tbd、framework|a、framework

#### 编译链接过程

1. 预编译（预编译器处理如 `#include`、`#define` 等预编译指令，生成 `.i` 或 `.ii` 文件）
2. 编译（编译器进行词法分析、语法分析、语义分析、中间代码生成、目标代码生成、优化，生成 `.s` 文件）
3. 汇编（汇编器把汇编码翻译成机器码，生成 `.o` 文件）
4. 链接（连接器进行地址和空间分配、符号决议、重定位，生成 `.out` 文件）

> 现在版本 GCC 把预编译和编译合成一步，预编译编译程序 cc1、汇编器 as、连接器 ld

> MSVC 编译环境，编译器 cl、连接器 link、可执行文件查看器 dumpbin

#### 目标文件

编译器编译源代码后生成的文件叫做目标文件。目标文件从结构上讲，它是已经编译后的可执行文件格式，只是还没有经过链接的过程，其中可能有些符号或有些地址还没有被调整。

> 可执行文件（Windows 的 `.exe` 和 Linux 的 `ELF`）、动态链接库（Windows 的 `.dll` 和 Linux 的 `.so`）、静态链接库（Windows 的 `.lib` 和 Linux 的 `.a`）都是按照可执行文件格式存储（Windows 按照 PE-COFF，Linux 按照 ELF）

##### 目标文件格式

* Windows 的 PE（Portable Executable），或称为 PE-COFF，`.obj` 格式
* Linux 的 ELF（Executable Linkable Format），`.o` 格式
* Intel/Microsoft 的 OMF（Object Module Format）
* Unix 的 `a.out` 格式
* MS-DOS 的 `.COM` 格式

> PE 和 ELF 都是 COFF（Common File Format）的变种

##### 目标文件存储结构

段 | 功能
--- | ---
File Header | 文件头，描述整个文件的文件属性（包括文件是否可执行、是静态链接或动态连接及入口地址、目标硬件、目标操作系统等）
.text section | 代码段，执行语句编译成的机器代码 
.data section | 数据段，已初始化的全局变量和局部静态变量
.bss section | BSS 段（Block Started by Symbol），未初始化的全局变量和局部静态变量（因为默认值为 0，所以只是在此预留位置，不占空间）
.rodata section | 只读数据段，存放只读数据，一般是程序里面的只读变量（如 const 修饰的变量）和字符串常量
.comment section | 注释信息段，存放编译器版本信息
.note.GNU-stack section | 堆栈提示段 

> 其他段略

#### 链接的接口————符号

在链接中，目标文件之间相互拼合实际上是目标文件之间对地址的引用，即对函数和变量的地址的引用。我们将函数和变量统称为符号（Symbol），函数名或变量名就是符号名（Symbol Name）。

如下符号表（Symbol Table）：

Symbol（符号名） | Symbol Value （地址）
--- | ---
main| 0x100
Add | 0x123
... | ...

### Linux 的共享库（Shared Library）

Linux 下的共享库就是普通的 ELF 共享对象。

共享库版本更新应该保证二进制接口 ABI（Application Binary Interface）的兼容

#### 命名

`libname.so.x.y.z`

* x：主版本号，不同主版本号的库之间不兼容，需要重新编译
* y：次版本号，高版本号向后兼容低版本号
* z：发布版本号，不对接口进行更改，完全兼容

#### 路径

大部分包括 Linux 在内的开源系统遵循 FHS（File Hierarchy Standard）的标准，这标准规定了系统文件如何存放，包括各个目录结构、组织和作用。

* `/lib`：存放系统最关键和最基础的共享库，如动态链接器、C 语言运行库、数学库等
* `/usr/lib`：存放非系统运行时所需要的关键性的库，主要是开发库
* `/usr/local/lib`：存放跟操作系统本身并不十分相关的库，主要是一些第三方应用程序的库

> 动态链接器会在 `/lib`、`/usr/lib` 和由 `/etc/ld.so.conf` 配置文件指定的，目录中查找共享库

#### 环境变量

* `LD_LIBRARY_PATH`：临时改变某个应用程序的共享库查找路径，而不会影响其他应用程序
* `LD_PRELOAD`：指定预先装载的一些共享库甚至是目标文件
* `LD_DEBUG`：打开动态链接器的调试功能

#### so 共享库的编写

使用 CLion 编写共享库

创建一个名为 MySharedLib 的共享库

CMakeLists.txt

```cmake
cmake_minimum_required(VERSION 3.10)
project(MySharedLib)

set(CMAKE_CXX_STANDARD 11)

add_library(MySharedLib SHARED library.cpp library.h)
```

library.h

```cpp
#ifndef MYSHAREDLIB_LIBRARY_H
#define MYSHAREDLIB_LIBRARY_H

// 打印 Hello World!
void hello();

// 使用可变模版参数求和
template <typename T>
T sum(T t)
{
    return t;
}
template <typename T, typename ...Types>
T sum(T first, Types ... rest)
{
    return first + sum<T>(rest...);
}

#endif
```

library.cpp

```cpp
#include <iostream>
#include "library.h"

void hello() {
    std::cout << "Hello, World!" << std::endl;
}
```

#### so 共享库的使用（被可执行项目调用）

使用 CLion 调用共享库

创建一个名为 TestSharedLib 的可执行项目

CMakeLists.txt

```cmake
cmake_minimum_required(VERSION 3.10)
project(TestSharedLib)

# C++11 编译
set(CMAKE_CXX_STANDARD 11)

# 头文件路径
set(INC_DIR /home/xx/code/clion/MySharedLib)
# 库文件路径
set(LIB_DIR /home/xx/code/clion/MySharedLib/cmake-build-debug)

include_directories(${INC_DIR})
link_directories(${LIB_DIR})
link_libraries(MySharedLib)

add_executable(TestSharedLib main.cpp)

# 链接 MySharedLib 库
target_link_libraries(TestSharedLib MySharedLib)
```

main.cpp

```cpp
#include <iostream>
#include "library.h"
using std::cout;
using std::endl;

int main() {

    hello();
    cout << "1 + 2 = " << sum(1,2) << endl;
    cout << "1 + 2 + 3 = " << sum(1,2,3) << endl;

    return 0;
}
```

执行结果

```
Hello, World!
1 + 2 = 3
1 + 2 + 3 = 6
```

### Windows 应用程序入口函数

* GUI（Graphical User Interface）应用，链接器选项：`/SUBSYSTEM:WINDOWS`
* CUI（Console User Interface）应用，链接器选项：`/SUBSYSTEM:CONSOLE`

_tWinMain 与 _tmain 函数声明

```cpp
Int WINAPI _tWinMain(
    HINSTANCE hInstanceExe,
    HINSTANCE,
    PTSTR pszCmdLine,
    int nCmdShow);

int _tmain(
    int argc,
    TCHAR *argv[],
    TCHAR *envp[]);
```

应用程序类型|入口点函数|嵌入可执行文件的启动函数
---|---|---
处理ANSI字符（串）的GUI应用程序|_tWinMain(WinMain)|WinMainCRTSartup
处理Unicode字符（串）的GUI应用程序|_tWinMain(wWinMain)|wWinMainCRTSartup
处理ANSI字符（串）的CUI应用程序|_tmain(Main)|mainCRTSartup
处理Unicode字符（串）的CUI应用程序|_tmain(wMain)|wmainCRTSartup
动态链接库（Dynamic-Link Library）|DllMain|_DllMainCRTStartup 

### Windows 的动态链接库（Dynamic-Link Library）

> 部分知识点来自《Windows 核心编程（第五版）》

#### 用处

* 扩展了应用程序的特性
* 简化了项目管理
* 有助于节省内存
* 促进了资源的共享
* 促进了本地化
* 有助于解决平台间的差异
* 可以用于特殊目的

#### 注意

* 创建 DLL，事实上是在创建可供一个可执行模块调用的函数
* 当一个模块提供一个内存分配函数（malloc、new）的时候，它必须同时提供另一个内存释放函数（free、delete）
* 在使用 C 和 C++ 混编的时候，要使用 extern "C" 修饰符
* 一个 DLL 可以导出函数、变量（避免导出）、C++ 类（导出导入需要同编译器，否则避免导出）
* DLL 模块：cpp 文件中的 __declspec(dllexport) 写在 include 头文件之前
* 调用 DLL 的可执行模块：cpp 文件的 __declspec(dllimport) 之前不应该定义 MYLIBAPI

#### 加载 Windows 程序的搜索顺序

1. 包含可执行文件的目录
2. Windows 的系统目录，可以通过 GetSystemDirectory 得到
3. 16 位的系统目录，即 Windows 目录中的 System 子目录
4. Windows 目录，可以通过 GetWindowsDirectory 得到
5. 进程的当前目录
6. PATH 环境变量中所列出的目录

#### DLL 入口函数

DllMain 函数

```cpp
BOOL WINAPI DllMain(HINSTANCE hinstDLL, DWORD fdwReason, LPVOID lpvReserved)
{
    switch(fdwReason)
    {
    case DLL_PROCESS_ATTACH:
        // 第一次将一个DLL映射到进程地址空间时调用
        // The DLL is being mapped into the process' address space.
        break;
    case DLL_THREAD_ATTACH:
        // 当进程创建一个线程的时候，用于告诉DLL执行与线程相关的初始化（非主线程执行）
        // A thread is bing created.
        break;
    case DLL_THREAD_DETACH:
        // 系统调用 ExitThread 线程退出前，即将终止的线程通过告诉DLL执行与线程相关的清理
        // A thread is exiting cleanly.
        break;
    case DLL_PROCESS_DETACH:
        // 将一个DLL从进程的地址空间时调用
        // The DLL is being unmapped from the process' address space.
        break;
    }
    return (TRUE); // Used only for DLL_PROCESS_ATTACH
}
```

#### 载入卸载库

LoadLibrary、LoadLibraryExA、LoadPackagedLibrary、FreeLibrary、FreeLibraryAndExitThread 函数声明

```cpp
// 载入库
HMODULE WINAPI LoadLibrary(
  _In_ LPCTSTR lpFileName
);
HMODULE LoadLibraryExA(
  LPCSTR lpLibFileName,
  HANDLE hFile,
  DWORD  dwFlags
);
// 若要在通用 Windows 平台（UWP）应用中加载 Win32 DLL，需要调用 LoadPackagedLibrary，而不是 LoadLibrary 或 LoadLibraryEx
HMODULE LoadPackagedLibrary(
  LPCWSTR lpwLibFileName,
  DWORD   Reserved
);

// 卸载库
BOOL WINAPI FreeLibrary(
  _In_ HMODULE hModule
);
// 卸载库和退出线程
VOID WINAPI FreeLibraryAndExitThread(
  _In_ HMODULE hModule,
  _In_ DWORD   dwExitCode
);
```

#### 显示地链接到导出符号

GetProcAddress 函数声明

```cpp
FARPROC GetProcAddress(
  HMODULE hInstDll,
  PCSTR pszSymbolName  // 只能接受 ANSI 字符串，不能是 Unicode
);
```

#### DumpBin.exe 查看 DLL 信息

在 `VS 的开发人员命令提示符` 使用 `DumpBin.exe` 可查看 DLL 库的导出段（导出的变量、函数、类名的符号）、相对虚拟地址（RVA，relative virtual address）。如：
```
DUMPBIN -exports D:\mydll.dll
```

#### LoadLibrary 与 FreeLibrary 流程图

LoadLibrary 与 FreeLibrary 流程图

##### LoadLibrary

![WindowsLoadLibrary](https://gitee.com/huihut/interview/raw/master/images/WindowsLoadLibrary.png)

##### FreeLibrary

![WindowsFreeLibrary](https://gitee.com/huihut/interview/raw/master/images/WindowsFreeLibrary.png)

#### DLL 库的编写（导出一个 DLL 模块）

DLL 库的编写（导出一个 DLL 模块）
DLL 头文件

```cpp
// MyLib.h

#ifdef MYLIBAPI

// MYLIBAPI 应该在全部 DLL 源文件的 include "Mylib.h" 之前被定义
// 全部函数/变量正在被导出

#else

// 这个头文件被一个exe源代码模块包含，意味着全部函数/变量被导入
#define MYLIBAPI extern "C" __declspec(dllimport)

#endif

// 这里定义任何的数据结构和符号

// 定义导出的变量（避免导出变量）
MYLIBAPI int g_nResult;

// 定义导出函数原型
MYLIBAPI int Add(int nLeft, int nRight);
```

DLL 源文件

```cpp
// MyLibFile1.cpp

// 包含标准Windows和C运行时头文件
#include <windows.h>

// DLL源码文件导出的函数和变量
#define MYLIBAPI extern "C" __declspec(dllexport)

// 包含导出的数据结构、符号、函数、变量
#include "MyLib.h"

// 将此DLL源代码文件的代码放在此处
int g_nResult;

int Add(int nLeft, int nRight)
{
    g_nResult = nLeft + nRight;
    return g_nResult;
}
```

#### DLL 库的使用（运行时动态链接 DLL）

DLL 库的使用（运行时动态链接 DLL）

```cpp
// A simple program that uses LoadLibrary and 
// GetProcAddress to access myPuts from Myputs.dll. 
 
#include <windows.h> 
#include <stdio.h> 
 
typedef int (__cdecl *MYPROC)(LPWSTR); 
 
int main( void ) 
{ 
    HINSTANCE hinstLib; 
    MYPROC ProcAdd; 
    BOOL fFreeResult, fRunTimeLinkSuccess = FALSE; 
 
    // Get a handle to the DLL module.
 
    hinstLib = LoadLibrary(TEXT("MyPuts.dll")); 
 
    // If the handle is valid, try to get the function address.
 
    if (hinstLib != NULL) 
    { 
        ProcAdd = (MYPROC) GetProcAddress(hinstLib, "myPuts"); 
 
        // If the function address is valid, call the function.
 
        if (NULL != ProcAdd) 
        {
            fRunTimeLinkSuccess = TRUE;
            (ProcAdd) (L"Message sent to the DLL function\n"); 
        }
        // Free the DLL module.
 
        fFreeResult = FreeLibrary(hinstLib); 
    } 

    // If unable to call the DLL function, use an alternative.
    if (! fRunTimeLinkSuccess) 
        printf("Message printed from executable\n"); 

    return 0;
}
```

### 运行库（Runtime Library）

#### 典型程序运行步骤

1. 操作系统创建进程，把控制权交给程序的入口（往往是运行库中的某个入口函数）
2. 入口函数对运行库和程序运行环境进行初始化（包括堆、I/O、线程、全局变量构造等等）。
3. 入口函数初始化后，调用 main 函数，正式开始执行程序主体部分。
4. main 函数执行完毕后，返回到入口函数进行清理工作（包括全局变量析构、堆销毁、关闭I/O等），然后进行系统调用结束进程。

> 一个程序的 I/O 指代程序与外界的交互，包括文件、管程、网络、命令行、信号等。更广义地讲，I/O 指代操作系统理解为 “文件” 的事物。

#### glibc 入口

`_start -> __libc_start_main -> exit -> _exit`

其中 `main(argc, argv, __environ)` 函数在 `__libc_start_main` 里执行。

#### MSVC CRT 入口

`int mainCRTStartup(void)`

执行如下操作：

1. 初始化和 OS 版本有关的全局变量。
2. 初始化堆。
3. 初始化 I/O。
4. 获取命令行参数和环境变量。
5. 初始化 C 库的一些数据。
6. 调用 main 并记录返回值。
7. 检查错误并将 main 的返回值返回。

#### C 语言运行库（CRT）

大致包含如下功能：

* 启动与退出：包括入口函数及入口函数所依赖的其他函数等。
* 标准函数：有 C 语言标准规定的C语言标准库所拥有的函数实现。
* I/O：I/O 功能的封装和实现。
* 堆：堆的封装和实现。
* 语言实现：语言中一些特殊功能的实现。
* 调试：实现调试功能的代码。

#### C语言标准库（ANSI C）

包含：

* 标准输入输出（stdio.h）
* 文件操作（stdio.h）
* 字符操作（ctype.h）
* 字符串操作（string.h）
* 数学函数（math.h）
* 资源管理（stdlib.h）
* 格式转换（stdlib.h）
* 时间/日期（time.h）
* 断言（assert.h）
* 各种类型上的常数（limits.h & float.h）
* 变长参数（stdarg.h）
* 非局部跳转（setjmp.h）

<a id="books"></a>

## 📚 书籍

> [huihut/CS-Books](https://github.com/huihut/CS-Books)：📚 Computer Science Books 计算机技术类书籍 PDF

### 语言

* 《C++ Primer》
* 《Effective C++》
* 《More Effective C++》
* 《深度探索 C++ 对象模型》
* 《深入理解 C++11》
* 《STL 源码剖析》

### 算法

* 《剑指 Offer》
* 《编程珠玑》
* 《程序员面试宝典》

### 系统

* 《深入理解计算机系统》
* 《Windows 核心编程》
* 《Unix 环境高级编程》

### 网络

* 《Unix 网络编程》
* 《TCP/IP 详解》

### 其他

* 《程序员的自我修养》

<a id="cc-development-direction"></a>

## 🔱 C/C++ 发展方向

> C/C++ 发展方向甚广，包括不限于以下方向， 以下列举一些大厂校招岗位要求。

### 后台/服务器

【后台开发】

* 编程基本功扎实，掌握 C/C++/JAVA 等开发语言、常用算法和数据结构；
* 熟悉 TCP/UDP 网络协议及相关编程、进程间通讯编程；
* 了解 Python、Shell、Perl 等脚本语言；
* 了解 MYSQL 及 SQL 语言、编程，了解 NoSQL, key-value 存储原理；
* 全面、扎实的软件知识结构，掌握操作系统、软件工程、设计模式、数据结构、数据库系统、网络安全等专业知识；
* 了解分布式系统设计与开发、负载均衡技术，系统容灾设计，高可用系统等知识。

### 桌面客户端

【PC 客户端开发】

* 计算机软件相关专业本科或以上学历，热爱编程，基础扎实，理解算法和数据结构相关知识；  
* 熟悉 windows 操作系统的内存管理、文件系统、进程线程调度； 
* 熟悉 MFC/windows 界面实现机制，熟练使用 VC，精通 C/C++，熟练使用 STL，以及 Windows 下网络编程经验；
* 熟练掌握 Windows 客户端开发、调试，有 Windows 应用软件开发经验优先；
* 对于创新及解决具有挑战性的问题充满激情，具有良好的算法基础及系统分析能力。

### 图形学/游戏/VR/AR

【游戏客户端开发】

* 计算机科学/工程相关专业本科或以上学历，热爱编程，基础扎实，理解算法、数据结构、软件设计相关知识；
* 至少掌握一种游戏开发常用的编程语言，具 C++/C# 编程经验优先；
* 具游戏引擎（如 Unity、Unreal）使用经验者优先；
* 了解某方面的游戏客户端技术（如图形、音频、动画、物理、人工智能、网络同步）者优先考虑；
* 对于创新及解决具有挑战性的问题充满激情，有较强的学习能力、分析及解决问题能力，具备良好的团队合作意识；
* 具阅读英文技术文档能力；
* 热爱游戏。

### 测试开发

【测试开发】

* 计算机或相关专业本科及以上学历；
* 一至两年的 C/C++/Python 或其他计算机语言的编程经验；
* 具备撰写测试计划、测试用例、以及实现性能和安全等测试的能力；
* 具备实现自动化系统的能力；
* 具备定位调查产品缺陷能力、以及代码级别调试缺陷的能力；
* 工作主动积极，有责任心，具有良好的团队合作精神。

### 网络安全/逆向

【安全技术】

* 热爱互联网，对操作系统和网络安全有狂热的追求，专业不限；
* 熟悉漏洞挖掘、网络安全攻防技术，了解常见黑客攻击手法；  
* 掌握基本开发能力，熟练使用 C/C++ 语言；
* 对数据库、操作系统、网络原理有较好掌握；  
* 具有软件逆向，网络安全攻防或安全系统开发经验者优先。

### 嵌入式/物联网

【嵌入式应用开发】

* 有良好的编程基础，熟练掌握 C/C++ 语言；
* 掌握操作系统、数据结构等软件开发必备知识；
* 具备较强的沟通理解能力及良好的团队合作意识；
* 有 Linux/Android 系统平台的开发经验者优先。

### 音视频/流媒体/SDK

【音视频编解码】

1. 硕士及以上学历，计算机、信号处理、数学、信息类及相关专业和方向； 
2. 视频编解码基础扎实，熟常用的 HEVC 或 H264，有较好的数字信号处理基础； 
3. 掌握 C/C++，代码能力强, 熟悉一种汇编语言尤佳； 
4. 较强的英文文献阅读能力； 
5. 学习能力强，具有团队协作精神，有较强的抗压能力。

### 计算机视觉/机器学习

【计算机视觉研究】

* 计算机、应用数学、模式识别、人工智能、自控、统计学、运筹学、生物信息、物理学/量子计算、神经科学、社会学/心理学等专业，图像处理、模式识别、机器学习相关研究方向，本科及以上，博士优先；
* 熟练掌握计算机视觉和图像处理相关的基本算法及应用；
* 较强的算法实现能力，熟练掌握 C/C++ 编程，熟悉 Shell/Python/Matlab 至少一种编程语言；
* 在计算机视觉、模式识别等学术会议或者期刊上发表论文、相关国际比赛获奖、及有相关专利者优先。

<a id="review-of-brush-questions-website"></a>

## 💯 复习刷题网站

* [cplusplus](http://www.cplusplus.com/)
* [cppreference](https://zh.cppreference.com/w/%E9%A6%96%E9%A1%B5)
* [runoob](http://www.runoob.com/cplusplus/cpp-tutorial.html)
* [leetcode](https://leetcode.com/) | [leetcode-cn](https://leetcode-cn.com/)
* [lintcode](https://www.lintcode.com/)
* [nowcoder](https://www.nowcoder.net/)

<a id="interview-questions-experience"></a>

## 📝 面试题目经验

* [牛客网 . 2020秋招面经大汇总！（岗位划分）](https://www.nowcoder.com/discuss/205497)
* [牛客网 . 【备战秋招】2020届秋招备战攻略](https://www.nowcoder.com/discuss/197116)
* [牛客网 . 2019校招面经大汇总！【每日更新中】](https://www.nowcoder.com/discuss/90907)
* [牛客网 . 2019校招技术类岗位面经汇总【技术类】](https://www.nowcoder.com/discuss/146655)
* [牛客网 . 2018校招笔试真题汇总](https://www.nowcoder.com/discuss/68802)
* [牛客网 . 2017秋季校园招聘笔经面经专题汇总](https://www.nowcoder.com/discuss/12805)
* [牛客网 . 史上最全2017春招面经大合集！！](https://www.nowcoder.com/discuss/25268)
* [牛客网 . 面试题干货在此](https://www.nowcoder.com/discuss/57978)
* [知乎 . 互联网求职路上，你见过哪些写得很好、很用心的面经？最好能分享自己的面经、心路历程。](https://www.zhihu.com/question/29693016)
* [知乎 . 互联网公司最常见的面试算法题有哪些？](https://www.zhihu.com/question/24964987)
* [CSDN . 全面整理的C++面试题](http://blog.csdn.net/ljzcome/article/details/574158)
* [CSDN . 百度研发类面试题（C++方向）](http://blog.csdn.net/Xiongchao99/article/details/74524807?locationNum=6&fps=1)
* [CSDN . c++常见面试题30道](http://blog.csdn.net/fakine/article/details/51321544)
* [CSDN . 腾讯2016实习生面试经验（已经拿到offer)](http://blog.csdn.net/onever_say_love/article/details/51223886)
* [cnblogs . C++面试集锦( 面试被问到的问题 )](https://www.cnblogs.com/Y1Focus/p/6707121.html)
* [cnblogs . C/C++ 笔试、面试题目大汇总](https://www.cnblogs.com/fangyukuan/archive/2010/09/18/1829871.html)
* [cnblogs . 常见C++面试题及基本知识点总结（一）](https://www.cnblogs.com/LUO77/p/5771237.html)
* [segmentfault . C++常见面试问题总结](https://segmentfault.com/a/1190000003745529)

<a id="recruitment-time-post"></a>

## 📆 招聘时间岗位

* [牛客网 . 名企校招日程](https://www.nowcoder.com/school/schedule)

<a id="recommend"></a>

## 👍 内推

* [Github . CyC2018/Job-Recommend](https://github.com/CyC2018/Job-Recommend)：🔎 互联网内推信息（社招、校招、实习）
* [Github . amusi/AI-Job-Recommend](https://github.com/amusi/AI-Job-Recommend)：国内公司人工智能方向（含机器学习、深度学习、计算机视觉和自然语言处理）岗位的招聘信息（含全职、实习和校招）

<a id="contributor"></a>

## 👬 贡献者

<a href="https://github.com/huihut/interview/graphs/contributors"><img src="https://opencollective.com/interview/contributors.svg?button=false" /></a>

<a id="support-sponsor"></a>

## 🍭 支持赞助

**[Avalive](https://store.steampowered.com/app/1137770/Avalive/)**：一个面部捕捉的虚拟形象扮演软件。

<a id="license"></a>

## 📜 License

本仓库遵循 CC BY-NC-SA 4.0（署名 - 非商业性使用 - 相同方式共享） 协议，转载请注明出处，不得用于商业目的。

[![CC BY-NC-SA 4.0](https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png)](https://github.com/huihut/interview/blob/master/LICENSE)

