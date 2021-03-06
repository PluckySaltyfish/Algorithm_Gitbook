### 最长上升子序列

#### 问题描述

给定一个长为n的整数序列$${a_0,a_1,a_2,...,a_n}$$，求这个序列中最长的上升子序列的**长度**。上升子序列指的是对于任意的$$i<j$$

都满足$$a_i<a_j$$的子序列。

例如序列{$${2,1,5,3,6,4,6,3}$$}的**LIS**为{$$1,3,4,6$$}或{$$2,3,4,6$$}，长度为4。

#### 问题分析

动态规划的思想，遍历该序列，对于序列中的元素$$a_i$$，若该元素结尾的LIS的长度为$$d_i$$，则可以得到:


$$
d_i= max(d_j) + 1 (0 <=j < i并且a_j < a_i)
$$


其含义就是，找寻位于该元素$$a_i$$前的比该元素小的元素$$a_j$$，那么以该元素结尾的LIS长度$$d_i$$便是以$$a_j$$结尾的LIS长度$$d_j+1$$，当然，因为是最长，所以要取所有$$d_j$$中的max。这便是该问题的一个基本的转移方程。

#### 解决方案

根据上述转移方程可以写出以下程序。

```cpp
int LIS(int a[],int n){
        if(n == 0)return 0;
        int d[MAXN];
        d[0] = 1;
        int res = 0;
        for(int i = 1;i < n;i++){
            int max_len = 0;
            for (int j = i - 1; j >= 0; j--) {
                if (a[j] < a[i] && d[j] > max_len)
                    max_len = d[j];
            }
            d[i] = max_len == 0 ? 1 : max_len + 1;
            res = d[i] > res ? d[i] : res;
        }
        return res;
    }
```

可以看出该程序的时间复杂度为$$O(n^2)$$，并且在向前遍历时存在了重复的操作，因此可以进行进一步改进。

#### 优化方案

记录$$d = i$$时最小的结尾元素值$$a_k$$，即：对于所有使得$$d_s = i$$的对于所有的$$s$$,$$a_k <= a_s$$。

例如如下序列：

![](/assets/lis.png)

可以发现元素2和1的$$d$$值都为1，对于后面的元素来说，仅需要比1大就可以进行$$d$$值的更新，所以仅仅记录当$$d=1$$时的结尾元素最小值（1）就行了。

下面是改进的方法，时间复杂度为$$O（nlogn）$$。

```cpp
int LIS(int a[],int n){
        if(n == 0)return 0;
        int ans[MAXN];
        ans[1] = a[0];
        int cnt = 1;
        for (int i = 1; i < n; i++) {
            if(a[i] > ans[cnt]){
                ans[++cnt] = a[i];
            }
            else{
                int pos = lower_bound(ans + 1, ans + cnt + 1, a[i]) - ans;
                ans[pos] = a[i];//这里用了一个比较巧妙的办法找到了a中比a[i]小的元素，并将其插入了ans中
            }
        }
        return cnt;
    }
```

数组$$ans[n]$$用来存储不同$$d$$对应的元素值，$$ans[i] = a$$代表$$d=i$$时最小的元素值为$$a$$。

#### 题目

[https://leetcode-cn.com/problems/longest-increasing-subsequence/](https://leetcode-cn.com/problems/longest-increasing-subsequence/submissions/)

