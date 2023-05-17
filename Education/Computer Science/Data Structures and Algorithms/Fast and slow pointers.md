Fast and slow pointers is an implementation of the [[two pointers]] technique that we learned in the [[arrays and strings]] chapter. The idea is to have two pointers that don't move side by side. This could mean they move at different "speeds" during iteration, begin iteration from different locations, or any other abstract difference.

When the pointers move at different speeds, usually the "fast" pointer moves two nodes at each iteration, whereas the "slow" pointer moves one node at each iteration (although this is not always the case). Here's some pseudocode:

	// head is the head node of a linked list
	function fn(head):
	    slow = head
	    fast = head

	    while fast and fast.next:
	    Do something here
	    slow = slow.next
	    fast = fast.next.next

>The reason we need the while condition to also check for `fast.next` is because if `fast` is at the final node, then `fast.next` is null, and `fast.next.next` will result in an error.

