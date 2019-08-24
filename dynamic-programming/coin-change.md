# 322. Coin Change
### 题目描述
> You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

#### Example 1:

    Input: coins = [1, 2, 5], amount = 11
    Output: 3 
    Explanation: 11 = 5 + 5 + 1
    
#### Example 2:

    Input: coins = [2], amount = 3
    Output: -1
    
**Note:**
You may assume that you have an infinite number of each kind of coin.
    
[原题链接](https://leetcode.com/problems/coin-change/)

### 解题思路
定义原子操作$$f(i)$$为min combination to achieve amount $$i$$

$$f(i)$$ = $$Min\{ f(i - coin[j] + 1) \}$$, for all $$coin[j]< = i$$


于此同时维护global

#### Java 代码实现
```java
public class Solution {
    public int coinChange(int[] coins, int amount) {
        int max = amount + 1;          
        int[] dp = new int[amount + 1];  
        
        // fill dp array with max indicating no combination is achievable 
        Arrays.fill(dp, max);  
        dp[0] = 0; // 0 coins needed for 0 amount
        
        for (int i = 1; i <= amount; i++) {
            for (int j = 0; j < coins.length; j++) {
                if (coins[j] <= i) {
                    dp[i] = Math.min(dp[i], dp[i - coins[j]] + 1);
                }
            }
        }
        return dp[amount] >= max ? -1 : dp[amount];
    }
}
```


