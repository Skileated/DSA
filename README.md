Data Structures & Algorithms — Reference (Markdown)
# Data Structures & Algorithms — Full Reference

This document provides clear explanations and pseudocode for core data structures and algorithms used in Computer Science.

---

# 1. STACK

A **stack** is a LIFO (Last In, First Out) structure.

### Operations  
- push(x) – insert at top  
- pop() – remove top  
- peek() – view top  
- isEmpty()  
- isFull() (for array-based)

### Pseudocode (Array-based)

```
STACK createStack(maxSize):
s.data ← new array[maxSize]
s.top ← -1
return s

isEmpty(s):
return s.top = -1

isFull(s):
return s.top = maxSize - 1

PUSH(s, value):
if isFull(s): ERROR "Overflow"
s.top ← s.top + 1
s.data[s.top] ← value

POP(s):
if isEmpty(s): ERROR "Underflow"
value ← s.data[s.top]
s.top ← s.top - 1
return value

PEEK(s):
if isEmpty(s): ERROR "Empty"
return s.data[s.top]
```

---

# 2. QUEUE

A **queue** is FIFO (First In, First Out).

---

## 2.1 Simple Linear Queue (Array)

```
QUEUE createQueue(maxSize):
q.data ← new array[maxSize]
q.front ← 0
q.rear ← -1
q.count ← 0
return q

isEmpty(q): return q.count = 0
isFull(q): return q.count = maxSize

ENQUEUE(q, value):
if isFull(q): ERROR
q.rear ← q.rear + 1
q.data[q.rear] ← value
q.count ← q.count + 1

DEQUEUE(q):
if isEmpty(q): ERROR
val ← q.data[q.front]
q.front ← q.front + 1
q.count ← q.count - 1
return val
```

---

## 2.2 Circular Queue (Array)

```
CIRCULAR_QUEUE create(maxSize):
q.data ← array[maxSize]
q.front ← 0
q.rear ← 0
q.count ← 0
q.maxSize ← maxSize

isEmpty(q): return q.count = 0
isFull(q): return q.count = q.maxSize

ENQUEUE(q, value):
if isFull(q): ERROR
q.data[q.rear] ← value
q.rear ← (q.rear + 1) mod q.maxSize
q.count ← q.count + 1

DEQUEUE(q):
if isEmpty(q): ERROR
value ← q.data[q.front]
q.front ← (q.front + 1) mod q.maxSize
q.count ← q.count - 1
return value
```

---

# 3. LINKED LISTS

---

## 3.1 Singly Linked List (SLL)
Node:

```
NODE:
value
next
```

### Common Operations

```
createList():
L.head ← null

insertAtHead(L, value):
node ← new NODE(value)
node.next ← L.head
L.head ← node

insertAtTail(L, value):
node ← new NODE(value)
if L.head = null:
L.head ← node
return
cur ← L.head
while cur.next ≠ null:
cur ← cur.next
cur.next ← node

deleteHead(L):
if L.head = null: ERROR
value ← L.head.value
L.head ← L.head.next
return value
```

---

## 3.2 Doubly Linked List (DLL)

Node:

```
NODE_D:
value
prev
next
```

### Pseudocode

```
createDLL():
L.head ← null
L.tail ← null

insertAtHead(L, value):
node ← new NODE_D
node.value ← value
node.next ← L.head
node.prev ← null
if L.head ≠ null:
L.head.prev ← node
else:
L.tail ← node
L.head ← node

removeNode(L, node):
if node.prev ≠ null:
node.prev.next ← node.next
else:
L.head ← node.next
if node.next ≠ null:
node.next.prev ← node.prev
else:
L.tail ← node.prev
```

---

## 3.3 Circular Linked List (Singly)

```
createCircular():
L.tail ← null

insertAfterTail(L, value):
node ← new NODE(value)
if L.tail = null:
node.next ← node
L.tail ← node
return
node.next ← L.tail.next
L.tail.next ← node
L.tail ← node
```

---

## Applications of Linked Lists  
- Stack using SLL → push/pop at head  
- Queue using SLL → enqueue at tail, dequeue at head  

Both run in **O(1)**.

---

# 4. TREES

---

## 4.1 Binary Tree  
Nodes contain: `value`, `left`, `right`.

---

## 4.2 Binary Search Tree (BST)

### FindMin, FindMax

```
FIND_MIN(n):
while n.left ≠ null: n ← n.left
return n

FIND_MAX(n):
while n.right ≠ null: n ← n.right
return n
```

### Insert

```
INSERT(root, value):
if root = null:
return new Node(value)
if value < root.value:
root.left ← INSERT(root.left, value)
else:
root.right ← INSERT(root.right, value)
return root
```

### Delete

