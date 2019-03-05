### 输入输出

通常情况下使用`scanf()`与`printf()`进行输入输出。

考试中测试数据可以重定向到文件。

```cpp
freopen("input.txt","r",stdin);
```

### 迭代器

#### 正向遍历

```cpp
vector<int>v;
...
for (vector<int>::iterator it = v.begin(); it < v.end(); it++) {
    cout << *it <<endl;
}
```

#### 反向遍历

```cpp
map<int,int>m1;
...
for(map<int,int>::reverse_iterator it =m1.rbegin();it!=m1.rend();it++){
    cout it->second <<endl;
}
```

### 位运算





