In terms of algorithm problems, arrays (1D) and strings are very similar: they both represent an ordered group of elements. Most algorithm problems will include either an array or string as part of the input, so it's important to be comfortable with the basic operations and to learn the most common patterns.

![[Arrays]]

> Technically, *an array can't be resized*. A **dynamic array, or list, can be**. In the context of algorithm problems, usually when people talk about arrays, they are referring to dynamic arrays. In this entire course, we will be talking about dynamic arrays/lists, but we will just use the word "array".

### Strings
**Similarly**, strings are implemented differently between languages. In Python and Java, they are immutable. In C++, they are mutable. It's important to know the details behind arrays and strings for the language you plan on using in interviews. We don't have time to go through all the different implementations for each language, so please research it for your chosen language if you aren't already familiar.

> Mutable: a type of variable that can be changed. Immutable: A type of variable that cannot be changed. If you want to change something immutable, you will need to recreate the entire thing.

Why should we care about something being mutable or immutable? If you have an array `arr = ["a", "b", "c"]` and an immutable string `s = "abc"`, but you want `"abd"`, you can easily do `arr[2] = "d"`, but you cannot do `s[2] = "d"`. As such, if you wanted the string `s = "abd"`, you would need to create it entirely from scratch. With such a small string, it's not a big deal, but sometimes you are dealing with strings with 100,000 characters, so creating new versions just to modify one character is very expensive $O(n)$, where n is the size of the string).

As mentioned before, a majority of algorithm problems will involve an array or string. They are extremely versatile data structures, and it's impossible to list all the relevant problem-solving techniques in one article. In the next few articles, we'll go over the most common techniques. But first, let's take a quick look at the complexity of array and string operations.

![time complexity chart for arrays and strings](https://leetcode.com/explore/interview/card/leetcodes-interview-crash-course-data-structures-and-algorithms/703/arraystrings/Figures/DSA/Chapter_1/1_1.png)  

> Appending to the end of a list is [amortized O(1)](https://stackoverflow.com/questions/33044883/why-is-the-time-complexity-of-pythons-list-append-method-o1).