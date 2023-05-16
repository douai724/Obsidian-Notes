In terms of time complexity, hash maps blow arrays out of the water. The following operations are all $O(1)$ for a hash map:

-   Add an element and associate it with a value
-   Delete an element if it exists
-   Check if an element exists

A hash map also has many of the same useful properties as an array with the same time complexity:

-   Find length/number of elements
-   Updating values
-   Iterate over elements

> Hash maps are also just easier/cleaner to work with. Even if your keys are integers and you could get away with using an array, if you don't know what the max size of your key is, then you don't know how large you should size your array. With hash maps, you don't need to worry about that, since your key can be anything.

However, from a practical perspective, there are some disadvantages to using hash maps, and it's important to know them as it is common in interviews to talk about tradeoffs.

**The biggest disadvantage of hash maps is that for smaller input sizes, they can be slower because of overhead.** Because big O ignores constants, the $O(1)$ time complexity can sometimes be deceiving - it's usually something more like $O(10)$ because every key needs to go through the hash function, and there can also be **collisions**, which we will talk about in the next section.

> When talking about the time complexity of hash map operations, they are constant relative to the size of the hash map. However, some keys can be very expensive to hash. For example, it may take �(�)O(m) time to hash a string, where m is the length of the string. If you want to store a **huge** string as a key, then the time complexity can be deceiving.