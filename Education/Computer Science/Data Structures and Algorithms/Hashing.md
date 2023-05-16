## Definition
A hash function is a function that takes any input and deterministically converts it to an integer that is less than a fixed size set by the programmer. Inputs are called **keys,** and the same input will always be converted to the same integer. 

### Example
Here's an example hash algorithm for a string containing letters of the English alphabet:

1.  Declare an integer `total`.
2.  Iterate over the string. For each character, convert it to its position in the alphabet. For example, `a -> 1`, `c -> 3`, `z -> 26`.
3.  Take that value, and multiply it by the current position in the string (index + 1). For example, given the string `"abc"`, the `b` is at position `2` in the alphabet and position `2` in the string, so we get the final value `2 * 2 = 4`. Add this to `total`.
4.  After going through every character, `total` is the converted value.

This algorithm isn't actually a good hash function (we'll talk about what makes a hash function "good" soon) but is an example of how to convert strings into integers. You may be wondering: don't we need to limit `total` to a fixed size? Correct! Right now, this algorithm is wrong. Let's say the limit we set was `x`. Then change step 4 to:

1.  After going through every character, `total % x` is the converted value.

`%` is the [modulo operation](https://en.wikipedia.org/wiki/Modulo_operation), and makes sure the final converted value will always be less than `x`.

---

### What is the point of a hash function?

We know that [[arrays]] have $O(1)$ random access. The main constraint with arrays is that they are a *fixed size*, and their *indices have to be integers*. Because hash functions can convert any input into an integer, if we combine an array with a hash function, we can create what is known as a **[[hash map]]**, also known as a **[[hash table]]** or **[[dictionary]]**. Then, we can essentially have the $O(1)$ random access of an array without the constraint of integers as indices. With arrays, we **map** indices to values. With hash maps, we map **[[keys]]** to values, and a key can be almost anything. Typically, the only constraint on a hash map's key is that it has to be **immutable** (this is language dependent but generally a good rule of thumb). Values can be anything.

***A hash map is probably the most important concept in all of algorithm interviewing***. It is extremely powerful and allows you to *reduce the time complexity* of an algorithm by a factor of $O(n)$  for a huge amount of problems. Every major language has a [built-in implementation of a hash map](https://en.wikipedia.org/wiki/Hash_table#Implementations). For example, in Python they're called dictionaries and declaring one is as simple as `dic = {}`. If you could only take one thing from this course, it should be to learn and master the hash map operations for the programming language you use.

**To summarize**, a hash map is an unordered data structure that stores key-value pairs. A hash map can add and remove elements in $O(1)$, as well as update values associated with a key and check if a key exists, also in $O(1)$. You can iterate over both the keys and values of a hash map, but a hash map isn't necessarily an ordered data structure (there are many implementations and this is language dependent for the built-in types).

> An ordered data structure is one where the insertion order is "remembered". An unordered data structure is one where the insertion order is not relevant.

### Comparison with arrays

![[hash map]]

![[hash table]]

> Note: remember that time complexity functions only care about the variables you give it. When we say that hash map operations are $O(1)$, the variable we are concerned with is usually n, which is the size of the hash map. However, this may be misleading. For example, hashing a string requires $O(m)$ time, where m is the length of the string. The constant time operations are only "constant" relative to the size of the map.

### Collisions
When different keys convert to the same integer, it is called a collision. Without handling collisions, older keys will get overridden and data will be lost. There are [multiple ways](https://en.wikipedia.org/wiki/Hash_table#Collision_resolution) to handle collisions, but here we'll talk about a common one called **chaining**
##### ![[chaining]]
Collisions are problematic because handling them is necessary, and handling them takes time, slowing down the overall speed and efficiency of the hash map. How can we design our hash map to minimize collisions? The most important thing is that the size of your hash table's array and [modulus is a prime number](https://stackoverflow.com/questions/1145217/why-should-hash-functions-use-a-prime-number-modulus). Prime numbers near significant magnitudes that are common to use are:
-   10,007
-   1,000,003
-   1,000,000,007

### ![[Sets]]
### Arrays as keys
We said that being immutable is usually a requirement for being a hash map key. Arrays are mutable, so how do we store an ordered collection of elements as a key? Depending on the language you're using, there are several ways to convert an array into a unique immutable key. In Python, tuples are immutable, so it's as easy as doing `tuple(arr)`. Another trick is to convert the array into a string, delimited by some character that is guaranteed to not show up in any element. For example, use a comma to separate integers. `[1, 51, 163] --> "1,51,163"`. Some implementations like `map` in the standard library of C++ allows vectors as keys, but the time complexity of operations is not $O(1)$.

![[Checking for existence]]