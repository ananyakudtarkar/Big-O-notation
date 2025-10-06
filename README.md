# Algorithm Analysis using Big O Notation

## Overview

This repository provides a comprehensive guide to understanding and analyzing algorithms using **Big O notation**. Big O notation is a mathematical notation that describes the limiting behavior of a function when the argument tends towards a particular value or infinity, commonly used in computer science to classify algorithms according to how their run time or space requirements grow as the input size grows.

## What is Big O Notation?

Big O notation, written as **O(f(n))**, describes the **upper bound** of an algorithm's time or space complexity in the worst-case scenario. It gives us a way to describe how the performance of an algorithm scales with the size of the input data.

### Key Characteristics:
- **Growth Rate**: How runtime increases as input size increases
- **Worst Case**: Focuses on the maximum time/space an algorithm might need
- **Asymptotic**: Behavior as input approaches infinity
- **Scalability**: How well an algorithm performs with large datasets

## Common Big O Complexities

### 1. **O(1) - Constant Time**
```
Performance: Excellent
```
- **Definition**: Algorithm takes the same amount of time regardless of input size
- **Examples**: 
  - Array element access by index
  - Hash table lookup (average case)
  - Stack push/pop operations
- **Graph**: Flat horizontal line

```python
def get_first_element(arr):
    return arr[0]  # Always takes same time regardless of array size
```

### 2. **O(log n) - Logarithmic Time**
```
Performance: Excellent
```
- **Definition**: Runtime grows logarithmically with input size
- **Examples**:
  - Binary search in sorted array
  - Tree operations (balanced trees)
  - Divide and conquer algorithms
- **Graph**: Slow-growing curve that levels off

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

### 3. **O(n) - Linear Time**
```
Performance: Good
```
- **Definition**: Runtime grows linearly with input size
- **Examples**:
  - Linear search through unsorted array
  - Single loop through array
  - Finding min/max in unsorted array
- **Graph**: Straight diagonal line

```python
def linear_search(arr, target):
    for i, element in enumerate(arr):
        if element == target:
            return i
    return -1
```

### 4. **O(n log n) - Linearithmic Time**
```
Performance: Fair
```
- **Definition**: Combination of linear and logarithmic growth
- **Examples**:
  - Efficient sorting algorithms (Merge Sort, Quick Sort, Heap Sort)
  - Fast Fourier Transform
- **Graph**: Slightly curved upward from linear

```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    
    return merge(left, right)
```

### 5. **O(n²) - Quadratic Time**
```
Performance: Poor
```
- **Definition**: Runtime grows quadratically with input size
- **Examples**:
  - Bubble Sort, Selection Sort, Insertion Sort
  - Nested loops over same dataset
  - Naive string matching
- **Graph**: Steep upward curve

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr
```

### 6. **O(n³) - Cubic Time**
```
Performance: Very Poor
```
- **Definition**: Runtime grows cubically with input size
- **Examples**:
  - Triple nested loops
  - Naive matrix multiplication
  - Some dynamic programming solutions
- **Graph**: Very steep upward curve

### 7. **O(2ⁿ) - Exponential Time**
```
Performance: Terrible
```
- **Definition**: Runtime doubles with each additional input element
- **Examples**:
  - Recursive Fibonacci (naive implementation)
  - Subset generation
  - Traveling Salesman Problem (brute force)
- **Graph**: Extremely steep exponential curve

```python
def fibonacci_naive(n):
    if n <= 1:
        return n
    return fibonacci_naive(n-1) + fibonacci_naive(n-2)
```

### 8. **O(n!) - Factorial Time**
```
Performance: Catastrophic
```
- **Definition**: Runtime grows factorially with input size
- **Examples**:
  - Generating all permutations
  - Traveling Salesman Problem (brute force with all permutations)
- **Graph**: Fastest growing complexity

## Big O Complexity Comparison

| Big O      | Name           | n=1 | n=10   | n=100     | n=1,000     | n=10,000      |
|------------|----------------|-----|--------|-----------|-------------|---------------|
| O(1)       | Constant       | 1   | 1      | 1         | 1           | 1             |
| O(log n)   | Logarithmic    | 1   | 3      | 7         | 10          | 13            |
| O(n)       | Linear         | 1   | 10     | 100       | 1,000       | 10,000        |
| O(n log n) | Linearithmic   | 1   | 30     | 700       | 10,000      | 130,000       |
| O(n²)      | Quadratic      | 1   | 100    | 10,000    | 1,000,000   | 100,000,000   |
| O(2ⁿ)      | Exponential    | 1   | 1,024  | 1.27×10³⁰ | -           | -             |
| O(n!)      | Factorial      | 1   | 3,628,800 | -      | -           | -             |

## Space Complexity

Big O notation also applies to **space complexity** - how much memory an algorithm uses.

### Common Space Complexities:

- **O(1)**: Constant space (only using a fixed amount of variables)
- **O(n)**: Linear space (space grows with input size)
- **O(n²)**: Quadratic space (2D arrays, matrices)

```python
# O(1) space - only uses a few variables
def find_max(arr):
    max_val = arr[0]
    for num in arr[1:]:
        if num > max_val:
            max_val = num
    return max_val

