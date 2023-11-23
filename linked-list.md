# LINKED LIST

## LL: Find Middle Node
**Pseudo Code:**  

1.  Initialize two pointers:  `slow`  and  `fast`, both pointing to the head of the list.
    
2.  While  `fast`  is not null and the next node of  `fast`  is not null:
    
    1.  Move  `slow`  one step ahead (i.e.,  `slow = slow.next`).
        
    2.  Move  `fast`  two steps ahead (i.e.,  `fast = fast.next.next`).
        
3.  When the while loop ends,  `slow`  will point to the middle node of the list. Return  `slow`.
    
This algorithm uses the slow and fast pointer technique, also known as **Floyd's Tortoise and Hare algorithm**, to find the middle element of the linked list.

```
public  Node findMiddleNode()  {
  Node slow = head;
  Node fast = head;

  while  (fast !=  null  && fast.next  !=  null)  {
	  slow = slow.next;
	  fast = fast.next.next;
  }

  return slow;
  }
```

## LL: Has Loop

**Pseudo Code:**  

1.  Initialize two pointers:  `slow`  and  `fast`, both pointing to the head of the list.
    
2.  Start a while loop that continues until both  `fast`  is null and the next node of  `fast`  is null:
    
    1.  Move  `slow`  one step ahead (i.e.,  `slow = slow.next`).
        
    2.  Move  `fast`  two steps ahead (i.e.,  `fast = fast.next.next`).
        
    3.  Check if  `slow`  is equal to  `fast`. If they are equal, it means the list has a loop, so return  `true`.
        
3.  If the while loop ends without finding a loop, return  `false`.

