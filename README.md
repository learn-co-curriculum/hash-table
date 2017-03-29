## Introduction

Thus far we have talked about two data structures: arrays and linked lists.  Let's quickly review this.

1. Arrays
Remember that arrays work by storing each element a fixed distance from an initial element.  

```text

|'b' |'c' |'d'| ____|___ |___|
 500  508   516   524  532 540
```

This works well for retrieving information, because by knowing that an array starts at a specific address in memory, it then knows exactly where an element at a specific index lives.  With a sorted array, one can employ binary search to determine if an element is included in the array in big o log(n) time.

More costly is adding or removing an element to the beginning of an array.  To add an element to the beginning means, that each subsequent element must move down one slot, which therefore take big o (n) time.

```text

|'a' |'b' |'c'| 'd' |___ |___|
 500  508  516  524  532 540
```

2. Linked Lists

Linked lists are more costly for retrieval index, as each node can live at any specific address, and one must visit each node to discover where the next node lives.  Because of this, retrieval costs big o (n).  However, adding or removing elements to the beginning of the linked list can be done by only changing the node before and after the inserted node.
is not dependent on the number of elements in the list.  For example, in the diagram below we insert a node holding the string 'c' by changing what the previous node points to and changing what the inserted node points to.

```text

'a'  ->    'b' ->    'd'
500        1024      35
  1024       35


'a' -> 'b' -> 'c' -> 'd'
500   1024    42     35
  1024   42     35
```
> To insert the node, we only had to go change the second node to point to the inserted node, and have the inserted node point to the proper subsequent node.

Let's see this in a chart:

Data Structure | Adding Elements | Retrieving Elements
Arrays             BigO(n)             BigO(1)
Linked List        BigO(1)             BigO(n)             

So arrays are retrieval but not great at manipulation, while linked lists are stronger at manipulation while weaker at retrieval.  Are trees the tool that can perform with both?  But first, what is a tree?

### Trees in the world

Trees are a data structure that connects nodes in a parent - child relationship.  Each parent node would have a pointer and therefore know about its children.  

For example, here is a family tree.

```text
      Grampa (Abe) Simpson
              |      
              V
          Homer Simpson
          |     |      |
          V     V      V
      Bart    Lisa    Maggie
```
> Simpson Family Tree

In the diagram above, Grampa Simpson is a parent of Homer Simpson and Homer Simpson is a parent of Bar, Lisa and Maggie.  Each individual in the Simpson family tree is a node.  The **root node** is the only node in a tree without a parent.  Another example of a tree is an organizational chart.

```text
                                   CEO
       |                            |                                 |
       V                            V                                 V
  Chief Ops Officer        Chief Finance Officer             Chief Marketing Officer
    |             |               |         |                        |        |
    V             V               V         V                        V        V
  VP Human Resources    VP Operations      VP Accounting       VP Sales      VP Advertising  

```

In the above diagram, the CEO has a parent-child relationship with his direct reports, the Chief Operating Officer, the Chief Financial Officer and the Chief Marketing Officer.  Each of the C level people has a parent-child relationship with each one of their direct reports.  

One thing that you may start noticing is that the parent child relationship can become convenient for sorting information.  For example, the tree above represents the organizational hierarchy.  Those on the same level (for example, all of the Vice Presidents) can be thought of as **siblings**.  

> In a tree, siblings are nodes who share a parent node.


### Binary Search Trees

Let's now discuss a specific type of tree.  A binary search tree.  Binary search trees are trees where we organize the nodes such that the nodes adhere to two rules:
  1. No parent can have more than two children (explaining the binary)
  2. Each left child node is less than it's parent node, and each right child is more than the parent node.

Let's place the following numbers in a binary search tree.  4, 1, 2, 5, 6, 3

```text
   T1       T2     T3       T4             T5            T6

   4        4      4         4             4              4
           /      /        /   \         /   \          /   \
          1      1        1     5       1     5        1     5
                   \       \             \     \        \     \
                   2        2            2     6        2     6
                                                         \
                                                          3
```

Above we illustrate the steps involved in inserting each node into a binary search tree.  WE indicate each step at the top, with T1 as the first step, T2 as the second, and so on(T stands for time).  The root node is the first node that we begin with, the number 4.  Then 1 is less than 4, so we place the number to the left.  In T3, we take the number 2.  Two is less than four, so it belongs to the left of four.  Because 1 is already to the left of four, we need to place the 2 one more level down.  Now 2 is greater than 1, so we place it to the right of the node with the number 1.  So if you look at our tree at T3, you can see that the number 2 is to the left of all of the numbers that it is smaller than, the number four.  And it is to the right of all of the numbers that it is larger than, the number 1.  Trace the subsequent steps followed at T4, T5 and T6.  

Note that the same list of numbers results in a different tree, if we insert each node in a different order.

1, 2, 3, 4, 5, 6

1  
  2
    3
      4
        5
          6

So then take these same numbers and get a totally different looking tree.

4, 1, 2, 5, 6, 3
A second example - start at number 4.  So then how does 1 compare to 4.  Is 2 less than one, and then don't go to the left of one, instead go to the right.  

Question - how do you deal with duplicates.
What is the application of this, an org chart with people being equal.  
Then would have to rebalance a tree. So the dom is a tree, and git is a tree, and is just a tree.

Or react it is comparing one tree to the other and making the smallest number of operations.  Hashketball you can think of as a tree.



  So now each node will need three pieces of information
  Has a value, and each one takes it.  Point out that it's a directed graph so the parent knows about children but child does not know about parent.  

  Know that there is nothing
  The definition of a binary search tree, is that everything to the smaller is
  this is a concept rather than a rule - we are using code to model these concepts.

  So then inserting into a binary search tree, so write this method find or add.    

31 - 47 is questions
So you have to start at the root for a bst.

A.   Coding with Trees
    1. find_or_add(4, 3)
      true
    2. find_or_add(4, 7)
      root, element

    So at this point in time, I am doing the same procedure

B. def in_order
In order - it is everything to the left in order followed by root node, followed by everything to the right in order.  So then if I want to place in order, then it is left subtree in order, root ,and then everything to the right in order. So this is recursion all over again.  

def in_order(root_node)
  if root_node.left
    puts node.left
    in_order(root_node.left)
  end
    root_node
  if node.right
    in_order(root_node.right)
  end
end
