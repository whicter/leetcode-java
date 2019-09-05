# Union Find

# Related Definition

## Disjoint Set
A disjoint-set data structure is a data structure that keeps track of a set of elements partitioned into a number of disjoint (non-overlapping) subsets.

## Union Find Algorithm
A union-find algorithm is an algorithm that performs two useful operations on such a data structure:

Find: Determine which subset a particular element is in. This can be used for determining if two elements are in the same subset.

## 需要解决的基本问题抽象化
1. 有一堆节点
2. union操作： 把两个节点连在一起
3. find操作： 两个节点是否存在一条路径连到一起？

## 应用场景
1. 判断网络上的电脑是否相连？道路是否相通？互联网上的网页是否相连？
2. 同名变量的识别
3. 照片上的点？ (假设颜色完全一样称为相连, 比如photoshop里面就用到类似的技术)


## 思路一
每次union的时候，找到所有j对应的parent，都把他改成i对应的parent， 这样，每次union完以后，属于同一个connected component的节点的parent都会被更新到同一个值

实现方法如下：
``` java
public class UnionFind1_QuickFind {

    private int[] parents;
    public UnionFind1_QuickFind(int n) {
        parents = new int[n];
        for(int i = 0; i < n; ++i) {
            parents[i] = i;
        }
    }
    void union(int i, int j) {
        int oldParent = parents[j];
        for(int k = 0; k < parents.length; ++k) {
            if(parents[k] == oldParent) {
                parents[k] = parents[i];
            }
        }
    }
    boolean find(int i, int j) {
        return parents[i] == parents[j];
    }

}
```

## 思路二
1. 建立一个root表，保存最开始union的那个节点， 每次union的时候把root更新一下，
2. 通过判断两个节点的root来判断是否相通
3. find的时候就要遍历所有connected component里面的节点才可能判断是否相连。 相当于只是把思路一union的所有复杂度转移到find

实现方法如下：
``` java
class UnionFind2_QuickUnion {
    private int[] roots;
    public UnionFind2_QuickUnion(int n) {
        roots = new int[n];
        for(int i = 0; i < n; ++i) {
            roots[i] = i;
        }
    }

    public int findRoot(int i) {
        while(roots[i] != i) {
            // Path Compression
            parent[i] = parent[parent[i]];
            i = roots[i];
        }
        return i;
    }

    public boolean find(int i, int j) {
        return findRoot(i) == findRoot(j);
    }

    public void union(int i, int j) {
        int rootOfi = findRoot(i);
        int rootOfj = findRoot(j);
        roots[rootOfj] = rootOfi;
    }
}
```

## Refrence
http://www.noteanddata.com/classic-algorithm-union-find-1.html

