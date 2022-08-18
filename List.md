# 一、分治
## 例题
169.多数元素

# 二、位运算
## 例题

136.只出现一次的数字
异或运算中，0 XOR 0 = 0, 0 XOR 1 = 1, 1 XOR 0 = 1, 1 XOR 1 = 1。异或运算也满足交换律和结合律。
```
  return reduce(lambada x,y:x^y, nums)
  #reduce(function, iterable[]可迭代对象), reduce函数会对参数序列中元素进行function操作。
```


# 三、Boyer-Moore投票算法
## 例题

169.多数元素
维护一个候选众数***candidate***,和他出现的次数***count***。***candidate***可以为任意值，***count***为0。
遍历数组中的所有元素，对于每个元素***x***，如果***count***的值为0，就将***x***赋予给***candidate***，随后判断***x***：
  1.如果x与candidate相等，那么count增加1
  2.如果x与candidate不等，那么count减少1
遍历完，***candidate***的值即为整个数组的众数


# 四、模拟
## 例题

292.Nim游戏
如果堆中有4块石头，一定会失败，因为你拿1，2，3块，对手都有办法拿到剩下的几块。堆中有5，6，7块的时候，你可以分别拿1，2，3块，从而对手无论拿多少块，都会有剩下的。
当对手有8块的时候，跟4块的情况相似。类推我们可以得出，必须避免石头堆中的石子数为4的倍数的情况。

# 五、动态规划
## 例题

1143.最长公共子序列
暴力解法就是对于每个text1的字母，循环text2找出和i相等的j，再计算对于每个i最大的子序列

1035.不相交的线
本质和最长公共子序列一样
```
m,n = len(nums1), len(nums2)
dp = [[0]*(m+1) for _ in range(n+1)]
for i in range(m):
  for j in range(n):
    if nums1[i] == nums2[j]:
      dp[i+1][j+1] = dp[i][j]+1
    else:
      dp[i+1][j+1] = max(dp[i][j+1], dp[i+1][j])
return dp[m][n]
```


