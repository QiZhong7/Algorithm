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

