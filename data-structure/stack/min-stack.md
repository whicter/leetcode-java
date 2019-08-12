# 155. Min Stack

### 题目描述

> Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.
- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.

#### Example:
    MinStack minStack = new MinStack();
    minStack.push(-2);
    minStack.push(0);
    minStack.push(-3);
    minStack.getMin();   --> Returns -3.
    minStack.pop();
    minStack.top();      --> Returns 0.
    minStack.getMin();   --> Returns -2.




[原题链接](https://leetcode.com/problems/min-stack/)

### 解题思路
- 每次push的时候需要对min进行维护：小于当前min的时候更新min，同时把之前的min压入栈
- 每次pop的时候需要对min进行维护：如果pop的是当前min，需要将2nd min也pop同时更新min的值

#### Java代码实现：

```java
class MinStack {
    private int min = Integer.MAX_VALUE;
    private Stack<Integer> stack = new Stack<>();

    /** initialize your data structure here. */
    public MinStack() {
    
    }
    
    public void push(int x) {
        // push the older min when min is changed
        // this can help to track the next min when the min value is poped
        // basically the local min value is pushed twise:
        // 1. when the number appears 2. when it is replaced by a smaller value regarding min
        
        if (x <= min) {
            stack.push(min);
            min = x;
        }
        stack.push(x);
        
    }
    
    public void pop() {
        // if the number poped is the min value
        // do another pop to update the min
        // and keep the top value to be the correct one
        if (stack.pop() == min) {
            min = stack.pop();
        }
    }
    
    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return this.min;
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```



