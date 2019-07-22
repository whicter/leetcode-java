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

## 基本思路
1. 建立一个root表，保存最开始union的那个节点， 每次union的时候把root更新一下，
2. 通过判断两个节点的root来判断是否相通

Leetcode 684为基本模板