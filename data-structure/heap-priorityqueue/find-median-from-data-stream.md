# 295. Find Median from Data Stream
### 题目描述
> Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.
>
> For example,
[2,3,4], the median is 3
[2,3], the median is (2 + 3) / 2 = 2.5
>
> Design a data structure that supports the following two operations:
- void addNum(int num) - Add a integer number from the data stream to the data structure.
- double findMedian() - Return the median of all elements so far.
 

#### Example:

    addNum(1)
    addNum(2)
    findMedian() -> 1.5
    addNum(3) 
    findMedian() -> 2
     

**Follow up:**

- If all integer numbers from the stream are between 0 and 100, how would you optimize it?
- If 99% of all integer numbers from the stream are between 0 and 100, how would you optimize it?


[原题链接](https://leetcode.com/problems/meeting-rooms-ii/)

### 解题思路
维护一个最大堆，一个最小堆。
最大堆存的是到目前为止较小的那一半数，最小堆存的是到目前为止较大的那一半数，这样中位数只有可能是某个堆顶或者堆顶两个数的均值。

维护两个堆时判断堆顶数和新来的数的大小关系，还有两个堆的大小关系。新数加入堆后，要保证两个堆的大小之差不超过1。

### 复杂度
时间 O(NlogN) 空间 O(N)

#### Java代码实现
```java
class MedianFinder {
    
    private PriorityQueue<Integer> maxheap; // storing "smaller" numbers
    private PriorityQueue<Integer> minheap; // storing "bigger" numbers
    
    /** initialize your data structure here. */
    public MedianFinder() {
        maxheap = new PriorityQueue<>(Comparator.reverseOrder());
        minheap = new PriorityQueue<>(Integer::compareTo);
    }
    
    public void addNum(int num) {
        if (maxheap.isEmpty() || maxheap.peek() > num) {
            maxheap.offer(num);
        } else {
            minheap.offer(num);
        }
        
        int size1 = maxheap.size();
        int size2 = minheap.size();
        
        if (size1- size2 > 1) {
           minheap.offer(maxheap.poll()); 
        } else if (size2 - size1 > 1) {
            maxheap.offer(minheap.poll());
        }
    }
    
    public double findMedian() {
        int size1 = maxheap.size();
        int size2 = minheap.size();
        return size1 == size2 ? (maxheap.peek() + minheap.peek()) * 1.0 / 2 : (size1 > size2 ? maxheap.peek() : minheap.peek());
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```