A set is another data structure that is very similar to a [[hash table]]. It uses the same mechanism for hashing keys into integers. The difference between a set and hash table is that sets do not map their keys to anything. *Sets are more convenient to use when you only care about checking if elements exist*. You can add, remove, and check if an element exists in a set all in $O(1)$.

An important thing to note about sets is that ***they don't track frequency***. If you have a set and add the same element 100 times, the first operation adds it and the next 99 do nothing.

