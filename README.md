# LeetCode 2: Add Two Numbers (Python 3)

An elegant, highly optimized Python 3 solution for the **Add Two Numbers** problem on LeetCode. 

## 📝 Problem Description

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

### Example
* **Input:** `l1 = [2,4,3]`, `l2 = [5,6,4]`
* **Output:** `[7,0,8]`
* **Explanation:** `342 + 465 = 807`.

---

## 💻 Source Code

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        dummy = ListNode(0)
        current = dummy
        carry = 0
        
        # Loop while there are digits left to add or a remaining carry
        while l1 or l2 or carry:
            val1 = l1.val if l1 else 0
            val2 = l2.val if l2 else 0
            
            # Calculate sum and carry
            total = val1 + val2 + carry
            carry = total // 10
            digit = total % 10
            
            # Create new node
            current.next = ListNode(digit)
            current = current.next
            
            # Move pointers forward
            if l1: l1 = l1.next
            if l2: l2 = l2.next
                
        return dummy.next
```

---

## 🔍 Line-by-Line Code Breakdown

### 1. Initialization
* **`dummy = ListNode(0)`**: Creates a placeholder starting node. This avoids writing conditional logic to handle the head node creation separately.
* **`current = dummy`**: A tracking pointer that moves along our new list as we append digits.
* **`carry = 0`**: Tracks the value carried over to the next decimal column when a sum equals or exceeds `10`.

### 2. The Iterative Loop
* **`while l1 or l2 or carry:`**: The loop processes as long as there is an unvisited node in `l1`, an unvisited node in `l2`, or a lingering `carry` value that needs its own final node.

### 3. Pointer Protection & Math
* **`val1 = l1.val if l1 else 0`**: Safely extracts the node value. If one list is shorter than the other and runs out of elements (`None`), it defaults to `0` to prevent crashing.
* **`total = val1 + val2 + carry`**: Computes the sum of the current digits and the previous carry.
* **`carry = total // 10`**: Uses integer division to extract the carry (e.g., `14 // 10 = 1`).
* **`digit = total % 10`**: Uses the modulo operator to get the single digit to store (e.g., `14 % 10 = 4`).

### 4. Linking and Stepping Forward
* **`current.next = ListNode(digit)`**: Spawns a new node with our single digit and links it next.
* **`current = current.next`**: Slides our marker forward onto the node we just made.
* **`if l1: l1 = l1.next`**: Safely advances the input list pointers if they aren't empty.

### 5. Delivering the Result
* **`return dummy.next`**: Bypasses the initial placeholder node (`0`) and returns the clean, head-pointer of the summation list.

---

## ⚡ Complexity Profile

* **Time Complexity:** \(\mathcal{O}(\max(N, M))\) 
  We iterate through the linked lists exactly once, where N and M represent the number of nodes in `l1` and `l2` respectively.
* **Space Complexity:** \(\mathcal{O}(\max(N, M))\) 
  The depth of our memory footprint scales directly with the length of the longest input list (plus at most 1 extra node for a final trailing carry).
