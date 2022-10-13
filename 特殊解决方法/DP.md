# 一、数位DP
数位DP一般应用于：
  求出在给定区间[A,B]内，符合条件P（i）的数i的个数。
  条件P（i）一般与数的大小无关，而是与数的组成有关。
  
  
## 例题
788. 旋转数字
```
  class Solution:
    def rotatedDigits(self, n: int) -> int:
        check = [0, 0, 1, -1, -1, 1, 1, -1, 0, 1]
        digits = [int(digit) for digit in str(n)]

        @cache
        def dfs(pos: int, bound: bool, diff: bool) -> int:
        # 从第 00 位到第 \textit{pos}-1pos−1 位的数是否「贴着」nn，记为bound。
        例如当 n=12345n=12345，\textit{pos}=3pos=3 时，如果前面的数位是 123123，那就表示贴着 nn，
        如果是 122, 121, \cdots122,121,⋯，那就表示没有贴着 nn。区分是否「贴着」nn 的作用是，如果 bound 为真，第 pos 位只能在 00 到 (n 的第pos位)进行选择，否则构造出的数就超过 n 了；
        如果 bound 为假，那么第pos 位可以在 00 到 99 之间任意选择

            if pos == len(digits):
                return int(diff)
            
            ret = 0
            for i in range(0, (digits[pos] if bound else 9) + 1):
                if check[i] != -1:
                    ret += dfs(
                        pos + 1,
                        bound and i == digits[pos],
                        diff or check[i] == 1
                    )
            
            return ret
            
        
        ans = dfs(0, True, False)
        dfs.cache_clear()
        return ans
```


322. 零钱兑换

当amount=11, coins = [1,2,3]时， dp[4] = min(dp[1], dp[2], dp[3])+1, 所以我们对于每个coin的面值，再循环更新dp的值.

```
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [float("inf")]*(amount+1)
        dp[0]=0
        for coin in coins:
            for i in range(coin, amount+1):
                dp[i] = min(dp[i], dp[i-coin]+1)
        return dp[amount] if dp[amount]!= float("inf") else -1
            

```
