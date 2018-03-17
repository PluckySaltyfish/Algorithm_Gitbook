### 最短路径

---

#### dijkstra（单源）

```cpp
void dijkstra(int s){
    priority_queue<P,vector<P>,greater<P>>que;
    fill(d,d+V,INF);
    d[s]=0;
    que.push(P(0,s));

    while(!que.empty()){
        P q = que.top();
        que.pop();
        int v = q.second;
        if(d[v]<q.first)continue;
        for (int i = 0; i <G[v].size() ; ++i) {
            edge e = G[v][i];
            if(d[e.to]>d[v]+e.cost){
                d[e.to]=d[v]+e.cost;
                que.push(P(d[e.to],e.to));

            }
        }
    }
}
```

#### Floyd-Warshall

任意两点的最小距离

```cpp
for (int i = 0; i < V; ++i)
{
    for (int j = 0; j < V; ++j)
    {
        if (i==j)
        {
            d[i][j]=0;
        }
        else d[i][j] = INF;
    }
}

for (int k = 0; k < V; ++k)
{
    for (int i = 0; i < V; ++i)
    {
        for (int j = 0; j < V; ++j)
        {

            d[i][j]=min(d[i][j],d[i][k]+d[k][j]); 
        }
    }
}
```

#### SPFA

```cpp
bool spfa(int src){
    int cnt =0;
    queue<int>q;
    fill(d1,d1+V+1,INF);
    d1[src] = 0;
    q.push(src);
    visited[src]=1;
    while (!q.empty()){
        int v = q.front();
        q.pop();

        for (int i = 0; i <G[v].size(); ++i) {
            edge e =G[v][i];
            if(d1[e.to]>d1[v]+e.cost){
                d1[e.to]=d1[v]+e.cost;
                if(!visited[e.to]){
                    visited[e.to]=1;
                    q.push(e.to);
                    if(++cnt>V)
                        return 1;
                }
            }
        }
    }
    return 0;
}
```



