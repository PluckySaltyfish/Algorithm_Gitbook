### algorithm

#### 排序

**sort\(**RandomIt first, RandomIt last, Compare comp**\)**

```cpp
int a[20];
vector<int>v;
...
sort(a,a+20);
sort(v.begin(),v.end(),greater<int>());     //将v中的元素从大到小排列
sort(v.begin()+3,v.end(),less<int>());      //从v中第3个元素到最后一个元素按照从小到大的顺序排序
```

#### 查找

在使用前应确保有序，默认情况下函数都默认为从大到小的顺序进行二分搜索。查找即插入，并且以下插入指的都是前插。

**lower\_bound\(**RandomIt first, RandomIt last,Obj ,Compare comp**\)**

返回一个迭代器，指向可插入的第一个位置。

**upper\_bound\(**RandomIt first, RandomIt last, Obj,Compare comp**\)**

返回一个迭代器，指向可插入的最后一个位置。

另外，如果自定义比较函数，注意是重写严格规则，即，重写`<`和`>`规则。

```cpp
vector<int>::iterator it = upper_bound(v.begin(), v.end(),4,greater<int>());
vector<int>::iterator it2 = lower_bound(v.begin(), v.end(),4,greater<int>());
int pos = upper_bound(v.begin(), v.end(),4,greater<int>()) -v.begin();   //获得位置
```



