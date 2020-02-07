

### 递归算法

最简单的思路应该是递归。首先我们按照递归的思路来分析一下。

1. 当前树的中序遍历结果，需要组合左子树中序遍历的结果，根节点的值和右子树中序遍历的结果得到。
2. 左右子树的中序遍历又是完全一样的新问题。
3. 递归的终止条件应该为当前的根节点为空。

以下为go语言版的二叉树中序遍历


```go
func inorderTraversal(root *TreeNode) []int {
    if root == nil {
        return []int{}
    }
    leftSlice := inorderTraversal(root.Left)
    result := append(leftSlice, root.Val)
    return append(result, inorderTraversal(root.Right)...)
}
```

### 迭代算法



