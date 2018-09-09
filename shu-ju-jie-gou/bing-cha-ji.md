### 并查集

#### 说明

并查集是一种用来管理元素分组情况的数据结构。它可以实现对元素集中分组元素的查询和合并。其功能有两个：

1.查询元素属于哪个分组

2.将两个分组的元素合并为同一个分组

并查集利用树形结构实现。所以实现其功能实际上是：

1.查询该元素所属结点属于哪个根

2.将一个组的根向另一个组的根连边

要注意：为了避免退化造成复杂度大的情况，连边时将深度小的连至深度大的根上。

#### 实现

```cpp
int V,E;
int par[MAX_V];//分组信息
int rk[MAX_V];//每一组树的深度
//初始化，每一个元素单独为一组
void init(int n){
    for (int i = 1; i <=n ; ++i) {
        par[i]=i;
        rk[i]=0;
    }
}

int find(int x){
    if(par[x] == x){
        return x;
    }else{
        return par[x] = find(par[x]);
    }
}

void unite(int x,int y){
    x = find(x);
    y = find(y);
    if(x==y)return;
    if(rk[x]<rk[y]){
        //如果x的深度比有小，x连到y下
        par[x] = y;
    }else{
        par[y] = x;
        //如果x的深度比有大，y连到x下
        if(rk[x]==rk[y])rk[x]++;
        //同深度相连，深度会增加
    }
}
```

#### 例题

![](/assets/1.png)



