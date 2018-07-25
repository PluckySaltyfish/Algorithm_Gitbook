### 图的表示

> #### 注意无向图需要连两边

#### 邻接矩阵

查找快，浪费空间，边多的时候用

```cpp
int V,E;
int edge[MAX_V][MAX_V];
scanf("%d %d",&V,&E);
for (int i = 0; i <E ; ++i) {
    int s,t,cost;
    scanf("%d %d %d",&s,&t,&cost);
    edge[s][t]=cost;
}
```

#### 邻接表

省空间，查找慢，边不多的时候用

```cpp
struct edge{
    int to,cost;
};
int main()
{
    int V,E;
    vector<edge>G[MAX_V];
    scanf("%d %d",&V,&E);
    for (int i = 0; i <E ; ++i) {
        int s,t,cost;
        scanf("%d %d %d",&s,&t,&cost);
        edge e;
        e.to =t;
        e.cost=cost;
        G[s].push_back(e);
    }
    return 0;
}
```



