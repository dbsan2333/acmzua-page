---
title: 算法集训#1:C++STL基础
date: 2023-12-17 19:00:00
tags: 算法集训
---
## 头文件引入

```cpp
#include <bits/stdc++.h> // 万能头文件
using namespace std; // 使用标准命名空间
// 竞赛玩法，完全避免溢出的错误
// #define int long long
// signed main() {}
```

## cin, cout

基本类型变量输入输出

支持以下类型

`int, long long, float, double, char, char[], string`

```cpp
    int a;
    double b;
    string ss;
    char s[100];

	// 输入
    cin >> a;
    cin >> b;
    cin >> ss；
    cin >> s;

	// 输出
    cout << a << '\n';
    cout << b << '\n';
    cout << ss << '\n';
    cout << s << '\n';

	// 链式使用，效果等价于上面的输出，cin也可以这么用
    cout << a << '\n' << b << '\n' << ss << '\n' << s << '\n';
```

## container

容器，就是存储数据的一个东西

可以分为两类：

顺序容器，使用线性存储：1. 动态数组（vector）2. 字符串（string，实际就是特殊化的字符型动态数组）

关联容器，使用树形存储：1. 集合（set，存储不同的元素）2. 映射（或称为字典）（map，存储键值对）

容器支持的操作

1. 迭代器：头指针 `begin()` 尾指针 ` end()`
2. 容器大小（存储元素个数）：`size()`
3. 是否为空：`empty()`
4. 清空：`clear()`
5. 顺序容器支持的索引随机访问：`a[i]` 第 i 个元素
6. 添加：`push()`, `push_back()`, `insert()`
7. 删除：`pop()`, `pop_back()`, `erase()`

## string

