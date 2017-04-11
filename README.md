## Hash Table

### Objectives 
* Learn the benefits of using a hash table over arrays and linked lists.
* Learn the components of a hash table.
* Learn about collisions and how to resolve them.
* Learn about the attributes of a good hash function. 

### Review

Previously we have talked about arrays and linked lists.   	

##### Arrays 

Remember that with arrays we store elements contiguously in memory.  This means that each element is evenly spaced in memory from the next one.   Because of this, when we initialize a new array also must allocate a fixed amount of space in memory to store the array, and when the array runs out of space, we need to copy over the elements into a different spot.  

However, the benefit of using an array is that because each element is in a predictable location, we can determine where to access an element at a specific index in the array and therefore can retrieve elements in constant time.
	
##### Linked Lists 

Elements in a linked list are not contiguous in memory - instead we can store an element anywhere in memory, with each element having a pointer that tells us the location of the next element.  The benefit of this is that we can our linked lists can continue to grow in size and we will not run out of space.  But the price paid for dynamic size is that to access an element, we need to follow the pointers from node to node, which makes the time to retrieve an element is O(n).

##### The Goal

Our goal is to have a mechanism that allows to predict precisely where a piece of data is (like we can with an array), while still allowing our data structure to grow (like we can with a hash).

### Hash Tables

A hash table is an array where we place the element in a specific location based on data from that element and a function.  So we use the **hash function** to determine where exactly to store a given key.  Later, use the same hash function to determine where to search for a given key.

Let's try this with an example.  Imagine we would like to use our hash table to store a collection of books.  We'll determine at which index to place the book by using the first number of each section of the Dewey Decimal System, which we conveniently have below.

![](https://s3-us-west-2.amazonaws.com/curriculum-content/algorithms/dewey-decimal-arrangement.jpg)

We have the following books: *The Bible*, *Alexander Hamilton*, *Introduction to Physics*, and *War and Peace*.  Based on our hash function, we store the books in the following locations:

| Index        |Book           |
| ------------- |:-------------:|
| 000 |  |
| 100 |  |
| 200 | *The Bible*|
| 300 | |
| 400 | |
| 500 | *Introduction to Physics*|
| 600 | |
| 700 | |
| 800 | *War and Peace* |
| 900 | *Alexander Hamilton*|

So now when we need to retrieve a book, we do not need to look through every index to find our books, instead we just look at the place of the book based on the Dewey Decimal System. 

![](http://i2.cdn.cnn.com/cnnnext/dam/assets/131126190621-geroge-peabody-library-horizontal-large-gallery.jpg)
> A massive library

So we use our formula to tell us both where to insert a book, and also where to look to retrieve a book.  If someone asks us if *Eloquent Javascript* is in our hash table, we simply visit our index at location 600, see that nothing is there, and can confidently reply that the book is not located there.  Note that the indices are not necessarily contiguous, as they are in an array, but because our formula tells us exactly where to place a book, and also where to retrieve a book we are able to retrieve and insert an element in constant time.

So with a hash table, we look at the data in our element, run it through our hash function to determine where to place the element, and because the hash function does not rely on our elements being evenly spaced apart, we do not need to allocate a contiguous chunk of memory for our hash table.  So we achieve our goal of constant time for inserting and retrieving elements while having a data structure that can grow. 

 
#### The Problem: Collision

Our hash table currently looks like the following: 

| Index        |Book           |
| ------------- |:-------------:|
| 000 |  |
| 100 |  |
| 200 | *The Bible*|
| 300 | |
| 400 | |
| 500 | *Introduction to Physics*|
| 600 | |
| 700 | |
| 800 | *War and Peace* |
| 900 | *Alexander Hamilton*|

Now what happens if we need to store another book, this time *Introduction to Biology*.  Well, our Dewey Decimal System tells us to store the key at the location with index 500.  The only problem is that the slot is already filled.  We have just encountered a **collision**.  A collision is where our hash function outputs a value that already is occupied in our hash table.  

To handle our collision we apply separate chaining.  With separate chaining, each index points to a linked list.  So in our example above we could place both *Introduction to Physics* and *Introduction to Biology* in the place linked list is located at index 500.  Applying the separate chaining technique, our hash table will look like the following:  

| Index        |Book           |
| ------------- |:-------------:|
| 000 |  |
| 100 |  |
| 200 | [ "*The Bible*" ]|
| 300 | |
| 400 | |
| 500 | [ "*Introduction to Physics*", "*Introduction to Biology*" ]|
| 600 | |
| 700 | |
| 800 | [ "*War and Peace*" ]|
| 900 | [ "*Alexander Hamilton*" ]|

Note that in the worse case scenario, all of our inserted elements collide and we have to traverse a linked list of length n to retrieve an element, so we have O(n).  However, on average collisions do not occur, so we retrieve constant time for lookup, insertion and deletion *on average*.  

### Choosing a good hash function

So choose a hash function that minimizes the chance of a collision occurring.  Some properties of a good hash function. 

1. Makes use of all information provided by a given key to maximize the number of possible hash values.  So books of two different titles should map to two different values. 
2. Our hash function should produce a hash value that is distributed evenly across the table, which avoids long linked lists at certain keys.
3. Maps similar keys to very different values - making collisions much less likely.
4. Also hash function called frequently so should employ simple and quick introductions.  

### Summary

In this function we learned about hash tables.  Hash tables place the value of an element into a hash function which outputs a hash value.  The hash value determines where to place the element.  Because a hash function produces the same hash value for a given element, it also gives us fast lookup time to retrieve an element.  

When a hash function ouputs the same hash value for two different elements we have a collision.  We can resolve a collision by employing separate chaining where each hash value points to a linked list, and when there is a collision we attach the element to the linked list.  

Because retrieving elements from a linked list is O(n), we try to choose a hash function that avoids collisions.  Because we must use our hash function to insert, delete, and retrieve elements we also choose a fast hash function.



	
 


