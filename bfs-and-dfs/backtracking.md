## 回溯定义
>Backtracking is a general algorithm for finding all (or some) solutions to some computational problem, that incrementally builds candidates to the solutions, and abandons each partial candidate c ("backtracks") as soon as it determines that c cannot possibly be completed to a valid solution.   ----[Wikipedia](https://en.wikipedia.org/wiki/Backtracking)

假设要从点A去点B，一开始会发现有好几条道可走，当选择某个岔口，走到一定的地方会发现又有几条岔道可供选择，当然每次只能选择一个岔口。

如果能最终走到B，挺好；但是经常会发现走到了尽头去到了另一个目的地。此时只好返回到最近的一个路口C，重新选择一条从C出发的但没有走过的岔口。如果所有从C出发的岔口都走完还是没能到目的地，那继续回到C上一层的岔口。最终要么找到了通往B的路，要么无路可通

## 回溯与DFS
- 回溯是一种找路方法，搜索的时候走不通就回头换路接着走，直到走通了或者发现此山根本不通。
- DFS是一种开路策略，就是一条道先走到头，再往回走一步换一条路走到头，这也是回溯用到的策略。在树和图上回溯时人们叫它DFS。


## 回溯的题型
通常需要穷举的就可以考虑回溯。
比如all sub sets, all path from root to leaf诸如此类的
求所有解的个数
求所有解的具体信息