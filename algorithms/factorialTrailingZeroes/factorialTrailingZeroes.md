### 1、模拟

只有2*5才得到0,5的数量肯定比2少，那就是有多少5就有多少0

```cpp
class Solution {
public:
    int trailingZeroes(int n) {
        // n!=n*..1   5*2
        int res = 0;
        while (n) {
            res += n / 5; // 计算当前 n 中包含的 5 的因子个数
            n /= 5; // 更新 n，继续计算更高阶的 5 的因子
        }
        return res;
    }
};
```



对于5的倍数：count = n / 5 + n / 25 + n / 125 + ...

- 每个 `5` 的倍数贡献一个因子 `5`。
- 每个 `25` 的倍数额外贡献一个因子 `5`。
- 每个 `125` 的倍数再额外贡献一个因子 `5`，以此类推。



### **时间复杂度**

- 每次循环 `n` 除以 5，因此循环次数为 **O(log₅n)**。
- 时间复杂度为 **O(log n)**。

------

### **空间复杂度**

- 只使用了常数级别的额外空间，空间复杂度为 **O(1)**。
