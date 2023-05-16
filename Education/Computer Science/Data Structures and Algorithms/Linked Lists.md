Let's start by introducing the concept of a **node**.
### ![[Node]]
[[Arrays]] are implemented under the hood in a way that the elements are stored contiguously in memory. Let's say you declared an array to hold 32-bit integers. Each element in the array is at an address that is 4 bytes (32 bits) away from its neighbours. This allows the programmer to access elements in an array with indexing (like `arr[6]` etc.).

A linked list is a data structure that is similar to an [[arrays]]. It also stores data in an ordered manner, but it is implemented using node objects (you will have a custom class). Each node will have a "next" [[pointer]], which points to the node representing the next element in the sequence.

### Advantages and disadvantages compared to arrays
To be honest, the advantages and disadvantages are not super relevant in terms of algorithm problems. This is because almost all the problems that involve linked lists will have the linked list as part of the input, so there isn't a decision on if you should use a linked list. However, there are a few problems that use a linked list as part of the optimal algorithm, and you may be asked trivia in an interview, so it's still good to know the advantages and disadvantages.

*The main advantage of a linked list is that you can add and remove elements at any position in $O(1)$.* The caveat is that you need to have a reference to a node at the position in which you want to perform the addition/removal, otherwise the operation is $O(n)$, because you will need to iterate starting from the `head` until you get to the desired position. However, this is still much better than a normal (dynamic) array, which requires $O(n)$ for adding and removing from an _arbitrary_ position.

*The main disadvantage of a linked list is that there is no random access.* If you have a large linked list and want to access the 150,000th element, then there usually isn't a better way than to start at the head and iterate 150,000 times. So while an array has $O(1)$ indexing, a linked list has $O(n)$.

A few other notes that are less relevant for algorithm problems but may come up in an interview discussion - linked lists have the advantage of not having fixed sizes. While dynamic arrays can be resized, under the hood they still are allocated a fixed size - it's just that when this size is exceeded, the array is resized, which is expensive. Linked lists don't suffer from this. However, linked lists have more overhead than arrays - every element needs to have extra storage for the pointers. If you are only storing small items like booleans or characters, then you may be more than doubling the space needed.

### **Singly linked list**

This is the most common type of linked list and the one that is given in the code above. In a singly linked list, each node only has a pointer to the **next** node. This means you can only move forward in the list when iterating. The pointer used to reference the next node is usually called `next`.

Let's say you want to add an element to a linked list so that it becomes the element at position `i`. To do this, you need to have a pointer to the element currently at position `i - 1`. The next element (currently at position `i`), call it `x`, will be pushed to the element at position `i + 1` after the insertion. This means that `x` should become the `next` node to the one being added, and the node being added should become the `next` node to the one currently at `i - 1`.

	class ListNode {
	    int val;
	    ListNode next;
	    ListNode (int val) {
	        this.val = val;
	    }
	}

	// Let prevNode be the node at position i - 1
	void addNode(ListNode prevNode, ListNode nodeToAdd) {
	    nodeToAdd.next = prevNode.next;
	    prevNode.next = nodeToAdd;
	}

> Note: it is unusual that you will have a pointer to the node at the position before where you want to perform an operation, but we are writing these functions as a demonstration. In most cases, you will need to iterate from the `head` until you are at the desired position, which means the operation is typically �(�)O(n).

Let's say you want to delete the element at position `i`. Again, you need to have a pointer to the element currently at position `i - 1`. The element at position `i + 1`, call it `x`, will be shifted over to be at position `i` after the deletion. Therefore, you should set `x` as the `next` node to the element currently at position `i - 1`. Here's some code and images demonstrating:

	class ListNode {
	    int val;
	    ListNode next;
	    ListNode (int val) {
	        this.val = val;
	    }
	}

	// Let prevNode be the node at position i - 1
	void deleteNode(ListNode prevNode) {
	    prevNode.next = prevNode.next.next;
	}

As mentioned before, when you have a reference to the node at `i - 1`, then insertion and deletion is $O(1)$. However, without that reference, you need to obtain the reference by iterating from the head, which for an **arbitrary** position is $O(n)$.

