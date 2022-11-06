# Binary Heap Documentation

## OVERVIEW

A binary heap is a data structure similar to the binary tree but has 2 additional properties. 
- It must be a complete binary tree, meaning that there are no gaps anywhere on the tree. Every row must be completely filled except for possibly the bottom row, but if it is only partially filled, must be filled from left to right. 
- It must either be a min-heap or a max-heap. Min-heap means that for any given node in the tree, all nodes below it are larger. Max-heap means that for any given node in the tree, all nodes below it are smaller. For the rest of this document, it will be referring to a max-heap, but every part would apply the same but just as the smaller values or minimum values instead of larger or maximum ones. 

Binary heaps are important because they are an effective foundation for a priority queue and heap sort. This document will explain the reasons to implement one and how to do so. 

## HOW IS THIS DATA STRUCTURE USEFUL?

Due to binary heaps being complete binary trees, they are easy to represent as an array. There are also useful formulas for finding a parent node's left and right children within the array. Assuming the root node of the binary heap is array index 0 and the index of the other nodes are counted down like this:

![indexTree](https://github.com/Colby626/binaryheap-documentation/blob/main/indexTree.jpg) 

- (i-1)/2 will return i's parent node. 
- (i\*2)+1 will return i's left child
- (i\*2)+2 will return i's right child
This system makes it extremely easy to remove items with the highest priority in a max-heap or lowest priority if it is a min-heap. 

The binary heap is especially efficient when it comes to deleting the maximum in a max-heap or minimum in a min-heap. When compared to a linked list or array, these are the Big-O values for different functions from Carnegie Mellon: 

![OTable](https://github.com/Colby626/binaryheap-documentation/blob/main/OTable.png)

The binary heap may not have the same efficiency for insertion or removal compared to the other options, but it is still really fast at O(log n), but it beat the rest at deleting the maximum. That speed makes it tremendously effective when implementing a priority queue where priority ranks are put in as the value of the nodes. 

## HOW DOES IT WORK?

### Insertion 

When a new number is inserted it is put on the end of the array or the bottom-most / left-most location on the binary tree, it gets compared to its parent to see if it breaks the rules of a binary heap by either being too large or too small. If it does break the rules, it is swapped with its parent. It then rechecks its new parent if it has any, and so on and so forth until it doesn't break the rules anymore. The node that it swaps with will never break the rules in the new location because the ones underneath that one are already smaller or larger than it is. 

This process is shown through these images from Wikipedia where 15 is inserted into a max-heap:

![Wiki1](https://github.com/Colby626/binaryheap-documentation/blob/main/Wiki1.jpg) 

![Wiki2](https://github.com/Colby626/binaryheap-documentation/blob/main/Wiki2.jpg)

![Wiki3](https://github.com/Colby626/binaryheap-documentation/blob/main/Wiki3.jpg)

### Deletion 

Traverse the array to find the index of the element you want to be deleted. Swap that element with the last element in the array and heapify it as discussed in the insertion. Then it can be safely removed. 

### DeleteMax 

The root node is removed and the lowest / rightmost node replaces the root node of the binary heap. Then, it checks its children to see if it is larger than them. If not, it swaps with the larger of the two children and then checks its new children. It does this until the binary heap follows the rules again. The things it is swapping with will never break the rules where they move to because it picks the larger of the two children to swap with, making deleting the maximum value take just as long as insertion. 

These images from Wikipedia show what this would look like in a max-heap where DeleteMax is called:

![Wiki4](https://github.com/Colby626/binaryheap-documentation/blob/main/Wiki4.jpg) 

![Wiki5](https://github.com/Colby626/binaryheap-documentation/blob/main/Wiki5.jpg)

![Wiki6](https://github.com/Colby626/binaryheap-documentation/blob/main/Wiki6.jpg)

### Demonstration

The binary heap is a standard template library or STL for C++. GeekforGeeks demonstrates this code use well in the program below. 

    // C++ program to show that priority_queue is by
    // default a Max Heap
    #include <bits/stdc++.h>
    using namespace std;
    
    // Driver code
    int main ()
    {
        // Creates a max heap
        priority_queue <int> pq;
        pq.push(5);
        pq.push(1);
        pq.push(10);
        pq.push(30);
        pq.push(20);
  
        // One by one extract items from max heap
        while (pq.empty() == false)
        {
            cout << pq.top() << " ";
            pq.pop();
        }
  
        return 0;
    }

#### Output
    30 20 10 5 1

## FURTHER READING

Carnegie Mellon https://www.andrew.cmu.edu/course/15-121/lectures/Binary%20Heaps/heaps.html#:~:text=Since%20a%20heap%20is%20a,to%20implement%20a%20priority%20queue. 

GeeksforGeeks https://www.geeksforgeeks.org/implement-min-heap-using-stl/ 

Research Gate https://www.researchgate.net/figure/Numbering-of-nodes-in-a-fully-populated-binary-tree-with-L-3-levels-The-root-is-the_fig1_317356628 
  
Wikipedia https://en.wikipedia.org/wiki/Binary_heap 
