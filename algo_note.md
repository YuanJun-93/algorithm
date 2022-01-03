### 数组

#### 704. 二分查找

https://leetcode-cn.com/problems/binary-search/

```go
func search(nums []int, target int) int {
    left := 0
    right := len(nums) - 1
    for left <= right {
        mid := left + (right - left) / 2
        if nums[mid] == target {
            return mid
        }else if nums[mid] > target {
            right = mid - 1
        }else if nums[mid] < target {
            left = mid + 1
        }
    }
    return -1
}
```

#### 27. 移除元素

https://leetcode-cn.com/problems/remove-element/

```go
func removeElement(nums []int, val int) int {
    left := 0
    for right := 0; right < len(nums); right++ {
        if nums[right] != val {
            nums[left] = nums[right]
            left++
        }
    }
    return left
}
```

#### 977. 有序数组的平方

https://leetcode-cn.com/problems/squares-of-a-sorted-array/

```go
func sortedSquares(nums []int) []int {
    n := len(nums)
    left, right, k := 0, n-1, n-1
    arr := make([]int, n)
    for left <= right {
        if nums[left]*nums[left] > nums[right]*nums[right] {
            arr[k] = nums[left]*nums[left]
            left++
        }else{
            arr[k] = nums[right]*nums[right]
            right--
        }
        k--
    }
    return arr
}
```

#### 209. 长度最小的子数组

https://leetcode-cn.com/problems/minimum-size-subarray-sum/

```go
func minSubArrayLen(target int, nums []int) int {
    sum := 0
    length := 0
    res := len(nums) + 1
    left := 0
    for i := 0; i < len(nums); i++ {
        sum += nums[i]
        for sum >= target {
            length = (i - left + 1)
            res = min(res, length)
            sum -= nums[left]
            left++
        }
    }
    if res == len(nums) + 1 {
        return 0
    }
    return res
}

func min(a,b int) int {
    if a < b {
        return a
    }
    return b
}
```

#### 59. 螺旋矩阵2

https://leetcode-cn.com/problems/spiral-matrix-ii/

```go
func generateMatrix(n int) [][]int {
    left, right := 0, n-1
    top, bottom := 0, n-1
    index := 1
    step := n*n
    matrix := make([][]int, n)
    for i := 0; i < n; i++ {
        matrix[i] = make([]int, n)
    }
    for index <= step {
        for i := left; i <= right; i++ {
            matrix[top][i] = index
            index++
        }
        top++
        for i := top; i <= bottom; i++ {
            matrix[i][right] = index
            index++
        }
        right--
        for i := right; i >= left; i-- {
            matrix[bottom][i] = index
            index++
        }
        bottom--
        for i := bottom; i >= top; i-- {
            matrix[i][left] = index
            index++
        }
        left++
    }
    return matrix
}
```

### 链表

#### 203. 移除链表元素

https://leetcode-cn.com/problems/remove-linked-list-elements/

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func removeElements(head *ListNode, val int) *ListNode {
    newHead := &ListNode{}
    newHead.Next = head
    cur := newHead
    for cur != nil && cur.Next != nil {
        if cur.Next.Val == val {
            cur.Next = cur.Next.Next
        }else{
            cur = cur.Next
        }
    }
    return newHead.Next
}
```

#### 707. 设计链表

https://leetcode-cn.com/problems/design-linked-list/

#### 206. 反转链表

https://leetcode-cn.com/problems/reverse-linked-list/

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseList(head *ListNode) *ListNode {
    var pre *ListNode
    cur := head
    for cur != nil {
        next := cur.Next
        cur.Next = pre
        pre = cur
        cur = next
    }
    return pre
}
```

#### 24. 两两交换链表中的节点

https://leetcode-cn.com/problems/swap-nodes-in-pairs/

```go
// 虚拟头结点
func swapPairs(head *ListNode) *ListNode {
    dummy := &ListNode{
        Next: head,
    }
    cur := dummy
    for cur.Next != nil && cur.Next.Next != nil {
        tmp := cur.Next
        tmp1 := cur.Next.Next.Next

        cur.Next = cur.Next.Next
        cur.Next.Next = tmp
        cur.Next.Next.Next = tmp1

        cur = cur.Next.Next
    }
    return dummy.Next
}
```

```go
// 递归
func swapPairs(head *ListNode) *ListNode {
    if head == nil || head.Next == nil {
        return head
    }
    next := head.Next
    newHead := swapPairs(next.Next)
    next.Next = head
    head.Next = newHead
    return next
}
```

#### 19. 删除链表的倒数第N个结点

https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/

```go
func removeNthFromEnd(head *ListNode, n int) *ListNode {
    dummy := &ListNode{
        Next: head,
    }
    slow := dummy
    fast := dummy
    for n > 0 && fast != nil {
        fast = fast.Next
        n--
    }
    fast = fast.Next
    for fast != nil {
        fast = fast.Next
        slow = slow.Next
    }  
    slow.Next = slow.Next.Next
    return dummy.Next
}
```

#### 面试题 02.07. 链表相交

https://leetcode-cn.com/problems/intersection-of-two-linked-lists-lcci/

```go
func getIntersectionNode(headA, headB *ListNode) *ListNode {
    curA := headA
    curB := headB
    lenA, lenB := 0, 0
    for curA != nil {
        lenA++
        curA = curA.Next
    }
    for curB != nil {
        lenB++
        curB = curB.Next
    }
    curA = headA
    curB = headB
    if lenB > lenA {
        lenA, lenB = lenB, lenA
        curA, curB = curB, curA
    }
    gap := lenA - lenB
    for gap > 0 {
        curA = curA.Next
        gap--
    }
    for curA != nil {
        if curA == curB {
            return curA
        }
        curA = curA.Next
        curB = curB.Next
    }
    return nil
}
```

#### 142. 环形链表2

https://leetcode-cn.com/problems/linked-list-cycle-ii/

```go
func detectCycle(head *ListNode) *ListNode {
    slow := head
    fast := head
    for fast != nil && fast.Next != nil {
        slow = slow.Next
        fast = fast.Next.Next
        if slow == fast {
            index1 := fast
            index2 := head
            for index1 != index2 {
                index1 = index1.Next
                index2 = index2.Next
            }
            return index2
        }
    }
    return nil
}
```

