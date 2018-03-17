### 最大公约数

```cpp
int gcd(a,b){
    return b==0?a:gcd(b,a%b);
}
```



