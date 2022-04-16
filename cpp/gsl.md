# 《C++ Core Guildlines》笔记

本文是对[C++ Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#main)的阅读笔记。因为个人阅读的顺序并不是文章的顺序阅读的，因此记录的比较也是乱序。

## 尽量在编译器做检查

### Case1

**Bad**

```cpp
// Int是代码里面针对整数的别名，检查Int是否是4或者8字节
int bits = 0;        
for (Int i = 1; i; i <<= 1)
    ++bits;
if (bits < 32)
    cerr << "Int too small\n";
```

**Good**

```cpp
static_assert(sizeof(Int) >= 4); 
```

### Case2

**Bad**

```cpp
void read(int* p, int sz);    // sz用于指明p的大小 


int a[100];
read(a, 1000);    // 第二个参数1000大于100，芭比Q了
```

**Good**

```cpp
void read(std::span<int> p);

int a[100];
read(a);
```

```std::span```是C++20新增的特性，是对连续内存序列的轻型视图，目前就是为了安全的访问连续序列。

## 关于资源管理

### R.1：使用资源句柄（resource handle）和RAII管理资源

### R.2：在函数定义中，指针最好只是用于指向一个单独的实例


