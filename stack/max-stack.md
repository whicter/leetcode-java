# 716. Max Stack

### 题目描述

> Design a max stack that supports push, pop, top, peekMax and popMax.
- push(x) -- Push element x onto stack.
- pop() -- Remove the element on top of the stack and - return it.
- top() -- Get the element on the top.
- peekMax() -- Retrieve the maximum element in the stack.
- popMax() -- Retrieve the maximum element in the stack, and remove it. If you find more than one maximum elements, only remove the top-most one.

#### Example:
    MaxStack stack = new MaxStack();
    stack.push(5); 
    stack.push(1);
    stack.push(5);
    stack.top(); -> 5
    stack.popMax(); -> 5
    stack.top(); -> 1
    stack.peekMax(); -> 5
    stack.pop(); -> 1
    stack.top(); -> 5


**Note: **
1. -1e7 <= x <= 1e7
2. Number of operations won't exceed 10000.
3. The last four operations won't be called when stack is empty.

[原题链接](https://leetcode.com/problems/max-stack/)

### 解题思路一
难点在于popmax，需要把当前max stack的peek 从stack里面remove掉，同时更新当前的max，用个temp stack解决，存储当前的Integer到max的值，然后再存储回来；

### Java代码实现：

```java
class MaxStack {
    Stack<Integer> stack;
    Stack<Integer> maxStack;
    
    /** initialize your data structure here. */
    public MaxStack() {
        stack = new Stack<Integer>();
        maxStack = new Stack<Integer>();
    }
    
    public void push(int x) {
        stack.push(x);
        
        if (maxStack.isEmpty() || x >= maxStack.peek()) {
            maxStack.push(x);
        } 
    }
    
    public int pop() {
        int value = stack.pop();
        if (!maxStack.isEmpty() && value == maxStack.peek()) {
            maxStack.pop();
        }
        return value;
    
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int peekMax() {
        return maxStack.peek();
    }
    
    public int popMax() {
        int value = maxStack.pop();
        
        Stack<Integer> temp = new Stack<Integer>();
        while (stack.peek() != value){
            temp.push(stack.pop());
        }
        stack.pop();
        while (!temp.isEmpty()) {
            this.push(temp.pop()); // need to update maxStack meantime
        }
        return value;
    }
}


/**
 * Your MaxStack object will be instantiated and called as such:
 * MaxStack obj = new MaxStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.peekMax();
 * int param_5 = obj.popMax();
 */
```

### 解题思路二
为了使popMax操作复杂度更小，考虑使用双向列表 + TreeMap
TreeMap基于红黑树（Red-Black tree）实现。该映射根据其键的自然顺序进行排序，或者根据创建映射时提供的 Comparator 进行排序，具体取决于使用的构造方法。
TreeMap的基本操作 containsKey、get、put 和 remove 的时间复杂度是 log(n) 。

### Java 代码实现
```java
class MaxStack {

    /** initialize your data structure here. */
    private Node head;
    private Node tail;
    private TreeMap<Integer, List<Node>> map;
    
    public MaxStack() {
        map = new TreeMap();
        head = new Node(-1);
        tail = new Node(-1);

        head.next = tail;
        tail.pre = head;
    }
    
    public void push(int x) {
        Node node = new Node(x);
        node.pre = tail.pre;
        tail.pre.next = node;
        node.next = tail;
        tail.pre = node;

        if (!map.containsKey(x)) {
            map.put(x, new ArrayList());
        }
        map.get(x).add(node);
    }
    
    public int pop() {
        Node last = tail.pre;
        last.pre.next = last.next;
        tail.pre = last.pre;
        
        List<Node> list = map.get(last.val);
        list.remove(list.size() - 1);

        if (list.size() == 0) {
            map.remove(last.val);
        }
        
        return last.val;
    }
    
    public int top() {
        return tail.pre.val;
    }
    
    public int peekMax() {
        List<Node> list = map.lastEntry().getValue();
        return list.get(list.size() - 1).val;    
    }
    
    public int popMax() {
        List<Node> list = map.lastEntry().getValue();
        Node max = list.remove(list.size() - 1);
        
        if (list.size() == 0) {
            map.remove(max.val);
        }
        
        max.pre.next = max.next;
        max.next.pre = max.pre;
        
        return max.val;
    }
    
    private class Node {
        private int val;
        private Node pre;
        private Node next;
        public Node(int val) {
            this.val = val;
        }
    }
}

```



