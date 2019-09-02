# Binary Search

## Binary Search Basic Template
须仔细体会循环终结条件
### Recursion
``` java
int binarySearch(int arr[], int start, int end, int x) { 
    if (start <= end) { 
        int mid = start + (end - start) / 2; 

        // If the element is present at the 
        // middle itself 
        if (arr[mid] == x) 
            return mid; 

        // If element is smaller than mid, then 
        // it can only be present in left subarray 
        if (arr[mid] > x) 
            return binarySearch(arr, start, mid - 1, x); 

        // Else the element can only be present 
        // in right subarray 
        return binarySearch(arr, mid + 1, end, x); 
    } 

    // We reach here when element is not present 
    // in array 
    return -1; 
} 
```

### Iteration
```java
int binarySearch(int arr[], int start, int end, int x) { 

    while (start <= end) { 
        int mid = start + (end - start) / 2; 

        // If the element is present at the 
        // middle itself 
        if (arr[mid] == x) 
            return mid; 

        // If element is smaller than mid, then 
        // it can only be present in left subarray 
        if (arr[mid] > x) 
            end = mid - 1;

        // Else the element can only be present 
        // in right subarray 
        end = mid + 1;
    } 

    // We reach here when element is not present 
    // in array 
    return -1; 
} 

```