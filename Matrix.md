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