This algorithm uses the slow and fast pointer technique (also known as Floyd's Tortoise and Hare algorithm) to efficiently detect the presence of a loop in the linked list.

```
public boolean hasLoop() {
        if (length == 1) {
            return false;
        }
        
        Node slow = head;
        Node fast = head;
        
        while(fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if(slow == fast) {
                return true;
            }
        }
        
        return false;
    }
```

## Find Kth Node From End

Pseudo Code:

 -  Initialize two pointers: slow and fast, both pointing to the head of the list.
 -  Move fast k steps ahead:
	 - Start a for loop that iterates k times.
	 - Inside the loop, check if fast is null. If it is, the list has fewer than k nodes, so return null.
	 - Move fast one step ahead (i.e., fast = fast.next).
 -  Start a while loop that continues until fast is null:
	 - Move slow one step ahead (i.e., slow = slow.next).
	 - Move fast one step ahead (i.e., fast = fast.next).
 -  When the while loop ends, slow will point to the k-th node from the end of the list. Return slow.
 
This algorithm uses the two-pointer technique to efficiently find the k-th node from the end of the linked list.

  ```
  public Node findKthFromEnd(int k) {
        Node fast = head;
        Node slow = head;
        
        for (int i=0; i<k; i++ ) {
            if(fast == null) {
                return null;
            }
            fast = fast.next;
        }
        
        while(fast != null) {
            slow = slow.next;
            fast = fast.next;
        }
        
        return slow;
    }
```


## LL: Partition Linked List
**Pseudo Code:**  

1.  Check if  `head`  is null. If it is, the list is empty, so simply return.
    
2.  Create two dummy nodes,  `dummy1`  and  `dummy2`, and initialize two pointers,  `prev1`  and  `prev2`, pointing to these dummy nodes respectively.
    
3.  Initialize a pointer  `current`  pointing to the head of the list.
    
4.  Start a while loop that continues until  `current`  is null:
    
    1.  Check if the value of the  `current`  node is less than the given value x. i. If it is, update the next pointer of  `prev1`  to point to  `current`, and update  `prev1`  to point to  `current`.
        
    2.  If it is not, update the next pointer of  `prev2`  to point to  `current`, and update  `prev2`  to point to  `current`.
        
    3.  Move  `current`  one step ahead (i.e.,  `current = current.next`).
        
5.  Set the next pointer of  `prev2`  to null, which terminates the second partition.
    
6.  Set the next pointer of  `prev1`  to the first node of the second partition (i.e.,  `prev1.next = dummy2.next`).
    
7.  Update the head of the list to the first node of the first partition (i.e.,  `head = dummy1.next`).

This algorithm uses two dummy nodes and two pointers to maintain two separate partitions of the original list, one containing nodes with values less than x, and the other containing nodes with values greater than or equal to x. It then concatenates the two partitions and updates the head of the list accordingly.

```
 public void partitionList(int x) {
         if (head == null) return;
         
        Node dummy1 = new Node(0);
        Node dummy2 = new Node(0); 
        Node prev1 = dummy1;
        Node prev2 = dummy2;
        Node current = head;
        
        while(current != null) {
            if(current.value < x) {
                prev1.next = current;
                prev1 = current;
            } else {
                prev2.next = current;
                prev2 = current;
            }
            current = current.next;
        }
        
        prev2.next = null;
        prev1.next = dummy2.next;
        head = dummy1.next;
        
    }
```

## LL: Remove duplicates

**Pseudo Code (for solution that uses a set):**

1.  Create an empty HashSet called  `values`  to store the unique node values encountered in the linked list.
    
2.  Initialize two pointers:  `previous`  set to  `null`, and  `current`  pointing to the head of the list.
    
3.  Start a while loop that continues until  `current`  is null: a. Check if  `values`  contains the value of the  `current`  node. i. If it does, update the next pointer of the  `previous`  node to skip the  `current`  node (i.e.,  `previous.next = current.next`), and decrement the list length by 1. b. If it does not, add the value of the  `current`  node to the  `values`  set and update the  `previous`  pointer to point to the  `current`  node. c. Move  `current`  one step ahead (i.e.,  `current = current.next`).
    
4.  When the while loop ends, all duplicate nodes will have been removed from the list.

This algorithm uses a HashSet to keep track of unique values in the linked list and removes duplicates by updating the next pointers of the nodes as needed.
```
    public void removeDuplicates() {
        
    if (head == null) return;
    
    Node previous = null;
    Node current = head;
    HashSet dupNodeValue = new HashSet();
    
    while(current != null) {
        if (dupNodeValue.contains(current.value)) {
            previous.next = current.next;
            length--;
        } else {
            dupNodeValue.add(current.value);
            previous = current;
        }
        current = current.next;
    }
    
    }
```

## LL: Binary to Decimal

**Objective:**

You have a linked list where each node represents a binary digit (0 or 1). The goal of the  `binaryToDecimal`  function is to convert this binary number, represented by the linked list, into its decimal equivalent.

**How Binary to Decimal Conversion Works:**

In binary-to-decimal conversion, each position of a binary number corresponds to a specific power of 2, starting from the rightmost digit.

-   The rightmost digit is multiplied by 2^0 (which equals 1).
    
-   The next digit to the left is multiplied by 2^1 (which equals 2).
    
-   The digit after that is multiplied by 2^2 (which equals 4). ... and so on.
    

To find the decimal representation:

1.  Multiply each binary digit by its corresponding power of 2 value.
    
2.  Sum up all these products.

**Example Execution with Binary** `101`**:**

1.  Start with  `num = 0`.
    
2.  Process  `1`  (from the head of the linked list):  `num = 0 * 2 + 1 = 1`
    
3.  Process  `0`:  `num = 1 * 2 + 0 = 2`
    
4.  Process  `1`:  `num = 2 * 2 + 1 = 5`
    
5.  Return  `num`, which is  `5`.

```
public int binaryToDecimal() {
        int num = 0;
        Node current = head;
        
        while(current != null) {
            num = num * 2 + current.value;
            current = current.next;
        }
        return num;
    }
```

## LL: Reverse Between

**Pseudo Code:**

1.  Check if the head of the list is null.
    
    -   If the list is empty, there is nothing to reverse. Return immediately (do nothing).
        
2.  Create a  `dummyNode`  with value 0.
    
    -   This node serves as a placeholder to simplify operations involving the list head.
        
3.  Set the  `next`  pointer of  `dummyNode`  to point to the head of the list.
    
4.  Initialize a variable  `previousNode`  and set it to  `dummyNode`.
    
    -   `previousNode`  will track the node right before the segment we want to reverse.
        
5.  Move  `previousNode`  forward  `startIndex`  steps to position it just before the start of the segment to reverse.
    
    -   Use a loop with an index  `i`  going from 0 to  `startIndex`.
        
6.  Set a  `currentNode`  variable to point to the  `next`  node after  `previousNode`.
    
    -   `currentNode`  will be the first node of the segment to be reversed.
        
7.  Now we're ready to reverse the segment.
    
    -   Perform the following steps  `endIndex - startIndex`  times:
        
    -   Set a  `nodeToMove`  variable to point to the  `next`  node after  `currentNode`. This is the node we will "cut" from the segment and "paste" to the front of the segment.
        
    -   Update  `currentNode.next`  to skip over  `nodeToMove`  and point to the node right after  `nodeToMove`.
        
    -   Set the  `next`  pointer of  `nodeToMove`  to point to the node at the front of the segment. This is the node that  `previousNode.next*`  is pointing to.
        
    -   Update  `previousNode.next`  to point to  `nodeToMove`.  `nodeToMove`  has now been moved to the front of the segment.
        
8.  After the loop, the segment between  `startIndex`  and  `endIndex`  is reversed.
    
    -   Update the head of the list to point to the actual first node (not  `dummyNode`).
        
    -   Set  `head`  to point to  `dummyNode.next`.

```
1.  public  void reverseBetween(int startIndex,  int endIndex)  {
2.  if  (head ==  null)  return;

4.  Node dummyNode =  new  Node(0);
5.  dummyNode.next  = head;
6.  Node previousNode = dummyNode;

8.  for  (int i =  0; i < startIndex; i++)  {
9.  previousNode = previousNode.next;
10.  }

12.  Node currentNode = previousNode.next;

14.  for  (int i =  0; i < endIndex - startIndex; i++)  {
15.  Node nodeToMove = currentNode.next;
16.  currentNode.next  = nodeToMove.next;
17.  nodeToMove.next  = previousNode.next;
18.  previousNode.next  = nodeToMove;
19.  }

21.  head = dummyNode.next;
22.  }
```

## Rotate List
Leetcode:
Given the `head` of a linked list, rotate the list to the right by `k` places.

This is not the best solution according to leetCode, But something to start with.

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null || head.next == null) {
            return head;
        }

        for(int i=0; i<k; i++) {
            ListNode previous = head;
            ListNode current = head.next;
            while(current.next != null)
            {
                previous = previous.next;
                current = current.next;
            }

            current.next = head;
            previous.next = null;

            head = current;
        }

        return head;
        
    }
}
```


