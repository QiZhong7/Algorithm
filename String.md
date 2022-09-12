## 1、计算器

用preSign记录当前指针之前的符号，用num记录当前的数值，再用stack记录所有需要加减的情况。
```
class Solution:
    def calculate(self, s: str) -> int:
        n = len(s)
        stack = []
        preSign = '+'
        num = 0
        for i in range(n):
            if s[i] != ' ' and s[i].isdigit():
                num = num * 10 + int(s[i])
            if i == n - 1 or s[i] in '+-*/':
                if preSign == '+':
                    stack.append(num)
                elif preSign == '-':
                    stack.append(-num)
                elif preSign == '*':
                    stack.append(stack.pop() * num)
                else:
                    stack.append(int(stack.pop() / num))
                preSign = s[i]
                num = 0
        return sum(stack)
```


基本计算器

```
#没有乘除号，多了括号，本质是把括号拆开，变成纯粹只有一个加减号的算法。
#利用栈拆开括号，如果是减号则把括号里的全部符号取反。
class Solution:
    def calculate(self, s: str) -> int:
        bracketstack = [1]
        sign = 1
        num = 0
        i = 0
        n = len(s)
        res = 0
        while i<n:
            if s[i] == "+":
                sign = bracketstack[-1]
                i+=1
            elif s[i] == "-":
                sign = -bracketstack[-1]
                i+=1
            elif s[i] == "(":
                bracketstack.append(sign)
                i+=1
            elif s[i] == ")":
                bracketstack.pop()
                i+=1
            elif s[i] == " ":
                i+=1
            else:
                num= 0
                while i<n and s[i].isdigit():
                    num = num*10 + int(s[i])
                    i+=1
                res += num*sign
        return res
```
