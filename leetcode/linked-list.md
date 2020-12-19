# Linked-list

+ [Sort List](#sort-list)
+ [Intersection of Two Linked Lists](#intersection-of-two-linked-lists)
+ [Reorder List](#reorder-list)
+ [Linked List Cycle](#linked-list-cycle)
+ [Linked List Cycle II](#linked-list-cycle-ii)
+ [Remove Nth Node From End of List](#remove-nth-node-from-end-of-list)
+ [Merge Two Sorted Lists](#merge-two-sorted-list)
+ [Palindrome Linked List](#palindrome-linked-list)
+ [Middle of the Linked List](#middle-of-the-linked-list)
+ [Reverse Linked List](#reverse-linked-list)

## Sort List

https://leetcode.com/problems/sort-list/

```python
def merge(self, left: ListNode, right: ListNode) -> ListNode:
    head = ListNode(0)
    current = head
    while left and right:
        if left.val <= right.val:
            current.next = left
            left = left.next
        else:
            current.next = right
            right = right.next
        current = current.next
    if not left:
        current.next = right
    elif not right:
        current.next = left
    return head.next


def sortList(self, head: ListNode) -> ListNode:
    if not head or not head.next:
        return head

    mid = head
    temp = head
    while mid.next and temp.next and temp.next.next:
        mid = mid.next
        temp = temp.next.next

    right = self.sortList(mid.next)
    mid.next = None
    left = self.sortList(head)
    return self.merge(left, right)
```

## Intersection of Two Linked Lists

https://leetcode.com/problems/intersection-of-two-linked-lists/

```python
def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
    currentA = headA
    currentB = headB
    while currentA != currentB:
        if not currentA:
            currentA = headB
        else:
            currentA = currentA.next
        if not currentB:
            currentB = headA
        else:
            currentB = currentB.next
    return currentA
```

## Reorder List

https://leetcode.com/problems/reorder-list/

```python
def reorderList(self, head: ListNode) -> None:
    if not head:
        return head
    data = []
    current = head
    i, j = 0, -1
    while current:
        data.append(current)
        current = current.next
        j += 1
    while i < j:
        data[i].next = data[j]
        i += 1
        if i >= j:
            break
        data[j].next = data[i]
        j = j - 1
    data[j].next = None


def reorderList(self, head: ListNode) -> None:
    if not head:
        return head

    mid = head
    temp = head
    while mid.next and temp.next and temp.next.next:
        mid = mid.next
        temp = temp.next.next

    tail = mid
    previous = None
    half = mid.next
    while half:
        mid.next = previous
        previous = mid
        mid = half
        half = half.next
    mid.next = previous
    current = None
    while current != tail:
        current = head.next
        head.next = mid
        head = mid
        mid = current
```

## Linked List Cycle

https://leetcode.com/problems/linked-list-cycle/

```python
def hasCycle(self, head: ListNode) -> bool:
    if not head:
        return False
    slow = head
    fast = head.next
    while fast and fast != slow:
        fast = fast.next
        if not fast:
            return False
        slow = slow.next
        fast = fast.next
    if slow == fast:
        return True
    return False
```

## Linked List Cycle II

https://leetcode.com/problems/linked-list-cycle-ii/

```python
def detectCycle(self, head: ListNode) -> ListNode:
    if not head:
        return None
    slow = head
    fast = head.next
    while fast and fast != slow:
        fast = fast.next
        if not fast:
            return None
        slow = slow.next
        fast = fast.next
    if slow == fast:
        current = head
        fast = fast.next
        while current != fast:
            current = current.next
            fast = fast.next
        return current
    return None
```

## Remove Nth Node From End of List

https://leetcode.com/problems/remove-nth-node-from-end-of-list/

```python
def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
    start = ListNode(0)
    start.next = head
    
    first = start
    second = start
    for i in range(1, n + 2):
        first = first.next
    while first:
        first = first.next
        second = second.next
    second.next = second.next.next
    return start.next
```

## Merge Two Sorted Lists

https://leetcode.com/problems/merge-two-sorted-lists/

```python
def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
    head = ListNode(0)
    current = head
    while l1 and l2:
        if l1.val < l2.val:
            current.next = l1
            l1 = l1.next
        else:
            current.next = l2
            l2 = l2.next
        current = current.next
    if not l1:
        current.next = l2
    elif not l2:
        current.next = l1
    return head.next
```

## Palindrome Linked List

https://leetcode.com/problems/palindrome-linked-list/

```python
def reverseList(self, head: ListNode) -> ListNode:
    prev = None
    current = head
    while current:
        temp = current.next
        current.next = prev
        prev = current
        current = temp
    return prev


def isEqual(self, first: ListNode, second: ListNode) -> bool:
    while second:
        if second.val != first.val:
            return False
        second = second.next
        first = first.next
    return True


def isPalindrome(self, head: ListNode) -> bool:
    if not head or not head.next:
        return True
    prev = None
    slow = head
    fast = head

    while fast.next and fast.next.next:
        prev = slow
        slow = slow.next
        fast = fast.next.next
    
    secondHalf = slow.next
    if fast.next: # even length
        slow.next = None
        firstHalf = self.reverseList(head)
    else: # odd length
        prev.next = None
        firstHalf = self.reverseList(head)
    return self.isEqual(firstHalf, secondHalf)
```

## Middle of the Linked List

https://leetcode.com/problems/middle-of-the-linked-list/

```python
def middleNode(self, head: ListNode) -> ListNode:
    first = head
    second = head
    while second and second.next:
        first = first.next
        second = second.next.next
    return first
```

## Reverse Linked List

https://leetcode.com/problems/reverse-linked-list/

```python
def reverseList(self, head: ListNode) -> ListNode:
    prev = None
    current = head
    while current:
        temp = current.next
        current.next = prev
        prev = current
        current = temp
    return prev
```
