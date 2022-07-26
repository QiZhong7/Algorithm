# 一、双指针
## 例题：
  142.环形链表II
  ···
    条件：设a为环外部分的长度，b为入环点到相遇点的距离，c为环剩下的长度。fast指针走过的距离恒为slow指针的两倍。
    推导：a+(n+1)b+nc = 2(a+b) --> a = c+(n-1)(b+c) --> 从相遇点到入环点的距离，即为c，再加上n-1圈的环长，恰好等于从链表头部到入环点的距离。
    当fast和slow相遇时，创建一个新的指针ptr=head，再让ptr和slow每次走一步，ptr和slow相遇时便是入环点。
  ···
  
  160.相交链表
  ```
    #注意这里if moveA不能写成moveA.next，当两个链表没有相交点的时候，moveA和moveB会同时变成None而跳出循环
    moveA = moveA.next if moveA else headB
  ```
    
 

  
  
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
  
  23.合并两个/k个有序列表
  ```
  dummyhead = ListNode()
  prev = dummy
  while list1 and list2:
    if list1.val<list2.val:
      prev.next = list1
      list1 = list1.next
    else:
      prev.next = list2
      list2 = list2.next
    prev = prev.next
  if list1:
    prev.next = list1
  elif list2:
    prev.next = list2
  return dummyhead.next
  ```
  
  合并k个有序列表是在合并两个列表的基础上，用分治合并两两merge链表
  ```
  def merge(left, right):
    if left == right:
      return lists[left]
    if left > right:
      return None
    mid = left + (right-left)//2
    return mergeTwoLists(merge(left, mid),merge(mid+1, right))
  ```
  

