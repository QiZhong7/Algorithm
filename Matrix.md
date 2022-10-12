## 例题

剑指offer 29.顺时针打印矩阵

```
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        if not matrix:
            return []
        directions = [[0,1],[1,0],[0,-1],[-1,0]]
        m, n  = len(matrix),len(matrix[0])
        count = m*n
        move = 0
        index = 0
        res = []
        visited = [[False]*n for _ in range(m)]
        i, j = 0, 0
        for _ in range(count):
            visited[i][j] = True
            res.append(matrix[i][j])
            tempi = i + directions[index][0]
            tempj = j + directions[index][1]
            if not( 0<=tempi<m and 0<=tempj<n and not visited[tempi][tempj]):
                index = (index+1)%4
            i = i + directions[index][0]
            j = j + directions[index][1]
        return res
```

面试题13. 机器人运动轨迹

```
#倒推
class Solution1:
    def movingCount(self, m: int, n: int, k: int) -> int:
        
        def calculatedigit(num):
            twosum = 0
            while num>0:
                twosum += num%10
                num = num//10
            return twosum
        
        visited = set([(0,0)])
        for i in range(m):
            for j in range(n):
                if ((i-1,j) in visited or (i,j-1) in visited) and calculatedigit(i)+calculatedigit(j) <= k:
                    visited.add((i,j))
        return len(visited)
     
     
# 递推
class Solution2:
    def movingCount(self, m: int, n: int, k: int) -> int:
        from queue import Queue
        q = Queue()
        q.put((0, 0))
        s = set()
        while not q.empty():
            x, y = q.get()
            if (x, y) not in s and 0 <= x < m and 0 <= y < n and digitsum(x) + digitsum(y) <= k:
                s.add((x, y))
                for nx, ny in [(x + 1, y), (x, y + 1)]:
                    q.put((nx, ny))
        return len(s)


```
