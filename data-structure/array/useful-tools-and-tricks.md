# Useful Tools and Tricks

## Quick Select

```java
public int partition(int[]nums, int leftIndex, int rightIndex) {
    int pivot = nums[rightIndex];
    int partition = leftIndex;
    for (int i = leftIndex; i < rightIndex; i++) {
        if (nums[i] <= pivot) {
            swap(nums, partition++, i);
        }
    }
    swap(nums, partition, rightIndex);

    //System.out.println(Arrays.toString(nums));
    return partition;
}
```
**Sample problem:** [LeeCode 215. Kth Largest Element in an Array](data-structure/array/kth-largest-element-in-an-array.md)

## Iterate over the array twice

Iterate the array from beginning to end and then from end to beginning. Then combine the results

**Sample problem:** [LeeCode 238. Product of Array Except Self](data-structure/array/shortest-word-distance.md)





