<table style="width:100%">
  <tr>
    <th><a href="/just-learn-this"> < Home </a></th>
    <th align="right"><a href="/just-learn-this/data_structures/data_structure_menu.html"> Data Structures > </a></th>
  </tr>
</table>

```python


class AbstractQueue:
    def __init__(self):
        self.top = 0

    def isEmpty(self):
        return self.top == 0

    def __len__(self):
        return self.top

    def __str__(self):
        result = '------\n'
        for element in self:
            result += str(element) + '\n'
        return result[:-1] + '\n------'

class ArrayQueue(AbstractQueue):
    def __init__(self, size=10):
        """
        Initialize python List with size of 10 or user given input.
        Python List type is a dynamic array, so we have to restrict its
        dynamic nature to make it work like a static array.
        """
        AbstractQueue.__init__(self)
        self.array = [None] * size
        self.front = 0
        self.rear = 0

    def enqueue(self, value):
        if self.rear == len(self.array):
            self.expand()
        self.array[self.rear] = value
        self.rear += 1
        self.top += 1

    def dequeue(self):
        if self.isEmpty():
            raise IndexError("Queue is empty")
        value = self.array[self.front]
        self.array[self.front] = None
        self.front -= 1
        self.top -= 1
        return value

    def expand(self):
        """
         expands size of the array.
         Time Complexity: O(n)
        """
        new_array = [None] * len(self.array) * 2 # double the size of the array
        for i, element in enumerate(self.array):
            new_array[i] = element
        self.array = new_array

    def __iter__(self):
        probe = self.rear
        while True:
            if probe < 0:
                raise StopIteration
            yield self.array[probe]
            probe -= 1

class QueueNode(object):
    def __init__(self, value):
        self.value = value
        self.next = None

class LinkedListQueue(AbstractQueue):
    def __init__(self):
        AbstractQueue.__init__(self)
        self.front = None
        self.rear = None

    def enqueue(self, value):
        node = QueueNode(value)
        if not self.front:
            self.front = node
            self.rear = node
        node.next = self.rear
        self.rear = node
        self.top += 1

    def dequeue(self):
        if self.isEmpty():
            raise IndexError("Queue is empty")
        value = self.front.value
        if self.front is self.rear:
            self.front = None
        self.front = self.front.next
        self.top -= 1
        return value

    def __iter__(self):
        probe = self.rear
        while True:
            if probe is None:
                raise StopIteration
            yield probe.value
            probe = probe.next

class HeapPriorityQueue(AbstractQueue):
    def __init__(self):
        pass

# Queue Abstract Data Type (ADT)
# * Queue() creates a new queue that is empty.
#   It needs no parameters and returns an empty queue.
# * enqueue(item) adds a new item to the rear of the queue.
#   It needs the item and returns nothing.
# * dequeue() removes the front item from the queue.
#   It needs no parameters and returns the item. The queue is modified.
# * isEmpty() tests to see whether the queue is empty.
#   It needs no parameters and returns a boolean value.
# * size() returns the number of items in the queue.
#   It needs no parameters and returns an integer.

```