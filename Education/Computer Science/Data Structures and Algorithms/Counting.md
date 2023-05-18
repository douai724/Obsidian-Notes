**Counting is the most common hash map pattern**, and since hash maps are the most common interview concept, counting is arguably the most common interview pattern. By "counting", we are referring to tracking the *frequency* of things. This means our hash map will be mapping keys to integers. Anytime you need to count anything, think about using a hash map to do it.

Recall that when we were looking at [[sliding window]], some problems had their constraint as limiting the amount of a certain element in the window. For example, longest substring with at most `k` `0`s. In those problems, we could simply use an integer variable `count` because we are only focused on one element (we only cared about `0`). A [[hash map]] opens the door to solving problems where the constraint involves multiple elements.
