2023-06-10
### Stack
#### Array-based Stack
```
// t points to the top of the stack
Algorithm size():
	return t + 1

Algorithm pop():
	if isEmpty() then
		throw EmptyStackException
	else 
	 t <- t -1 
	 return S[t + 1]

Algorithm push(o):
	if t = S.length - 1 then
		signal stack overflow error
	else
		t <- t + 1
		S[t] <- o
```

###### Using the stack, describe an algorithm which reads a word and then writes it backwards.

```
S = new Stack()
while not the end of the stack:
	S.push(letter)
while not S.isEmpty():
	print(S.pop())

// if n is size of the word, O(n)
```

###### Describe how you can define a new Stack ADT method that returns the second item from the top of the stack without permanently changing the stack. What is the time complexity of this new method with respect to the size of the stack?

```
if (S.size >= 2):
	i = S.pop()
	j = S.top()
	S.push(i)

 // Time complexity: O(1)
```

### Queue

```
Algorithm size():
	return sz

Algorithm isEmpty():
	return (sz == 0)

Algorithm enqueue(o):
	if size() = N -1 then
	 signal queue full error
	else
		r <- (f + sz) mod N
		Q[r] <- o
		sz <- (sz + 1)
// r is rear of the Queue, f is the front, sz is stack size, N is array size

Algorithm dequeue():
	if isEmpty() then
		return null
	else o <- Q[f]
		f <- (f + 1) mod N
		sz <- (sz - 1)
		return o
```

*Note: Growable Array-based Queue and Stack:*
- O(n) with incremental strategy
- O(1) with doubling strategy

###### Assume we are implementing a queue as a circular array with length 5. What would the queue look like if we enqueue A, B, and C,then dequeue twice, then enqueue D, E, and F?

Enqueue A, B, C:

`r -> (f + sz) mod N`

| 0 | 1  | 2 | 3 | 4 |
|---|---|---|---|---|
| A | B | C |   |   |
| f |   | r |   |   |

Dequeue twice:

`f -> (f + 1) mod N`
`f -> 0 + 1 mod 5`
`f -> 1`

| 0 | 1  | 2 | 3 | 4 |
|---|---|---|---|---|
|   |   | C |   |   |
| f |   | r |   |   |

`Size = N - 1 = 4`

Add G:

| 0 | 1  | 2 | 3 | 4 |
|---|---|---|---|---|
| F |   | C | D | E |
| r |   | f |   |   |

Double it:

| 0 | 1  | 2 | 3 | 4 | 5 | 6  | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
| C | D  | E | F | G |  |   |  |  |  |
| f |    |   |   | r |  |   |  |  |  |

Copy Queue to Queue
###### Let S be original Q, create new queue S' with double size.
```
while !S.isEmpty():
	S'.enqueue(S.dequeue())
```

###### Describe in pseudo-code a linear-time algorithm for reversing a queue Q

```
S = new Stack()
while Q is not empty:
	S.push(Q.dequeue())
while S is not empyt:
	Q.enqueue(S.pop())
```

### Array-based lists

```
Algorithm add(r,e):
	if n = N then:
		return "Array is full"
	if r < n then:
		for i <- n - 1, n -2, ... ,r do:
			A[i+1] <- A[i] // make room for new element (shifting right)
		A[r] <- e
		n <- n + 1
Algorithm remove(r):
	e <- A[r] // e is a temporary variable
	if r < n - 1 then
		for i <- r, r+1, ... ,n-2 do
			A[i] <- A[i+1] // fill in removed element (shift left)
```

### Linked List
#### Singly Linked-list

Insertion Algorithm
```
Algorithm InsertAfter(p, e):
	Create new node v
	v.data <- e
	v.pre <- p //link v to predessor
	v.next <- p.next
	(p.next).prev <- v
	p.next <- v
	return v

Algorithm remove(p): 
	t <- p.element //a temporary variable to hold the return value
	(p.prev).next <- p.nxt
	(p.next).prev <- p.prev
	p.prev <- null
	p.next <- null
	return t 
```

### Trees

```
Algorithm inOrder(v):
	if isInternal(v):
		inOrder(leftChild(v))
	visit(v)
	if isInternal(v)
		inOrder(rightChild(v))

Algorithm printExpression(v):
	if isInternal(v)
		print("(")
		inOrder(leftChild(v))
	print(v.elemnt())
	if isInternal(v):
		inOrder(rightChild(v))
		print(")")

```
###### Let T be a tree with n nodes. Define the lowest common ancestor (LCA) between two nodes v and w as the lowest node in T that has both v and w as descendents. Given two nodes v and w, describe an efficient algorithm for finding the LCA of v and w. What is the running time of your method?
```
Algorithm LCA(T,W,V):
    lca = new Node()
	sv = new Stack()
	sw = new Stack()
	temp1 = new Node()
	temp2 = new Node()
	while(temp1 != null):
		sv.push(temp1)
		temp1 = T.parent(temp1)
	while(temp2 != null):
		sv.push(temp2)
		temp2 = T.parent(temp2)
	while(!sv.isEmpty && sv.peak() == sw.peak()):
		lca = sv.pop()
		sw.pop()
	return lca
```
###### Let T be a tree with n nodes, and for any node v in T, let dv denote the depth of v in T. Describe an algorithm for finding the distance between v and w.
```
Algorithm distance(T,W,V):
	sv = new Stack()
	sw = new Stack()
	temp1 = new Node()
	temp2 = new Node()
	while(temp1 != null):
		sv.push(temp1)
		temp1 = T.parent(temp1)
	while(temp2 != null):
		sv.push(temp2)
		temp2 = T.parent(temp2)
	while(!sv.isEmpty && sv.peak() == sw.peak()):
		sv.pop()
		sw.pop()
	return (sv.size() + sw.size())
```

