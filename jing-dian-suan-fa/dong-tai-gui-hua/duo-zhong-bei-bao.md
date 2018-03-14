### 多重背包

---

#### 问题描述

有$$N$$种物品，第$$i$$种物品的重量为$$w_{i}$$，价值为$$v_{i}$$，个数为$$n_i$$，每种可以取若干件装入背包，有一背包的容积为$$C$$，现在将物品装进背包，求在装载不超过背包容量大小的物品的最大价值。

#### 问题分析

对每种物品的个数进行拆分，用二进制表达。

```cpp
int count = 0;
for(int i =1;i<=N;i++){
    cin >> w[i]>>v[i]>>n[i];
    for(int k=1;k<=n[i];k<<=1){
        weight[count] = k*w[i];
        value[count++] = k*v[i];      
        n[i]-=k;
    }
    if(n[i]>0){
        weight[count] = n[i]*w[i];
        value[count++]=n[i]*i;
    }
}
```

之后就可以把新生成的$$value$$和$$weight$$当作01背包求解。

时间复杂度为$$O(C \sum logn)$$

