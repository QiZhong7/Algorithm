# 一、KMP算法
  KMP算法有个前缀函数，用来计算
```
def buildnxt(p):
  nxt = []
  nxt.append(0) #nxt[0] 默认为0，因为无法与自身相同
  x=1 #x表示右指针，指向当前扫描的位置
  now=0 #now表示nxt[x-1],同时也是当前扫描位置的对称点
  
  while x<len(p):
    if p[now] == p[x]:
      now+=1
      x+=1
      nxt.append(now)
    elif now:    #当p[now] != p[x]时，就要去缩减now值看看更小范围内有没有相同的前后缀
      now = nxt[now-1]
    else:
      nxt.append(0)
      x+=1
      
```
     
# 二、回溯算法


# 三、滑动窗口
## 例题：
- 30.串联所有单词的字串
- 438.找到字符串中所有字母异位词


# 四、动态规划
动态规划可以用来解决字符串匹配中的正则表达式匹配问题
## 例题：

10.正则表达式匹配

```
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        #match函数用来处理s中下标为i-1的元素和p中下标为j-1的元素是否相等。
        def match(i,j):
            #i==0说明s是个空字符
            if i==0:
                return False
            #如果p中下标为j-1的元素为".",等于任何一个元素都能匹配上
            if p[j-1] == ".":
                return True
            return s[i-1] == p[j-1]
        
        m, n = len(s), len(p)
        dp = [[False]*(n+1) for _ in range(m+1)]
        #当s和p都为空字符，也是可以匹配成功的。
        dp[0][0] = True
        for i in range(m+1):
            #j=0时，p为空字符，无法匹配s
            for j in range(1,n+1):
                if p[j-1] == "*":
                    #例如“a*”也可以是0个“a”，所以可以直接跳到dp[i][j-2]的位置，先检测“a*”是不是可以抛弃
                    dp[i][j] |= dp[i][j-2]
                    #假如“a*”有效，意味着可以匹配一个以上的“a”,所以dp[i][j] = dp[i-1][j] or dp[i][j-2]
                    if match(i, j-1):
                        #为什么等于dp[i-1][j]呢？本来是要一个个往前匹配s，如s[i-1]->s[i-2], 因为动态规划的原因，我们只需要匹配当前s末尾的一个字符，检测他是否与p匹配即可
                        dp[i][j] |= dp[i-1][j]
                else:
                    if match(i, j):
                        dp[i][j] |= dp[i-1][j-1]
        return dp[m][n] 

               
```


