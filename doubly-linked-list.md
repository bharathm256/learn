# DOUBLY LINKED LIST : DDL



## DLL: Swap First and Last
**Pseudo Code:**  

1.  Check if the length of the doubly linked list is less than 2. If it is, return, as there are no nodes to swap.
    
2.  If the length is 2 or more, proceed with swapping the values of the first and last nodes:
    
    1.  Store the value of the  `head`  node in a temporary variable,  `temp`.
        
    2.  Set the value of the  `head`  node to the value of the  `tail`  node.
        
    3.  Set the value of the  `tail`  node to the value stored in  `temp`.
        

This algorithm simply swaps the values of the first and last nodes of the doubly linked list. It does not involve updating any pointers or modifying the structure of the list.

```java
public void swapFirstLast() {
        if (length < 2) {
            return;
        }
        
        int temp = tail.value;
        tail.value = head.value;
        head.value = temp;
        
    }
```

## DLL: Reverse

**Pseudo Code:**

1.  Initialize variables:
    
    1.  Set currentNode to head.
        
    2.  Set temporaryNode to null.
        
2.  Iterate through the list:
    
    1.  While currentNode is not null, do the following:
        
        1.  Set temporaryNode to currentNode.prev.
            
        2.  Set currentNode.prev to currentNode.next.
            
        3.  Set currentNode.next to temporaryNode.
            
        4.  Set currentNode to currentNode.prev.
            
3.  Swap head and tail:
    
    1.  Set temporaryNode to head.
        
    2.  Set head to tail.
        
    3.  Set tail to temporaryNode.

```java
public void reverse() {
        if (length <=1) {
            return;
        }
        
    Node current = head;
    Node temp = null;
    
    while (current != null) {
        temp = current.prev;
        current.prev = current.next;
        current.next = temp;
        current = current.prev;
    }
    
    temp = head;
    head = tail;
    tail = temp;
        
    }
```

## DLL: Swap Nodes in Pairs

**Pseudo Code:**  

1.  Initialize variables:
    
    -   Create a  `dummyNode`  with value 0.
        
    -   Set  `dummyNode.next`  to  `head`.
        
    -   Set  `previousNode`  to  `dummyNode`.
        
2.  Iterate through the list:
    
    -   While  `head`  is not null and  `head.next`  is not null, execute the following sub-steps.
        
3.  Identify nodes to swap:
    
    -   Set  `firstNode`  to  `head`.
        
    -   Set  `secondNode`  to  `head.next`.
        
4.  Update pointers to swap nodes:
    
    -   Set  `previousNode.next`  to  `secondNode`.
        
    -   Set  `firstNode.next`  to  `secondNode.next`.
        
    -   Set  `secondNode.next`  to  `firstNode`.
        
5.  Update previous pointers:
    
    -   Set  `secondNode.prev`  to  `previousNode`.
        
    -   Set  `firstNode.prev`  to  `secondNode`.
        
    -   If  `firstNode.next`  is not null, set  `firstNode.next.prev`  to  `firstNode`.
        
6.  Move pointers for the next iteration and update list head:
    
    -   Set  `head`  to  `firstNode.next`.
        
    -   Set  `previousNode`  to  `firstNode`.
        
    -   Eventually, set  `head`  to  `dummyNode.next

```java
 public void swapPairs() {
        Node dummyNode = new Node(0);
        dummyNode.next = head;
        Node previousNode = dummyNode;
        
        while (head != null && head.next != null) {
            Node firstNode = head;
            Node secondNode = head.next;
            
            previousNode.next = secondNode;
            firstNode.next = secondNode.next;
            secondNode.next = firstNode;
            
            secondNode.prev = previousNode;
            firstNode.prev = secondNode;
            
            if (firstNode.next != null) {
                firstNode.next.prev = firstNode;
            }
    
            head = firstNode.next;
            previousNode = firstNode;
        }
    
        head = dummyNode.next;
        if (head != null) head.prev = null;
        
    }
```
