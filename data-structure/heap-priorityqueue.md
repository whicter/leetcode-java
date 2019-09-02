# Heap

## Time Complexity
- offer(), poll(), remove(), add(): O(log N)
- remove(Object), contains(Object): O(N)；

## Max / Min Heap Choice
需要找最大k的时候用Min Heap，这样当有新的更大的元素出现可以很容易把堆顶最小元素剔除