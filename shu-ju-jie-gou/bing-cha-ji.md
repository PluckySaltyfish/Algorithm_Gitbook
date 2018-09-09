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
        return par[x] = find(par[x]);//查询一次后直接连到根结点上
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

**输入格式**

第1行输入两个整数，N和K。

第2行至第K行，每行输入3个整数：信息种类t，x，y。

**样例输入**

```
100 7
1 101 1
2 1 2
2 2 3
2 3 3
1 1 3
2 3 1
1 5 5
```

**样例输出**

```
3（1，4，5条是错的）
```

**分析**

用i表示第i个动物属于A，i+N表示第i个动物属于B，i+2N表示第i个动物属于C

**示例程序**

```cpp
#include <cstdio>

using namespace std;
const int MAXN = 50001*3;

int N,K;
int par[MAXN];
int rank[MAXN];

void init(){
    for (int i = 1; i <= 3*N; i++) {
        par[i] = i;
        rank[i] = 0;
    }
}

int find(int i){
    if (par[i]==i) {
        return i;
    }
    return par[i] = find(par[i]);
}

void unite(int x,int y){
    x = find(x);
    y = find(y);
    if (rank[x]<rank[y]) {
        par[x] = y;
    }
    else{
        par[y] = x;
        if (rank[x]==rank[y]) {
            rank[x]++;
        }
    }
}

int same(int x,int y){
    return find(x)==find(y);
}

int main(){
    scanf("%d %d",&N,&K);
    int cnt = 0;
    init();
    while (K--) {
        int t,x,y;
        scanf("%d %d %d",&t,&x,&y);
        if (x>N||x<1||y>N||y<1) {
            cnt++;
            continue;
        }
        if (t==1) {
            //矛盾的情况：x和y不属于同一类别
            if (same(x,y+N)||same(x, y+2*N)) {
                cnt++;
            }
            else{
                unite(x, y);
                unite(x+N, y+N);
                unite(x+2*N, y+2*N);
            }
        }
        else{
            //矛盾的情况：x和y属于同一类别或y吃x
            if (same(x, y)||same(x, y+2*N)) {
                cnt++;
            }
            else{
                unite(x, y+N);
                unite(x+N, y+2*N);
                unite(x+2*N, y);
            }
        }
        
        
    }
    printf("%d",cnt);
}


```



























