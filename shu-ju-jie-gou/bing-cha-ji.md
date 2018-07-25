### 并查集

#### 实现

```cpp
int V,E;
int par[MAX_V];
int rk[MAX_V];
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
        par[x] = y;
    }else{
        par[y] = x;
        if(rk[x]==rk[y])rk[x]++;
    }
}
```



