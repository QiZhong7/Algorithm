# 一、用栈实现队列
## 例题

232.用栈实现队列

将一个栈当作输入栈，用于压入push() 传入的数据；另一个栈当作输出栈，用于 pop() 和peek() 操作。

每次 pop()或者peek()时，若输出栈为空则将输入栈的全部数据依次弹出并压入输出栈，这样输出栈从栈顶往栈底的顺序就是队列从队首往队尾的顺序。

```
class MyQueue:

    def __init__(self):
        self.instack = []
        self.outstack = []

    def push(self, x: int) -> None:
        self.instack.append(x)

    def pop(self) -> int:
        if len(self.outstack) == 0:
            self.in2out()
        return self.outstack.pop()

    def peek(self) -> int:
        if len(self.outstack):
            return self.outstack[-1]
        if len(self.instack):
            return self.instack[0]

    def empty(self) -> bool:
        if len(self.instack) or len(self.outstack):
            return False
        return True

    def in2out(self):
        while self.instack:
            self.outstack.append(self.instack.pop())
```
