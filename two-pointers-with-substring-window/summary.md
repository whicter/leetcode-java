two pointers方法需要确定
何时两个pointers终止移动跳出循环，能够包含所有情况。这里仍然是left&right pointers相遇。
何时移动左右pointers。灌水多少不仅与两个柱子的高度有关，也与两个柱子的距离有关。如何使得存放的水更多呢？较短的那一个柱子决定了灌水的area，因此可以移动指向较短的柱子的pointer，对于相会的pointer，一般趋势均为向中间移动，因此如果 heights[left] < heights[right]，则left++，反之right--。