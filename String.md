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

## 2. 括号

```
class Solution:
    def minRemoveToMakeValid(self, s: str) -> str:
        #存放能对应括号
        stack = []
        #有些特殊情况，比如stack为空但是遇到一个右括号，还有在字符串末尾遇到一个左括号，这时候直接加到location列表里
        location = []

        n = len(s)
        for i in range(n):
            if s[i] not in "()":
                continue
            if s[i] == "(":
                stack.append(i)
            elif s[i] == ")" and stack:
                stack.pop()      
            else:
                location.append(i)
        string = list(s)
        location = location+stack
        for i in location:
            string[i] = ""
        return "".join(string)

```

返回所有可能性
```
class Solution:
    def removeInvalidParentheses(self, s: str) -> List[str]:
        self.res = []
        lremove, rremove = 0, 0
        for i in s:
            if i == "(":
                lremove += 1
            elif i == ")":
                if lremove == 0:
                    rremove += 1
                else:
                    lremove -= 1

        def Valid(str):
            cnt = 0
            for c in str:
                if c == '(':
                    cnt += 1
                elif c == ')':
                    cnt -= 1
                    if cnt < 0:
                        return False
            return cnt == 0


        def helper(string, start, lremove, rremove):
            
            if lremove ==0 and rremove == 0:
                if Valid(string):
                    self.res.append(string)
                    return
            
            for i in range(start, len(string)):
                if i > start and string[i] == string[i - 1]:
                    continue
                if lremove+rremove > len(string)-i:
                    break
                if string[i] == "(" and lremove > 0:
                    helper(string[:i]+string[i+1:], i, lremove-1, rremove)
                if string[i] == ")" and rremove > 0:
                    helper(string[:i]+string[i+1:], i, lremove, rremove-1)
        
        helper(s, 0, lremove, rremove)
        return self.res
        


```
