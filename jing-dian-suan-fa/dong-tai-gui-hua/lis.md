### 最长上升子序列

```cpp
// n^2 和 nlgn 的最长上升子序列

#include <iostream>
#include <algorithm>
using namespace std;
const int maxn = 9;
int main(){
    int a[maxn]={0,2,1,5,3,6,4,6,3};
    int ans[maxn];//dp为i的最小结尾数字为ans[i]
    ans[1] = a[1];
    int cur = 1;
    for (int i = 2; i < maxn; i++) {
        if(a[i]>ans[cur]){
            ans[++cur] = a[i];
        }
        else{
            int pos = lower_bound(ans+1, ans+1+cur, a[i])-ans;
            ans[pos] = a[i];
        }
    }
    cout <<cur<< endl;
    return 0;
}
```



