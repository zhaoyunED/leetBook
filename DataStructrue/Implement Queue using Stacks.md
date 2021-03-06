#Implement Queue using Stacks
Implement the following operations of a queue using stacks.

push(x) -- Push element x to the back of queue.

pop() -- Removes the element from in front of queue.

peek() -- Get the front element.

empty() -- Return whether the queue is empty.

Notes:
You must use only standard operations of a stack -- which means only push to top, peek/pop from top, size, and is empty operations are valid.
Depending on your language, stack may not be supported natively. You may simulate a stack by using a list or deque 
(double-ended queue), as long as you use only standard operations of a stack.

You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).


---

思路：

利用两个stack 来实现

插入元素时先放入input
返回队首元素时先看看output栈里是否有元素，若有的话，直接返回output栈顶元素，若没有的话先将input栈里元素一个个push到output栈中，再返回栈顶元素。

```
class Queue {
    stack<int> input,output;
public:
    // Push element x to the back of queue.
    void push(int x) {
        input.push(x);
    }

    // Removes the element from in front of queue.
    void pop(void) {
        peek();
        output.pop();
    }

    // Get the front element.
    int peek(void) {
        if(output.empty())
        {
            while(!input.empty())
             output.push(input.top()),input.pop();
        }
        return output.top();
    }

    // Return whether the queue is empty.
    bool empty(void) {
        return input.empty() && output.empty();
    }
};
```