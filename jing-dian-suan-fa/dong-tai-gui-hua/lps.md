### 最长回文子序列

```cpp
class Solution {
public:
    int longestPalindromeSubseq(string s) {
        int dp[1005][1005];
        int n = s.length();
        for (int i = 0; i < n; i++) {
            dp[i][i] = 1;
        }
        for (int len = 2; len <= n; len++) {
            for (int i = 0; i + len <= n; i++) {
                int j = i + len - 1;
                if (s[i] == s[j])
                    dp[i][j] = dp[i+1][j-1] + 2;
                else
                    dp[i][j] = max(dp[i+1][j],dp[i][j-1]);
            }
        }
        return dp[0][n-1];

    }
};
```

```cpp
//逆序 再LCS 要比第一种慢
class Solution {
public:
    int longestPalindromeSubseq(string s) {
        int dp[1005][1005];
        dp[0][0] = 0;
        string s1 = s;
        reverse(s.begin(), s.end());
        int n = s.length();
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if(s[i] == s1[j])
                    dp[i+1][j+1] = dp[i][j] + 1;
                else
                    dp[i+1][j+1] = max(dp[i+1][j],dp[i][j+1]);
            }
        }
        return dp[n][n];

    }
};
```

马拉车

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int p[2005] = {0};//记录最长半径
        int id = 0,mx = 0,center = 0,len = 0;
        
        //初始化字符串
        string s1 = "$#";
        for (int i = 0; i < s.length(); i++) {
            s1 += s[i];
            s1 += '#';
        }
        
        for (int i = 1; i < s1.length() - 1; i++) {
            p[i] = mx > i ? min(mx - i,p[2 * id - i]):1;
            while (s1[i+p[i]] == s1[i-p[i]])p[i]++;
            if (p[i] + i > mx) {
                mx = p[i] + i;
                id = i;
            }
            if(p[i] > len){
                len = p[i];
                center = i;
            }
        }
        return s.substr((center - len)/2,len - 1);
    }
};
```



