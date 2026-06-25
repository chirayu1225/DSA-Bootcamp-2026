# Deque (Double Ended Queue)

[Home](../../README.md) > [Week 4](../README.md) > Deque

> Week 4 · Topic 4 of 5 · Prerequisites: [Queue](../03-Queue/README.md)

---

## Why This Topic Now

You have built stacks (one-end access) and queues (two-end access, but insert at one, remove at the other). A deque generalises both - insert and delete from either end in O(1). This is the data structure behind the sliding window maximum pattern, monotonic queues, and 0–1 BFS. Mastering it here will make those problems straightforward when you encounter them.

---

## What is a Deque?

A **Deque (Double Ended Queue)** is a linear data structure that allows **insertion and deletion from both ends**.

Unlike:

* **Stack →** insert/delete from one end
* **Queue →** insert from rear and delete from front

Deque allows:

```text
Front ← [ Elements ] → Rear
```

Operations at both sides:

```text
insertFront()
insertRear()

deleteFront()
deleteRear()
```

---

## Why Use Deque?

Deque is useful when:

* Need both **stack + queue behavior**
* Sliding Window problems
* Monotonic Queue
* LRU Cache
* 0–1 BFS
* Maintaining min/max of windows

---

## Time Complexity

| Operation   | Complexity |
| ----------- | ---------- |
| insertFront | O(1)       |
| insertRear  | O(1)       |
| deleteFront | O(1)       |
| deleteRear  | O(1)       |
| getFront    | O(1)       |
| getRear     | O(1)       |

---

## STL Deque - C++

```cpp
#include <iostream>
#include <deque>
using namespace std;

int main() {

    deque<int> dq;

    dq.push_back(10);
    dq.push_back(20);
    dq.push_front(5);

    for(int x:dq)
        cout<<x<<" ";

    cout<<"\n";

    dq.pop_front();
    dq.pop_back();

    for(int x:dq)
        cout<<x<<" ";
}
```

Output

```text
5 10 20
10
```

---

## Java Deque

```java
import java.util.*;

public class Main {

    public static void main(String[] args){

        Deque<Integer> dq = new ArrayDeque<>();

        dq.addFirst(10);
        dq.addLast(20);
        dq.addFirst(5);

        System.out.println(dq);

        dq.removeFirst();
        dq.removeLast();

        System.out.println(dq);
    }
}
```

Output

```text
[5,10,20]
[10]
```

---

## Python Deque

```python
from collections import deque

dq = deque()

dq.append(10)
dq.append(20)
dq.appendleft(5)

print(dq)

dq.pop()
dq.popleft()

print(dq)
```

Output

```text
deque([5,10,20])
deque([10])
```

---

## Deque Using Circular Array

## Idea

Normal arrays waste space.

Example:

```text
[10][20][30][ ][ ]

front=0
rear=2
```

After deleting:

```text
[ ][ ][30][ ][ ]

front=2
rear=2
```

Front moved ahead.

If rear reaches end:

```text
[ ][ ][30][40][50]
```

Array appears full even though left side is empty.

Solution:

→ connect ends logically

```text
0 ←→ 1 ←→ 2 ←→ 3 ←→ 4
↑                 ↓
└─────────────────┘
```

This is called **Circular Array**.

---

## Circular Array Working

Insert Rear:

```text
rear=(rear+1)%size
```

Insert Front:

```text
front=(front-1+size)%size
```

Delete Front:

```text
front=(front+1)%size
```

Delete Rear:

```text
rear=(rear-1+size)%size
```

---

## C++ Implementation

```cpp
#include <iostream>
using namespace std;

class Deque {

    int arr[100];

    int front;
    int rear;

    int size;

public:

    Deque(){

        front=-1;
        rear=-1;

        size=100;
    }

    bool isEmpty(){

        return front==-1;
    }

    bool isFull(){

        return (rear+1)%size==front;
    }

    void insertFront(int x){

        if(isFull())
            return;

        if(isEmpty()){

            front=rear=0;
        }

        else{

            front=(front-1+size)%size;
        }

        arr[front]=x;
    }

    void insertRear(int x){

        if(isFull())
            return;

        if(isEmpty()){

            front=rear=0;
        }

        else{

            rear=(rear+1)%size;
        }

        arr[rear]=x;
    }

    void deleteFront(){

        if(isEmpty())
            return;

        if(front==rear){

            front=rear=-1;
        }

        else{

            front=(front+1)%size;
        }
    }

    void deleteRear(){

        if(isEmpty())
            return;

        if(front==rear){

            front=rear=-1;
        }

        else{

            rear=(rear-1+size)%size;
        }
    }

int getFront(){

    if(isEmpty())
        return -1;

    return arr[front];
}

int getRear(){

    if(isEmpty())
        return -1;

    return arr[rear];
}

};
```

