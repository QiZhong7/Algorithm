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

# 六、特殊处理方法
## 例题

### 1. 标记法，交换法
41.缺失的第一个正数

对于一个长度为n的数组，缺失的第一个正整数只能出现在[1,n+1]中，这是因为如果1-n都出现了，那么答案就是n+1；如果n+1出现了，那么答案就是1-n中最小的正整数。
所以我们可以用哈希表来表示1-n的数是否出现过，但是此题的目标空间复杂度为O（1），我们需要把题目给的数组当作一个特殊的哈希表来进行标记：
对于数组中的正整数，应该如何证明他在1-n中并且我们已经遍历过呢？标记法采取的方法是，我们遍历数组的下标i时，如果nums[i]是一个正整数，那么我们可以通过把nums[nums[i]-1]
的元素变为负数来证明这个数出现在了数组中，同时大于n的数不需要操作，因为超出了数组的下标大小。

因为我们做标记的方法是取负，所以要提前对数组中的负数进行额外操作。这里是把他们变成值为n+1的正整数，不会干扰到以上的操作。

```
#标记法
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        n = len(nums)

        for i in range(n):
            if nums[i] <= 0 :
                nums[i] = n+1
            
        for i in range(n):
            # 我们遍历数组中的每一个数x时，有可能这个数已经被变为负数，所以要取绝对值。
            temp = abs(nums[i])
            if temp<=n:
                nums[temp-1] = -abs(nums[temp-1])

        for i in range(n):
            #第一个正整数的位置再加1就是答案。
            if nums[i] > 0 :
                return i+1
        
        return n+1
        
        
#交换法
#把1-n之间的数字通过交换到正确的位置，第一个不正确位置的数字就是答案
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        n = len(nums)
        for i in range(n):
            while 1 <= nums[i] <= n and nums[nums[i] - 1] != nums[i]:
                nums[nums[i] - 1], nums[i] = nums[i], nums[nums[i] - 1]
        for i in range(n):
            if nums[i] != i + 1:
                return i + 1
        return n + 1

```


