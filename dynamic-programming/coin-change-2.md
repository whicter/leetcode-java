# 518. Coin Change 2
### 题目描述
> You are given coins of different denominations and a total amount of money. Write a function to compute the number of combinations that make up that amount. You may assume that you have infinite number of each kind of coin.
 
#### Example 1:

    Input: amount = 5, coins = [1, 2, 5]
    Output: 4
    Explanation: there are four ways to make up the amount:
    5=5
    5=2+2+1
    5=2+1+1+1
    5=1+1+1+1+1
    
#### Example 2:

    Input: amount = 3, coins = [2]
    Output: 0
    Explanation: the amount of 3 cannot be made up just with coins of 2.

#### Example 3:

    Input: amount = 10, coins = [10] 
    Output: 1

    
[原题链接](https://leetcode.com/problems/coin-change-2/)

### 解题思路
定义原子操作$$f(i)$$为total combination to achieve amount $$i$$

$$f(i)$$ = $$Sum\{ f(i - coin[j]) \}$$, for all $$coin[j]< = i$$

#### Java 代码实现
```java
class Solution {
    public int change(int amount, int[] coins) {
        int[] dp = new int[amount + 1];
        dp[0] = 1; // 1 way to form 0 target amount
        for (int coin : coins) {
            for (int targetAmout = 1; targetAmout <= amount; targetAmout++) {
                if (targetAmout >= coin) {
                    dp[targetAmout] += dp[targetAmout - coin];
                }
            }
        }
        return dp[amount];
    }
}
```