# O(n) space - creates a new array
def reverse_array(arr):
    return arr[::-1]

# O(n²) space - creates a 2D matrix
def create_matrix(n):
    return [[0 for _ in range(n)] for _ in range(n)]

## How to Analyze Big O
```

## 🎯 How to Analyze Big O

### Step-by-Step Process:

1. **Identify the input size** (usually denoted as 'n')
2. **Look for loops and recursive calls**
3. **Count nested operations**
4. **Focus on the fastest-growing term**
5. **Drop constants and lower-order terms**

### Rules for Analysis:

#### 1. **Drop Constants**
```python
# This is O(n), not O(3n)
def example(arr):
    for i in range(len(arr)):      # n operations
        print(arr[i])
    for i in range(len(arr)):      # n operations  
        print(arr[i] * 2)
    for i in range(len(arr)):      # n operations
        print(arr[i] * 3)
# Total: 3n operations = O(n)
```

#### 2. **Drop Lower-Order Terms**
```python
# This is O(n²), not O(n² + n)
def example(arr):
    for i in range(len(arr)):           # n operations
        for j in range(len(arr)):       # n² operations
            print(arr[i], arr[j])
    
    for i in range(len(arr)):           # n operations
        print(arr[i])
# Total: n² + n operations = O(n²)
```

#### 3. **Different Inputs = Different Variables**
```python
# This is O(a + b), not O(n)
def example(arr1, arr2):
    for item in arr1:     # 'a' operations
        print(item)
    for item in arr2:     # 'b' operations
        print(item)
```

#### 4. **Nested Loops = Multiplication**
```python
# This is O(a * b)
def example(arr1, arr2):
    for item1 in arr1:           # 'a' operations
        for item2 in arr2:       # 'b' operations for each 'a'
            print(item1, item2)

## Algorithm Analysis Examples
```

## 🛠️ Algorithm Analysis Examples

### Example 1: Two Sum Problem

```python
# Brute Force - O(n²) time, O(1) space
def two_sum_brute_force(nums, target):
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[i] + nums[j] == target:
                return [i, j]
    return []

# Optimized with Hash Map - O(n) time, O(n) space
def two_sum_optimized(nums, target):
    seen = {}
    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i
    return []
```

### Example 2: String Reversal

```python
# Method 1: O(n) time, O(n) space
def reverse_string_1(s):
    return s[::-1]

# Method 2: O(n) time, O(1) space (in-place)
def reverse_string_2(s):
    s = list(s)
    left, right = 0, len(s) - 1
    while left < right:
        s[left], s[right] = s[right], s[left]
        left += 1
        right -= 1
    return ''.join(s)
```

## Best, Average, and Worst Case

### Quick Sort Example:
- **Best Case**: O(n log n) - pivot always divides array evenly
- **Average Case**: O(n log n) - typical random input
- **Worst Case**: O(n²) - already sorted array with poor pivot choice

### Binary Search Example:
- **Best Case**: O(1) - target is in the middle
- **Average Case**: O(log n) - typical search
- **Worst Case**: O(log n) - target is at end or not found

## Optimization Strategies

### 1. **Choose Better Data Structures**
```python
# Slow: O(n) lookup in list
if item in my_list:  # O(n)
    # do something

# Fast: O(1) average lookup in set
if item in my_set:   # O(1)
    # do something
```

### 2. **Use Caching/Memoization**
```python
# Slow: O(2ⁿ) - recalculates same values
def fibonacci_slow(n):
    if n <= 1:
        return n
    return fibonacci_slow(n-1) + fibonacci_slow(n-2)

# Fast: O(n) - with memoization
def fibonacci_fast(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fibonacci_fast(n-1, memo) + fibonacci_fast(n-2, memo)
    return memo[n]
```

### 3. **Early Termination**
```python
# Continue searching even after finding answer
def linear_search_slow(arr, target):
    found = False
    for item in arr:
        if item == target:
            found = True
    return found

# Stop as soon as answer is found
def linear_search_fast(arr, target):
    for item in arr:
        if item == target:
            return True
    return False
```

## Practice Problems

### Beginner Level:
1. **Array Sum**: Calculate sum of all elements in array
2. **Find Maximum**: Find largest element in unsorted array
3. **Count Occurrences**: Count how many times element appears
4. **Palindrome Check**: Determine if string reads same forwards/backwards

### Intermediate Level:
1. **Binary Search**: Implement iterative and recursive versions
2. **Merge Two Sorted Arrays**: Combine two sorted arrays efficiently
3. **Remove Duplicates**: Remove duplicate elements from sorted array
4. **Valid Anagram**: Check if two strings are anagrams

### Advanced Level:
1. **Longest Common Subsequence**: Dynamic programming approach
2. **Graph Traversal**: BFS and DFS implementations
3. **Sliding Window Maximum**: Find maximum in all subarrays of size k
4. **Design LRU Cache**: Implement Least Recently Used cache

### Visualization Tools:
- [Algorithm Visualizer](https://algorithm-visualizer.org/)
- [VisuAlgo](https://visualgo.net/)
- [Big O Calculator](https://www.bigocalculator.com/)

