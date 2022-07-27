# 一、分治
##例题
169.多数元素


# 二、Boyer-Moore投票算法
##例题
<p>
169.多数元素
维护一个候选众数**candidate**,和他出现的次数**count**。**candidate**可以为任意值，**count**为0。
遍历数组中的所有元素，对于每个元素**x**，如果**count**的值为0，就将**x**赋予给**candidate**，随后判断**x**：
  1.如果x与candidate相等，那么count增加1
  2.如果x与candidate不等，那么count减少1
遍历完，**candidate**的值即为整个数组的众数
</p>
