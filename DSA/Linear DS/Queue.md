# Basic 
A queue is a fundamental data structure that follows the First-In-First-Out (FIFO) principle. In a queue, elements are added at the rear (enqueue) and removed from the front (dequeue). 

![[Pasted image 20240224101425.png]]



### Array 
``` python 
class Queue:
    def __init__(self, capacity):
        self.capacity = capacity
        self.front = self.rear = -1
        self.queue = [None] * capacity

    def is_empty(self):
        return self.front == self.rear == -1

    def is_full(self):
        """
        Check if the queue is full.

        The queue is considered full if the next position after self.rear
        is equal to self.front, or if self.front is at the beginning (0)
        and self.rear is at the end (self.capacity - 1). This condition
        indicates a circular array-based implementation of the queue.

        Returns:
            bool: True if the queue is full, False otherwise.
        """
        if (self.rear + 1 == self.front) or (self.front == 0 and self.rear == self.capacity - 1):
            return True
        else:
            return False

    def enqueue(self, data):
        if self.is_full():
            print("Queue is full. Cannot enqueue.")
        else:
            if self.is_empty():
                self.front = self.rear = 0
            else:
                self.rear = (self.rear + 1) % self.capacity
            self.queue[self.rear] = data

    def dequeue(self):
        if self.is_empty():
            print("Queue is empty. Cannot dequeue.")
            return None
        else:
            data = self.queue[self.front]
            if self.front == self.rear:
                self.front = self.rear = -1
            else:
                self.front = (self.front + 1) % self.capacity
            return data

    def peek(self):
        if self.is_empty():
            print("Queue is empty. Cannot peek.")
            return None
        else:
            return self.queue[self.front]

    def display(self):
        if self.is_empty():
            print("Queue is empty.")
        else:
            current = self.front
            while current != self.rear:
                print(self.queue[current], end=" ")
                current = (current + 1) % self.capacity
            print(self.queue[self.rear])

# Example usage:
queue = Queue(5)
queue.enqueue(1)
queue.enqueue(2)
queue.enqueue(3)

print("Queue elements:")
queue.display()

dequeued_item = queue.dequeue()
print("Dequeued item:", dequeued_item)

print("Queue elements after dequeue:")
queue.display()


```
### List 

```python 
class Queue:
    def __init__(self):
        self.items = []

    def is_empty(self):
        return len(self.items) == 0

    def enqueue(self, data):
        self.items.append(data)

    def dequeue(self):
        if not self.is_empty():
            return self.items.pop(0)
        else:
            return None

    def peek(self):
        if not self.is_empty():
            return self.items[0]
        else:
            return None

    def display(self):
        print(self.items)

# Example usage:
queue = Queue()
queue.enqueue(1)
queue.enqueue(2)
queue.enqueue(3)

print("Queue elements:")
queue.display()

dequeued_item = queue.dequeue()
print("Dequeued item:", dequeued_item)

print("Queue elements after dequeue:")
queue.display()


```
### Linked List

#### Empty Queue 
```python 
class Queue:
    def __init__(self):
        self.front = None
        self.rear = None

    def is_empty(self):
        return self.front is None

# Example usage:
queue = Queue()

if queue.is_empty():
    print("Queue is empty")
else:
    print("Queue is not empty")

```

#### Insert Data in queue 
```python 
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class Queue:
    def __init__(self):
        self.front = None
        self.rear = None

    def enqueue(self, data):
        new_node = Node(data)
        if self.front is None:
            self.front = self.rear = new_node
        else:
            self.rear.next = new_node
            self.rear = new_node

    def display(self):
        current = self.front
        while current:
            print(current.data, end=" ")
            current = current.next
        print()

# Example usage:
queue = Queue()
queue.enqueue(1)
queue.enqueue(2)
queue.enqueue(3)

print("Queue elements:")
queue.display()
# After the insertions, the queue will have elements 1, 2, and 3.
# The display method will print: "1 2 3"


# After the insertions, the queue will have elements 1, 2, and 3.
# Initially:
# front --> None
# rear  --> None

# After enqueue(1):
# front --> Node(1)
# rear  --> Node(1)

# After enqueue(2):
# front --> Node(1)
# rear  --> Node(2)**


```

![[Pasted image 20240224102202.png]]


#### Deletion of Element

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class Queue:
    def __init__(self):
        self.front = None
        self.rear = None

    def is_empty(self):
        return self.front is None

    def enqueue(self, data):
        new_node = Node(data)
        if self.is_empty():
            self.front = self.rear = new_node
        else:
            self.rear.next = new_node
            self.rear = new_node

    def dequeue(self):
        if self.is_empty():
            return None
        data = self.front.data
        self.front = self.front.next
        if self.front is None:
            self.rear = None
        return data

    def display(self):
        current = self.front
        while current:
            print(current.data, end=" ")
            current = current.next
        print()

# Example usage:
queue = Queue()
queue.enqueue(1)
queue.enqueue(2)
queue.enqueue(3)

print("Queue elements before dequeue:")
queue.display()

dequeued_item = queue.dequeue()

print("Dequeued item:", dequeued_item)

print("Queue elements after dequeue:")
queue.display()

```

#### Complete Implementation 

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class Queue:
    def __init__(self):
        self.front = None
        self.rear = None

    def is_empty(self):
        return self.front is None

    def enqueue(self, data):
        new_node = Node(data)
        if self.is_empty():
            self.front = self.rear = new_node
        else:
            self.rear.next = new_node
            self.rear = new_node

    def dequeue(self):
        if self.is_empty():
            return None
        data = self.front.data
        self.front = self.front.next
        if self.front is None:
            self.rear = None
        return data

    def peek(self):
        if self.is_empty():
            return None
        return self.front.data

    def display(self):
        current = self.front
        while current:
            print(current.data, end=" ")
            current = current.next
        print()

# Example usage:
queue = Queue()
queue.enqueue(1)
queue.enqueue(2)
queue.enqueue(3)

print("Queue elements:")
queue.display()

print("Peek:", queue.peek())

dequeued_item = queue.dequeue()
print("Dequeued item:", dequeued_item)

print("Queue elements after dequeue:")
queue.display()

```