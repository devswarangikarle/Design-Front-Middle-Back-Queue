# Design-Front-Middle-Back-Queue

Design a queue that supports push and pop operations in the front, middle, and back.
Implement the FrontMiddleBack class:

FrontMiddleBack() Initializes the queue.
void pushFront(int val) Adds val to the front of the queue.
void pushMiddle(int val) Adds val to the middle of the queue.
void pushBack(int val) Adds val to the back of the queue.
int popFront() Removes the front element of the queue and returns it. If the queue is empty, return -1.
int popMiddle() Removes the middle element of the queue and returns it. If the queue is empty, return -1.
int popBack() Removes the back element of the queue and returns it. If the queue is empty, return -1.
Notice that when there are two middle position choices, the operation is performed on the frontmost middle position choice. For example:

Pushing 6 into the middle of [1, 2, 3, 4, 5] results in [1, 2, 6, 3, 4, 5].
Popping the middle from [1, 2, 3, 4, 5, 6] returns 3 and results in [1, 2, 4, 5, 6].

class FrontMiddleBackQueue:
    def __init__(self):
        self.queue = deque()
        self.queue2 = deque()
    def pushFront(self, val: int) -> None:
        self.queue.appendleft(val)
    def pushMiddle(self, val: int) -> None:
        if len(self.queue)%2==0:
            for i in range(len(self.queue)//2):
                self.queue2.append(self.queue.pop())
            self.queue.append(val)
            for i in range(len(self.queue2)):
                self.queue.append(self.queue2.pop())
        else:
            for i in range((len(self.queue)//2)+1):
                self.queue2.append(self.queue.pop())
            self.queue.append(val)
            for i in range(len(self.queue2)):
                self.queue.append(self.queue2.pop())


    def pushBack(self, val: int) -> None:
        self.queue.append(val)
    def popFront(self) -> int:
        if len(self.queue)!=0:
            return self.queue.popleft()
        else:
            return -1
    
    def popMiddle(self) -> int:
        a = len(self.queue)
        if a==0:
            return -1
        if a%2==0:
            ans = self.queue[(a//2)-1]
            for i in range(a//2):
                self.queue2.append(self.queue.pop())
            self.queue.pop()
            for i in range(len(self.queue2)):
                self.queue.append(self.queue2.pop())
            return ans

        else:
            ans = self.queue[(a//2)]
            for i in range(a//2):
                self.queue2.append(self.queue.pop())
            self.queue.pop()
            for i in range(len(self.queue2)):
                self.queue.append(self.queue2.pop())
            return ans


    def popBack(self) -> int:
        if len(self.queue) != 0:
            return self.queue.pop()
        else:
            return -1
