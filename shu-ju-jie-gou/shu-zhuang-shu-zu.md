```cpp
class BinaryTree{
private:
    int arr[maxn];
    int n;
public:
    BinaryTree(int a[],int n){
        this->n = n;
        for(int i = 1;i <= n;i++){
            this->arr[i] = a[i];
        }

        for (int i = 1; i < n; i++) {
            int j = i + (i&-i);
            if (j < n+1) {
                this->arr[j] += this->arr[i];
            }
        }
    }

    void add(int idx,int num){
        this-> arr[idx] += num;
        for (int i = idx + (idx&-idx); i <= this->n; i += (i&-i)) {
            this->arr[i] += num;
        }
    }

    int sum(int idx){
        int sum0 = this->arr[idx];
        for (int i = idx-(idx&-idx); i >= 1; i = i-(i&-i)) {
            sum0 += this->arr[i];
        }
        return sum0;
    }

    int range(int from,int to){
        return sum(to)-sum(from-1);
    }
};
```



