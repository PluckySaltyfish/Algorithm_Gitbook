### 字符串String

> \#include&lt;string&gt;

---

字符串类型是C++提供的一个新的数据类型，用户仍然可以选用字符数组作为字符串，但是string型却更加简便。

#### 静态方法

**.length\(\)  **返回字符串的长度

**.append\(\) **在末尾追加字符串

**.replace\(\)** 替换字符串

```cpp
s.replace(0,4,"")        //s字符串从第0位开始替换4个字符为""
```

**.find\_first\_\_\_of\(\) ** 从头查找字符串

**.find\_last\_of\(\)**  从末尾查找字符串

**.substr\(\)**   截取字符串

```cpp
string str = s.substr(0,4)            //从s字符串的第0位开始截取4个字符
```

#### 流式输入输出

```cpp
#include <iostream>
#include <sstream>
#include <string>
using namespace std;

int main(){
    string line;
    while(getline(cin,line)){
        int sum = 0, x;
        stringstream ss(line);
        while(ss >> x){
            sum += x;
        }
        cout << sum << endl;
    }
    return 0;
}
```

需要注意的是，字符串数组不能使用`cin`输入输出，而**string**可以，正常情况下`cin`输入的字符串以空格分割，若想输入一行字符串，使用头文件`iostream`里的 `getline()`

#### 转换

String到从CString的转换：

```cpp
string s;
cin >> s;
const char * = s.c_str();
```

#### 构造

```cpp
string(const char *s);    //用c字符串s初始化
string(int n,char c);     //用n个字符c初始化
```

#### 



