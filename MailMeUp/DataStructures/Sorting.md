# Sorting

Sorting is an algorithm that arranges the elements of a list in a certain order [either ascending or descending]. The output is a permutation or reordering of the input.

Sorting is one of the important categories of algorithms in computer science and a lot of research has gone into this category. Sorting can significantly reduce the complexity of a problem, and is often used for database algorithms and searches.

## Bubble Sort

Bubble sort is the simplest sorting algorithm. It works by iterating the input array from the first element to the last, comparing each pair of elements and swapping them if needed. Bubble sort continues its iterations until no more swaps are needed.

The algorithm gets its name from the way smaller elements “`bubble`” to the top of the list. Generally, insertion sort has better performance than bubble sort.

The only significant advantage that bubble sort has over other implementations is that it can detect whether the input list is already sorted or not.

### Implementation

### Performance


| Type                                    | Complexity     |
| ----------------------------------------- | ---------------- |
| Worst case complexity                   | O(n2)          |
| Best case complexity (Improved version) | O(n)           |
| Average case complexity (Basic version) | O(n2)          |
| Worst case space complexity             | O(1) auxiliary |

## Selection Sort

Selection sort is an in-place sorting algorithm. Selection sort works well for small files. It is used for sorting the files with very large values and small keys. This is because selection is made based on keys and swaps are made only when required.

### Advantages
- Easy to implement
- In-place sort (requires no additional storage space)
### Disadvantages
- Doesn’t scale well: O(n2)

### Algorithm
1.  Find the minimum value in the list
2.  Swap it with the value in the current position
3.  Repeat this process for all the elements until the entire array is sorted This algorithm is called selection sort since it repeatedly selects the smallest element.

### Implementation

### Performance

| Type                                    | Complexity     |
| ----------------------------------------- | ---------------- |
| Worst case complexity                   | O(n2)          |
| Best case complexity     | O(n2)
| Average case complexity | O(n2)          |
| Worst case space complexity             | O(1) auxiliary |



## Insertion Sort

Insertion sort is a simple and efficient comparison sort. In this algorithm, each iteration removes an element from the input data and inserts it into the correct position in the list being sorted. The choice of the element being removed from the input is random and this process is repeated until all input elements have gone through.

### Advantages
- Simple implementation
- Efficient for small data
- Adaptive: If the input list is presorted [may not be completely] then insertions sort takes O(n + d), where d is the number of inversions
- Practically more efficient than selection and bubble sorts, even though all of them have O(n2) worst case complexity
- Stable: Maintains relative order of input data if the keys are same
- In-place: It requires only a constant amount O(1) of additional memory space
- Online: Insertion sort can sort the list as it receives it

### Algorithm

Every repetition of insertion sort removes an element from the input data, and inserts it into the correct position in the already-sorted list until no input elements remain. Sorting is typically done in-place. The resulting array after k iterations has the property where the first k + 1 entries are sorted.

<img src="./images/Insertion Sort.png" width="800"  />

Each element greater than x is copied to the right as it is compared against x.

### Implementation

<img src="./images/Insertion Sort Implementation.png" width="1000"  />



### Example
Given an array: 6 8 1 4 5 3 7 2 and the goal is to put them in ascending order.

<img src="./images/Insertion Sort Example.png" width="800"  />

### Analysis


**Worst case analysis**

Worst case occurs when for every i the inner loop has to move all elements A[1], . . . , A[i – 1](which happens when A[i] = key is smaller than all of them), that takes Θ(i – 1) time.

<img src="./images/Insertion Sort Worst case analysis.png" width="400"  />

**Average case analysis**

For the average case, the inner loop will insert A[i] in the middle of A[1], . . . , A[i – 1]. This takes Θ(i/2) time.

<img src="./images/Insertion Sort Average case analysis.png" width="400"  />



### Performance

If every element is greater than or equal to every element to its left, the running time of insertion sort is Θ(n). This situation occurs if the array starts out already sorted, and so an already-sorted array is the best case for insertion sort.


| Type                                    | Complexity     |
| ----------------------------------------- | ---------------- |
| Worst case complexity                   | O(n2)          |
| Best case complexity     | Θ(n)
| Average case complexity | O(n2)          |
| Worst case space complexity             |O(n2) total, O(1) auxiliary |


### Comparisons to Other Sorting Algorithms

Insertion sort is one of the elementary sorting algorithms with O(n2) worst-case time. Insertion sort is used when the data is nearly sorted (due to its adaptiveness) or when the input size is small(due to its low overhead). For these reasons and due to its stability, insertion sort is used as the recursive base case (when the problem size is small) for higher overhead divide-and-conquer sorting algorithms, such as merge sort or quick sort.

**Notes:**
- Bubble sort takes comparisons and swaps (inversions) in both average case and in worst case.
- Selection sort takes comparisons and n swaps.
- Insertion sort takes comparisons and swaps in average case and in the worst case they are double.
- Insertion sort is almost linear for partially sorted input.
- Selection sort is best suits for elements with bigger values and small keys.


## Shell Sort

## Merge Sort

## Heap Sort

## Quicksort

## Tree Sort

## Comparison of Sorting Algorithms

<img src="./images/Comparison of Sorting Algorithms.png" width="1000"  />
