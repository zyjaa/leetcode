[89. 格雷编码](https://leetcode.cn/problems/gray-code/)

**n 位格雷码序列** 是一个由 `2n` 个整数组成的序列，其中：

- 每个整数都在范围 `[0, 2n - 1]` 内（含 `0` 和 `2n - 1`）
- 第一个整数是 `0`
- 一个整数在序列中出现 **不超过一次**
- 每对 **相邻** 整数的二进制表示 **恰好一位不同** ，且
- **第一个** 和 **最后一个** 整数的二进制表示 **恰好一位不同**

给你一个整数 `n` ，返回任一有效的 **n 位格雷码序列** 。

 

**示例 1：**

```
输入：n = 2
输出：[0,1,3,2]
解释：
[0,1,3,2] 的二进制表示是 [00,01,11,10] 。
- 00 和 01 有一位不同
- 01 和 11 有一位不同
- 11 和 10 有一位不同
- 10 和 00 有一位不同
[0,2,3,1] 也是一个有效的格雷码序列，其二进制表示是 [00,10,11,01] 。
- 00 和 10 有一位不同
- 10 和 11 有一位不同
- 11 和 01 有一位不同
- 01 和 00 有一位不同
```

**示例 2：**

```
输入：n = 1
输出：[0,1]
```

 

### 1、模拟

镜像反转

```cpp
class Solution {
public:
    vector<int> grayCode(int n) {
        // 初始化结果数组，初始值为 0
        vector<int> res(1, 0);

        // 循环 n 次，每次生成更高一位的格雷码
        while (n--) {
            // 从后向前遍历当前结果数组
            for (int i = res.size() - 1; i >= 0; i--) {
                // 将当前值左移一位（相当于乘以 2）
                res[i] *= 2;
                // 在当前值的基础上加 1，并将其添加到结果数组中
                res.push_back(res[i] + 1);
            }
        }

        // 返回生成的格雷码序列
        return res;
    }
};
```

- 时间：O($$2^n$$)，外层循环执行 `n` 次，内层循环每次遍历的数组长度翻倍
- 空间：O($$2^n$$)，数组长度