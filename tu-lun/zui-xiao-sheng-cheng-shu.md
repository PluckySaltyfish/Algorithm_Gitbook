### 最小生成树

---

Kruskal\(利用并查集\)

```cpp
struct edge{
    int s,t,cost;
}
bool comp(const &edge e1,const &edge e2){
    return e1.cost <e2.cost;
}
edge e[MAX_E];
int kruskal(){
    init(V);
    int res = 0; 
    sort(e,e+E,comp);
    for(int i = 0;i < E;i++){
        if(find(e[i].t)!=find(e[i].s)){
            unite(e[i].s,e[i].t);
            res += e.cost;
        }
    }
    return res;
}
```



