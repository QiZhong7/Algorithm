# 一、前序，中序，后序遍历
```
#中序遍历

#递归
def inorderTraversal(self, root):
  self.res = []
  if not root:
    return self.res
  self.inorderhelper(root)
  return self.res
  
def inorderhelper(self, root):
  current = root
  if not current:
    return
  self.inorderhelper(current.left)
  self.res.append(current)
  self.inorderhelper(current.right)
```
```
  
  
#迭代
stack = []
res = []
while root or len(stack):
  while root:
    stack.append(root)
    root = root.left
  root = stack.pop()
  res.append(root.val)
  root = root.right
return res
```


## 例题
230.二叉搜索树中第k小的元素
```
#用中序遍历逐个排查节点，时间复杂度为O（h+k）,h为树的高度，要先到达叶结点，花费h时间，然后再根据k的数量逐一筛选。空间复杂度为O（h）
stack = []
while root or stack:
  while root:
    stack.append(root)
    root = root.left
  root = stack.pop()
  k-=1
  if k == 0:
    return root.val
  root = root.right

```

```
#计算每个结点有多少子节点，再根据数量排查是第k个节点是哪个
node_num = {}

def count_num(node):
  if not node:
    return 
  node_num[node] = 1+count_num(node.left)+count_num(node.right)
  return node_num[node] 

def get_node_num(node):
  return node_num[node] if node else 0

current = root
count_num(current)
while current:  
  left = get_node_num(current.left)
  if left==k-1:
    return current.val
  elif left>k-1:
    current = current.left
  else:
    k -= left+1
    current = current.right
  

```


