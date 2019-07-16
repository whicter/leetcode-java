## Quick Select
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
**Sample problem:** LeeCode 215. Kth Largest Element in an Array