---

## Deque Using Doubly Linked List

## Idea

Store:

```text
value
next
prev
```

Since both directions exist:

```text
NULL <- 10 <-> 20 <-> 30 -> NULL
```

Insertions and deletions happen in O(1).

---

## Working

Insert Front

```text
new → oldFront
```

Insert Rear

```text
oldRear → new
```

Delete Front

```text
front=front->next
```

Delete Rear

```text
rear=rear->prev
```

---

## C++ Implementation

```cpp
#include <iostream>
using namespace std;

class Node{

public:

    int data;

    Node* next;

    Node* prev;

    Node(int x){

        data=x;

        next=NULL;

        prev=NULL;
    }
};

class Deque{

    Node* front;

    Node* rear;

public:

    Deque(){

        front=NULL;

        rear=NULL;
    }

    bool isEmpty(){

        return front==NULL;
    }

    void insertFront(int x){

        Node* temp=new Node(x);

        if(isEmpty()){

            front=rear=temp;

            return;
        }

        temp->next=front;

        front->prev=temp;

        front=temp;
    }

    void insertRear(int x){

        Node* temp=new Node(x);

        if(isEmpty()){

            front=rear=temp;

            return;
        }

        rear->next=temp;

        temp->prev=rear;

        rear=temp;
    }

void deleteFront(){

    if(isEmpty())
        return;

    if(front==rear){

        delete front;

        front=rear=NULL;

        return;
    }

    Node* temp=front;

    front=front->next;

    front->prev=NULL;

    delete temp;
}

void deleteRear(){

    if(isEmpty())
        return;

    if(front==rear){

        delete rear;

        front=rear=NULL;

        return;
    }

    Node* temp=rear;

    rear=rear->prev;

    rear->next=NULL;

    delete temp;
}

int getFront(){

    if(isEmpty())
        return -1;

    return front->data;
}

int getRear(){

    if(isEmpty())
        return -1;

    return rear->data;
}
};
```

---

## Array vs Doubly Linked List

| Feature       | Circular Array | Doubly Linked List |
| ------------- | -------------- | ------------------ |
| Insert Front  | O(1)           | O(1)               |
| Insert Rear   | O(1)           | O(1)               |
| Delete Front  | O(1)           | O(1)               |
| Delete Rear   | O(1)           | O(1)               |
| Random Access | O(1)           | O(n)               |
| Memory        | Less           | More               |

---

## Key Takeaways

* Deque = insert/delete from both ends
* Circular Array avoids wasted space
* Doubly Linked List gives dynamic sizing
* Most DSA problems use STL deque
* Monotonic Deque is the most important application

---

## Before You Move On

- Can you implement a deque using a circular array?
- Can you implement a deque using a doubly linked list?
- Do you understand why a deque generalises both a stack and a queue?
- Can you explain the sliding window maximum pattern using a monotonic deque?

---

## Resources

- [Deque Data Structure - GeeksforGeeks](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)
- [Deque in C++ STL - GeeksforGeeks](https://www.geeksforgeeks.org/deque-cpp-stl/)
- [ArrayDeque in Java - GeeksforGeeks](https://www.geeksforgeeks.org/arraydeque-in-java/)

### Video Resources

- [Sliding Window Maximum - Striver (takeUforward)](https://www.youtube.com/watch?v=NwBvene4Imo)
- [Sliding Window Maximum - NeetCode](https://www.youtube.com/watch?v=DfljaUwZsOk)

---

[Previous: Queue](../03-Queue/README.md) | [Week 4 Overview](../README.md) | [Next: Backtracking](../05-Backtracking/README.md)

