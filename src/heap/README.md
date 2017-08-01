# Heap data structure
> Heap is a data structure that can fundamentally change the performance of fairly common algorithms in Computer Science.

> In this lesson we discuss the key operations of the Heap data stucture along with their performance. We then implement the data stucture using TypeScript / JavaScript.

The heap data structure is called a heap because it satisfies the heap property: if P is a parent node of C, then the key (the value) of node P is less than the key of node C.

```
           A
         ↙   ↘
       B       C
     ↙   ↘
    D     E

A < B
A < C
B < D
B < E
```

Even though its nice to have a mental model of a heap as an `Tree`, they are normally implemented as an

We start off by creating a generic class for a Heap for items of type T.
Each data structure has its strenghts. The raison d'etre of the heap data structure is its O(logn) `insert` and `extract` operations.

Lets add a `size` method, it is simply the length of the underlying array.

Another useful method to have is `peek` which instead of removing only looks at the value.

In future lessons we will see a few use cases where this O(logn) insertion and extract can greatly improve efficiency of simple programming challanges. Basically whenever you see an algorithm requiring repeated minimium (or maximum) computations, consisder using a heap.

