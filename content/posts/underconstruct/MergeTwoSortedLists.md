
#[ 4.Linked List](/LinkedList.md)

## 21. Merge Two Sorted Lists

很簡單的題目

https://leetcode.com/problems/merge-two-sorted-lists/description/

```go
func addNode(val int, head *ListNode) *ListNode {

    var curr *ListNode

    var node ListNode
    node.Val = val
    node.Next = nil

    curr = head
    if head == nil {
        head = &node
    } else {
        for curr.Next != nil {
            curr = curr.Next
        }
        curr.Next = &node
    }
    return head
}


func mergeTwoLists(l1 *ListNode, l2 *ListNode) *ListNode {
    var l1ptr *ListNode
    var l2ptr *ListNode
    var l3ptr *ListNode

    l1ptr = l1
    l2ptr = l2

    for l1ptr != nil && l2ptr != nil {

        if l1ptr.Val > l2ptr.Val {
            l3ptr = addNode(l2ptr.Val, l3ptr)
            l2ptr = l2ptr.Next
        } else {
            if l1ptr.Val < l2ptr.Val {
                l3ptr = addNode(l1ptr.Val, l3ptr)
                l1ptr = l1ptr.Next
            } else { //equal, so we add both node
                l3ptr = addNode(l1ptr.Val, l3ptr)
                l3ptr = addNode(l2ptr.Val, l3ptr)

                l1ptr = l1ptr.Next
                l2ptr = l2ptr.Next
            }
        }

    }
    //add the rest node
    for l1ptr != nil {
        l3ptr = addNode(l1ptr.Val, l3ptr)
        l1ptr = l1ptr.Next
    }
    for l2ptr != nil {
        l3ptr = addNode(l2ptr.Val, l3ptr)
        l2ptr = l2ptr.Next
    }

    return l3ptr

}
```