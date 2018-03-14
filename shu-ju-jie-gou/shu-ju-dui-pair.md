### 数据对pair

> \#include&lt;utility&gt; 有时不用

pair用来定义一对数据。

#### 构造

```cpp
pair<int,int>p;
p=pair<int,int>(3,4);
p=make_pair(3,4);
```

#### 访问

```cpp
typedef pair<int,int>p;
p p1 =p(1,3);
int x = p.first; //x=1
int y = p.second; //y=3
```

pair常常用来为map做插入用。