[std::basic_string - cppreference.com](https://zh.cppreference.com/w/cpp/string/basic_string)

```cpp
    // 定义string并赋值，也可以不赋值
    string s = "abcdabc";
    string t = "bcd";
    // 容器大小
    cout << s.size() << '\n';
    // 拼接
    cout << s + t << '\n';
    // 随机访问
    cout << s[2] << '\n';
    // 字串, 从1开始，长度为2的字串
    cout << s.substr(1, 2) << '\n';
    // 字符串匹配 O(mn)
    auto pos = s.find("e");
    if (pos != -1) {
        cout << pos << '\n';
    } else {
        cout << -1 << '\n';
    }
    // 插入（insert），删除（erase）不常用，暂时先不讲
    // 字符串比较（<, > , =, !=, <=, >=），按照字典序比较
    // 字串与其他类型的转化
    cout << stoi("123") << '\n'; // 转int
    cout << stoll("1234567890") << '\n'; // 转long long
    cout << stod("1.23") << '\n'; // 转double
    cout << to_string(1) << '\n'; // 其他类型转字符串
```

```cpp
// 2023年天梯赛L1 T6，对insert和erase的考察
#include <bits/stdc++.h>
using namespace std;

int main() {
    string ss;
    cin >> ss;
    int n;
    cin >> n;
    while (n--) {
        int a, b;
        cin >> a >> b;
        int n = b - a + 1;
        string cx = ss.substr(a - 1, n);
        ss.erase(a - 1, n);
        string s, t;
        cin >> s >> t;
        string u = s + t;
        int p = ss.find(u);
        if (p == -1)
            ss += cx;
        else
            ss.insert(p + s.size(), cx);
    }
    cout << ss;
}
```

## vector

[std::vector - cppreference.com](https://zh.cppreference.com/w/cpp/container/vector)

```cpp
    // 定义vector<T>并赋值，也可以不赋值
    vector<int> a = {3, 1, 2, 4, 5};
    vector<int> b(5); // 大小初始设置为5，默认填充为0
    vector<int> c(5, 1); // 大小初始设置为5，默认填充为1
    // 容器大小
    cout << a.size() << '\n';
    // 在尾部添加或删除
    a.push_back(6);
    a.pop_back();
    // 随机访问与遍历
    for (int i = 0; i < a.size(); i++)
        cout << a[i] << ' ';
    cout << '\n';
    // 范围循环 c++11 及以上特有的
    for (int x : a)
        cout << x << ' ';
    cout << '\n';
    // 插入
    // a.insert(a.begin() + it, val); // 在位置it插入val
    // a.insert(a.begin() + it, bg, ed); // 在位置it插入范围[bg, ed)的数据
    // 删除
    // a.erase(it); // 删除位置it的元素
    // a.erase(bg, ed); // 删除范围[bg, ed)的数据
    // 比较（<, > , =, !=, <=, >=），按照字典序比较
```

## stack - queue

https://zh.cppreference.com/w/cpp/container/stack

```cpp
    // 2 3
    stack<int> s;
    // 放入2
    s.push(2);
    // 放入3
    s.push(3);
    // 大小
    cout << s.size() << '\n';
    // 在容器非空时执行循环
    while (!s.empty()) {
        // 访问栈顶元素
        cout << s.top() << '\n';
        // 弹出栈顶元素
        s.pop();
    }
```

https://zh.cppreference.com/w/cpp/container/queue

```cpp
    // 2 3
    queue<int> q;
    // 放入2
    q.push(2);
    // 放入2
    q.push(3);
    // 大小
    cout << q.size() << '\n';
    // 在容器非空时执行循环
    while (!q.empty()) {
        // 访问队列头部元素
        cout << q.front() << '\n';
        // 弹出队列头部元素
        q.pop();
    }
```

## set

https://zh.cppreference.com/w/cpp/container/set

```cpp
    // 定义集合s
    set<int> s;
    // 插入
    s.insert(1);
    s.insert(2);
    s.insert(1);
    s.insert(3);
    // 删除
    s.erase(2);
    // 大小
    cout << s.size() << '\n';
    // 计数：返回集合中3的个数
    if (s.count(3)) {
        cout << "s contain 3\n";
    } else {
        cout << "s don't contain 3\n";
    }
    // 遍历（集合元素默认升序）
    for (int x : s) {
        cout << x << ' ';
    }
    cout << '\n';
    // 迭代器遍历
    for (auto it = s.begin(); it != s.end(); it++) {
        cout << *it << '\n';
    }
    cout << '\n';
```

## map

https://zh.cppreference.com/w/cpp/container/map

数组把索引映射到数组的值，a[i] 把 i 映射到数组第 i 个

```
如果我有三个映射：
1 -> 10
10000 -> 100
100000000 -> 1000
那么我需要定义长度大于100000000的数组
int a[100000005];
a[1] = 10;
a[10000] = 100;
a[100000000] = 1000;
这样会爆空间
```

所以出现了map，树形结构，红黑树

```cpp
    map<int, int> mp;
    mp[1] = 10;
    mp[10000] = 100;
    mp[100000000] = 1000;
    if (mp.count(10000)) {
        cout << "mp contain 10000\n";
    } else {
        cout << "mp don't contain 10000\n";
    }
	// 遍历 
    for (auto it : mp) {
        cout << it.first << " -> " << it.second << '\n';
    }
    for (auto &[k, v] : mp) { // c++17 结构化绑定 devc++ 没法用的报错 dev只支持c++11
        cout << k << " -> " << v << '\n';
    }
```

下面是泛型算法，泛型，意味着不限制类型，都可以使用的算法

## reorder element

### swap

交换两个对象的值

```c
#include <stdio.h>

void swap(int *a, int *b) {
    int t = *a;
    *a = *b;
    *b = t;
}
int main() {
    int a = 1, b = 2;
    swap(&a, &b);
    // int t = a;
    // a = b;
    // b = t;
    printf("%d %d", a, b);
}
```

```cpp
    int a = 1, b = 2;
    swap(a, b);
    cout << a << ' ' << b;
```

```cpp
    string a, b;
    a = "12";
    b = "21";
    swap(a, b);
    cout << a << '\n' << b << '\n';
```

### reverse

 逆转范围中的元素顺序

```cpp
    int a[5] = {1, 2, 3, 4, 5};
    reverse(a, a + 5);
    vector<int> b = {1, 2, 3, 4, 5};
    reverse(b.begin(), b.end());
    // [ )
    // [0 1 2 3 4 5)
    for (int i = 0; i < 5; i++)
        cout << a[i] << ' ';
    cout << '\n';

    for (int i = 0; i < b.size(); i++)
        cout << b[i] << ' ';
    cout << '\n';
```

## permutation

### next_permutation

产生某个元素范围的按字典顺序的下一个较大的排列

```cpp
vector<int> a = {1, 2, 3, 4};
    do {
        for (int x : a)
            cout << x << ' ';
        cout << '\n';
    } while (next_permutation(a.begin(), a.end()));
    // 4 * 3 * 2 = 24
```

### prev_permutation

```cpp
    vector<int> a = {4, 3, 2, 1};
    do {
        for (int x : a)
            cout << x << ' ';
        cout << '\n';
    } while (prev_permutation(a.begin(), a.end()));
    // 4 * 3 * 2 = 24
    // 字典序
```

## sort

### sort

将范围按升序/降序排序

```cpp
    vector<int> a = {3, 1, 2, 4, 5};
    // sort(a.begin(), a.end(), less()); // <
    sort(a.begin(), a.end(), greater()); // >
    for (int x : a)
        cout << x << " ";
```

自定义排序比较器

```cpp
bool cmp(int a, int b) {
    return a > b;
} // <=> greater()

int main() {
    vector<int> a = {3, 1, 2, 4, 5};
    sort(a.begin(), a.end(), cmp);
    for (int x : a) {
        cout << x << ' ';
    }
}
```

结构体排序

```cpp
struct Node {
    int height, weight;
};

// struct Node {
//     int height, weight;
// } A[10];
// <=>
// Node A[10];

bool cmp(const Node& a, const Node& b) {
    // if (a.attribute1 != b.attribute1) {
    // } else if (a.attribute2 != b.attribute2) {
    // } else {
    // }
    return a.height != b.height ? a.height < b.height : a.weight > b.weight;
}

int main() {
    vector<Node> a;
    a.push_back({175, 70});
    a.push_back({170, 68});
    a.push_back({170, 75});
    a.push_back({165, 80});

    // 传统写法
    sort(a.begin(), a.end(), cmp);

    // lambda函数 c++11特性 匿名函数
    // sort(a.begin(), a.end(), [](const Node& a, const Node& b) {
    //     return a.height != b.height ? a.height < b.height : a.weight > b.weight;
    // });

    for (auto &[h, w] : a) {
        cout << h << ' ' << w << '\n';
    }
}
```

## change element

### fill

将一个给定值复制赋值给一个范围内的每个元素

```cpp
    int a[5];
    fill(a, a + 5, 5);
    for (int i = 0; i < 5; i++) {
        cout << a[i] << " ";
    }
```

### unique

移除范围内的连续重复元素

```cpp
    vector<int> a = {1, 2, 3, 3, 4, 4, 5};
    auto end = unique(a.begin(), a.end());
    for (int x : a) {
        cout << x << ' ';
    }
    cout << '\n';
    for (auto it = a.begin(); it != end; it++) {
        cout << *it << ' ';
    }
    cout << '\n';
    vector<int> b = {1, 2, 3, 3, 4, 4, 5};
    a.erase(unique(b.begin(), b.end()), b.end());
    for (int x : b) {
        cout << x << ' ';
    }
```

## binary search

### lower_bound

返回指向第一个*不小于*给定值的元素的迭代器

### upper_bound

返回指向第一个*大于*给定值的元素的迭代器

```CPP
    vector<int> a = {1, 2, 3, 5, 6};
    cout << *lower_bound(a.begin(), a.end(), 3) << '\n'; // >=
    cout << lower_bound(a.begin(), a.end(), 3) - a.begin() << '\n';; // >=

    cout << *upper_bound(a.begin(), a.end(), 3) << '\n'; // >
    cout << upper_bound(a.begin(), a.end(), 3) - a.begin() << '\n';; // >
```

## minmax

### min

返回各给定值中的较小者

### max

返回各给定值中的较大者

```cpp
    int a = 1, b = 2, c = 3;
    cout << max(a, b) << '\n';
    cout << min(a, b) << '\n';

    cout << max({a, b, c}) << '\n';
    cout << min({a, b, c}) << '\n';
```

### min_element

返回范围内的最小元素

### max_element

返回范围内的最大元素

```cpp
    vector<int> a = {1, 2, 3, 4, 5};
    cout << *max_element(a.begin(), a.end()) << '\n';
    cout << *min_element(a.begin(), a.end()) << '\n';
```

## numeric

### accumulate

对一个范围内的元素求和

```cpp
    vector<int> a = {1, 2, 3, 4, 5};
    cout << accumulate(a.begin(), a.begin() + 3, 0) << '\n';
```

### iota

用从起始值开始连续递增的值填充一个范围

```cpp
    vector<int> a(5);
    // for (int i = 0; i < a.size(); i++)
    //     a[i] = i + 1;
    iota(a.begin(), a.end(), 1);
    for (int x : a) {
        cout << x << ' ';
    }
```
