## level: simple

#### 对称二叉树

[原题地址](https://leetcode-cn.com/problems/symmetric-tree/)

***题目：***

```
给定一个二叉树，检查它是否是镜像对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

    1
   / \
  2   2
 / \ / \
3  4 4  3

但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

    1
   / \
  2   2
   \   \
   3    3

进阶：

你可以运用递归和迭代两种方法解决这个问题吗？
```

***思考：***

Q:  满足对称的条件？
A:  拥有相同的根节点 && 每个子树左节点 == 另一子树的右节点（值相等）

我们可以实现这样一个递归函数，通过「同步移动」两个指针(p, q)的方法来遍历这棵树，一开始都指向这棵树的根，随后p右移时，q左移，p左移时，q 右移。每次检查当前 p 和 q 节点的值是否相等。
```js
const check = (p: TreeNode, q: TreeNode) => {
  // 特殊情况优先判断
  if(!q && !p) return true;

  // root一样理论上不会出现
  if(!q || !p) return false;

  // 所有子结点都满足 最终才是true
  return p.val === q.val && check(q.left, p.right) && check(q.right, p.left);

}

var isSymmetric = function(root: TreeNode | null): boolean {
    return check(root, root);
};

```