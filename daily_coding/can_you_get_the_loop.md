#Codewars #20
##Quesion
Description:

You are given a node that is the beginning of a linked list. This list always contains a tail and a loop.

Your objective is to determine the length of the loop.

For example in the following picture the tail's size is 3 and the loop size is 11.

```
# Use the `next' attribute to get the following node

node.next
```

[link](https://www.codewars.com/kata/can-you-get-the-loop/python)

##@laoris solution

```python
def loop_size(node):
    turtle, rabbit = node.next, node.next.next
    
    # Find a point in the loop.  Any point will do!
    # Since the rabbit moves faster than the turtle
    # and the kata guarantees a loop, the rabbit will
    # eventually catch up with the turtle.
    while turtle != rabbit:
        turtle = turtle.next
        rabbit = rabbit.next.next
  
    # The turtle and rabbit are now on the same node,
    # but we know that node is in a loop.  So now we
    # keep the turtle motionless and move the rabbit
    # until it finds the turtle again, counting the
    # nodes the rabbit visits in the mean time.
    count = 1
    rabbit = rabbit.next
    while turtle != rabbit:
        count += 1
        rabbit = rabbit.next

    # voila
    return count 
```

단순하게 루프크기만 구하면 되는 문제이다. 토끼와 거북이가 같은 점에서 시작하게 하고, 거북이를 고정시키고, 토끼를 거북이와 만날때까지 옮기면 루프크기를 구할 수 있다.

--
좀 더 생각해보자!

이제 리스트가 루프를 인지 아닌지 판단하는 문제로 가면 해법은 다음과 같다.

```python
# Python program to detect loop in the linked list
 
# Node class 
class Node:
 
    # Constructor to initialize the node object
    def __init__(self, data):
        self.data = data
        self.next = None
 
class LinkedList:
 
    # Function to initialize head
    def __init__(self):
        self.head = None
 
    # Function to insert a new node at the beginning
    def push(self, new_data):
        new_node = Node(new_data)
        new_node.next = self.head
        self.head = new_node
 
    # Utility function to prit the linked LinkedList
    def printList(self):
        temp = self.head
        while(temp):
            print temp.data,
            temp = temp.next
 
 
    def detectLoop(self):
        slow_p = self.head
        fast_p = self.head
        while(slow_p and fast_p and fast_p.next):
            slow_p = slow_p.next
            fast_p = fast_p.next.next
            if slow_p == fast_p:
                print "Found Loop"
                return
 
# Driver program for testing
llist = LinkedList()
llist.push(20)
llist.push(4)
llist.push(15)
llist.push(10)
 
# Create a loop for testing
llist.head.next.next.next.next = llist.head
llist.detectLoop()
 
# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

위 문제와 동일한 방법으로 해답을 구하는 것을 알 수 있다. 

[Reference](http://www.geeksforgeeks.org/write-a-c-function-to-detect-loop-in-a-linked-list/)