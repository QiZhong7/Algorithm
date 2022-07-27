# 一、双指针
## 例题：
  160.相交链表
  ```
    #注意这里if moveA不能写成moveA.next，当两个链表没有相交点的时候，moveA和moveB会同时变成None而跳出循环
    moveA = moveA.next if moveA else headB
  ```
    
 

- 
  
```

      
```

# 二、回溯算法

# 三、迭代/递归

## 例题：
  206.反转链表
  ```
  
  #迭代
  prev = None
  curr = head
  while curr:
    nxt = curr.next
    curr.next = prev
    prev = curr
    curr = nxt
  return prev
  
  ```
  
  ```
  
  #递归
  if head == None or head.next==None:
    return head
  last = reverseList(head.next)
  head.next.next = head
  head.next = None
  return last
  
  ```
  

