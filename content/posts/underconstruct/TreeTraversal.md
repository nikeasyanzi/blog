# [5.Binary Tree](/binaryTree.md)

## [145. Binary Tree Postorder Traversal](/questions/TreeTraversal.md)
```go

func postOrder(root *TreeNode, arr []int)[] int{
    if( root ==nil ) {
        return arr
    }
    arr=postOrder (root.Left,arr)
    arr=postOrder (root.Right,arr)
    arr=append(arr,root.Val) 
    return arr
}
func postorderTraversal(root *TreeNode) []int {
    var result []int
    result=postOrder(root,result)
    return result
}
```
## [94. Binary Tree Inorder Traversal](/questions/TreeTraversal.md)
```go

func inOrder(root *TreeNode, arr []int)[] int{
    if( root ==nil ) {
        return arr
    }
    arr=inOrder (root.Left,arr)
    arr=append(arr,root.Val) 
    arr=inOrder (root.Right,arr)
    return arr
}

func inorderTraversal(root *TreeNode) []int {
        var result []int
    result=inOrder(root,result)
    return result
}
```

## [230. Kth Smallest Element in a BST](/questions/TreeTraversal.md)
剛好 binary tree inorder 爬出來
找k-1 個 即可
      
```go
func inorderTraversal(root *TreeNode,arr [] int) []int {
    if( root ==nil ) {
        return arr
    }
    arr=inorderTraversal (root.Left,arr)
    arr=append(arr,root.Val) 
    arr=inorderTraversal (root.Right,arr)
    return arr
}


func kthSmallest(root *TreeNode, k int) int {
    var result []int
    result= inorderTraversal(root,result)
    return result[k-1]
}
```