```
DELETE(root, value):
if root = null: return null
if value < root.value:
root.left ← DELETE(root.left, value)
else if value > root.value:
root.right ← DELETE(root.right, value)
else:
if root.left = null: return root.right
if root.right = null: return root.left
succ ← FIND_MIN(root.right)
root.value ← succ.value
root.right ← DELETE(root.right, succ.value)
return root
```

---

# 5. SORTING ALGORITHMS

---

## 5.1 Selection Sort

```
for i = 0 to n-2:
min = i
for j = i+1 to n-1:
if A[j] < A[min]: min = j
swap(A[i], A[min])
```

---

## 5.2 Bubble Sort

```
for i = 0 to n-2:
swapped ← false
for j = 0 to n-2-i:
if A[j] > A[j+1]:
swap(A[j], A[j+1])
swapped ← true
if not swapped: break
```

---

## 5.3 Insertion Sort

```
for i = 1 to n-1:
key = A[i]
j = i-1
while j ≥ 0 and A[j] > key:
A[j+1] = A[j]
j = j-1
A[j+1] = key
```

---

## 5.4 Shell Sort

```
gap = n/2
while gap > 0:
for i = gap to n-1:
temp = A[i]
j = i
while j ≥ gap and A[j-gap] > temp:
A[j] = A[j-gap]
j = j-gap
A[j] = temp
gap = gap/2
```

---

## 5.5 Heap Sort

```
HEAPSORT(A):
buildMaxHeap(A)
for end = n-1 downto 1:
swap(A[0], A[end])
heapSize--
siftDown(A, 0)
```

---

## 5.6 Merge Sort

```
MERGESORT(A, l, r):
if l < r:
m = floor((l+r)/2)
MERGESORT(A, l, m)
MERGESORT(A, m+1, r)
MERGE(A, l, m, r)
```

---

## 5.7 Bucket Sort

```
create k buckets
for each x in A:
put x into bucket[idx(x)]
for bucket in buckets:
sort(bucket)
concatenate
```

---

# 6. SEARCHING

---

## Linear Search

```
for i = 0 to n-1:
if A[i] = key: return i
return -1
```

---

## Binary Search (sorted array)

```
low=0, high=n-1
while low ≤ high:
mid = (low+high)/2
if A[mid] = key: return mid
if key > A[mid]: low = mid+1
else: high = mid-1
return -1
```

---

# 7. HASHING

---

## Hash Functions  
-Modular hashing  
-Multiplicative hashing  

## Open Hashing (Chaining)
Buckets contain linked lists.

## Closed Hashing (Open Addressing)  
-Linear probing  
-Quadratic probing  
-Double hashing  

## Rehashing  
Resize table when load factor exceeds threshold.

---

# 8. GRAPH ADT

---

## Representations  
-Adjacency List  
-Adjacency Matrix  
-Edge List  

---

## BFS

```
BFS(G, src):
mark all unvisited
enqueue(src)
while queue not empty:
u = dequeue()
for every v in Adj[u]:
if unvisited:
mark visited
enqueue(v)
```

---

## DFS

```
DFS(u):
mark u visited
for v in Adj[u]:
if not visited:
DFS(v)
```

---

## Dijkstra’s Algorithm

```
for v in V: dist[v]=∞
dist[src]=0
PQ = priority queue
while PQ not empty:
u = extractMin()
for each (u,v) with weight w:
if dist[u] + w < dist[v]:
dist[v] = dist[u] + w
decreaseKey(v)
```

---

## Minimum Spanning Tree

### Prim’s Algorithm

```
key[v]=∞
key[root]=0
PQ = min-heap
while PQ not empty:
u = extractMin()
for each v in Adj[u]:
if weight(u,v) < key[v]:
key[v] = weight(u,v)
parent[v] = u
```

### Kruskal’s Algorithm

```
sort edges
for each edge (u,v):
if find(u) ≠ find(v):
union(u,v)
add edge to MST
```

---

# 9. ADVANCED PARADIGMS

---

## Greedy — Huffman Coding

```
build min-heap of characters by freq
while heap.size > 1:
x = extractMin()
y = extractMin()
z = new node(x,y)
insert(z)
return root
```

---

## Divide & Conquer — Quick Sort

```
QUICKSORT(A, low, high):
if low < high:
p = partition(A, low, high)
QUICKSORT(A, low, p-1)
QUICKSORT(A, p+1, high)
```

---

## Backtracking — N Queens

```
solve(row):
if row = n: record solution
for col = 0 to n-1:
if safe(row,col):
place queen
solve(row+1)
remove queen
```

---

## Dynamic Programming — Floyd Warshall

```
for k=0..n-1:
for i=0..n-1:
for j=0..n-1:
if dist[i][k] + dist[k][j] < dist[i][j]:
dist[i][j] = dist[i][k] + dist[k][j]
```

---