### **Doubly linked list**
A doubly linked list is like a singly linked list, but each node also contains a pointer to the previous node. This pointer is usually called `prev`, and it allows iteration in both directions.

In a singly linked list, we needed a reference to the node at `i - 1` if we wanted to add or remove at `i`. This is because we needed to perform operations on the `prevNode`. With a doubly linked list, we only need a reference to the node at `i`. This is because we can simply reference the `prev` pointer of that node to get the node at `i - 1`, and then do the exact same operations as above.

With a doubly linked list, we need to do extra work to make sure the `prev` pointers are correct.

	class ListNode {
	    int val;
	    ListNode next;
	    ListNode prev;
	    ListNode (int val) {
	        this.val = val;
	    }
	}

	void addNode(ListNode node, ListNode nodeToAdd) {
	    ListNode prevNode = node.prev;
	    nodeToAdd.next = node;
	    nodeToAdd.prev = prevNode;
	    prevNode.next = nodeToAdd;
	    node.prev = nodeToAdd;
	}

	void deleteNode(ListNode node) {
	    ListNode prevNode = node.prev;
	    ListNode nextNode = node.next;
	    prevNode.next = nextNode;
	    nextNode.prev = prevNode;
	}

### **Linked lists with sentinel nodes**

> We call the start of a linked list the `head` and the end of a linked list the `tail`.

Sentinel nodes sit at the start and end of linked lists and are used to make operations and the code needed to execute those operations cleaner. The idea is that, even when there are no nodes in a linked list, you still keep pointers to a `head` and `tail`. The real head of the linked list is `head.next` and the real tail is `tail.prev`. The sentinel nodes themselves are not part of our linked list.

> The previous code we looked at is prone to errors. For example, if we are trying to delete the last node in list, then `nextNode` will be `null`, and trying to access `nextNode.next` would result in an error. With sentinel nodes, we don't need to worry about this scenario because the last node's `next` points to the sentinel tail.

The sentinel nodes also allow us to easily add and remove from the front or back of the linked list. Recall that addition and removal is only $O(1)$ if we have a reference to the node at the position we are performing the operation on. With the sentinel tail node, we can perform operations at the end of the list in $O(1)$.

	class ListNode {
	    int val;
	    ListNode next;
	    ListNode prev;
	    ListNode (int val) {
	        this.val = val;
	    }
	}

	void addToEnd(ListNode nodeToAdd) {
	    nodeToAdd.next = tail;
	    nodeToAdd.prev = tail.prev;
	    tail.prev.next = nodeToAdd;
	    tail.prev = nodeToAdd;
	}

	void removeFromEnd() {
	    if (head.next == tail) {
	        return;
	    }

	    ListNode nodeToRemove = tail.prev;
	    nodeToRemove.prev.next = tail;
	    tail.prev = nodeToRemove.prev;
	}

	void addToStart(ListNode nodeToAdd) {
	    nodeToAdd.prev = head;
	    nodeToAdd.next = head.next;
	    head.next.prev = nodeToAdd;
	    head.next = nodeToAdd;
	}

	void removeFromStart() {
	    if (head.next == tail) {
	        return;
		}

	    ListNode nodeToRemove = head.next;
	    nodeToRemove.next.prev = head;
	    head.next = nodeToRemove.next;
	}

	ListNode head = new ListNode(-1);
	ListNode tail = new ListNode(-1);
	head.next = tail;
	tail.prev = head;

### **Dummy pointers**
As mentioned earlier, we usually want to keep a reference to the `head` to ensure we can always access any element. Sometimes, it's better to traverse using a "dummy" pointer and to keep `head` at the head.

	int getSum(ListNode head) {
	    int ans = 0;
	    ListNode dummy = head;
	    while (dummy != null) {
	        ans += dummy.val;
	        dummy = dummy.next;
	    }

	    // same as before, but we still have a pointer at the head
	    return ans;
	}

Using the `dummy` pointer allows us to traverse the linked list without losing a reference to the `head`.

>When it comes to linked list problems, many solutions are difficult to reach because of their elegance. In many cases, you could simply iterate through the linked list and put all the elements in an array, then just solve the problem using the array. However, the point of these problems is usually to manipulate pointers in a clean way using $O(1)$ space.

### ![[Fast and slow pointers]]




