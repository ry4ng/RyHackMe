---
title: "The Gang’s Guide to Algorithms: Largest Range [Technical Walkthrough - Python]"
date: 2024-10-26 22:50:17
author: ['ry4ng']
tags: ['algorithms','python','programming','software development','technical walkthrough', 'tech interviews']
---

## **Problem Statement**

Write a function that takes in an array of integers and returns an array of length 2 representing the **largest range** of numbers contained in that array. The first number in the output array should be the start of the range, and the second number should be the end of the range. A range of numbers is defined as a set of consecutive integers. For example, the output `[2, 6]` represents the range `{2, 3, 4, 5, 6}`, which has a length of 5.

- **Input**: `[1, 11, 3, 0, 15, 5, 2, 4, 10, 7, 12, 6]`
- **Output**: `[0, 7]`

The input numbers do not need to be ordered or next to each other in the array to form a range, and there will only be one largest range.

---

## **Solution Overview**

We aim to solve this efficiently by creating a hash map for fast lookups and marking numbers as visited, allowing us to find and expand the largest range in **O(N)** time. Let’s dive into each part of the solution.

### **Solution Code**

```python
nums = [1,2,3,4,5,6,7,8,9,10,11,88,89,76,77,78,79,80,81,82,83,84,85,86,87,300,310,305,308,309,1002,1005,1007,1006,1009]

hash_nums = {i:False for i in nums}
largest_range = [0,0]

for num in hash_nums:
    # If the number has already been checked previously move on
    if hash_nums[num]:
        continue

    left = num - 1 
    right = num + 1

    while left in hash_nums:
        hash_nums[left] = True
        left -= 1
    left += 1

    while right in hash_nums:
        hash_nums[right] = True
        right += 1
    right -= 1

    if (right - left) >= (largest_range[1] - largest_range[0]):
        largest_range = [left, right]

print(largest_range)
```

---

## **Step-by-Step Explanation**

### **1. Preparing the Hash Map**

To efficiently keep track of which numbers we have processed, we use a hash map:
```python
hash_nums = {i:False for i in nums}
```
This line creates a dictionary (`hash_nums`) with each number from the array as a key. The initial value for each key is set to `False`, indicating that we haven’t visited these numbers yet. Using a hash map allows us to perform lookups in **O(1)** time, which speeds up the solution significantly.

### **2. Initialize the Largest Range**

Before entering the main loop, we initialize `largest_range`:
```python
largest_range = [0, 0]
```
This variable stores the starting and ending numbers of the current largest range we’ve found so far.

### **3. Main Loop: Traversing Each Number**

The primary part of the solution involves iterating through each number in `hash_nums`:
```python
for num in hash_nums:
    if hash_nums[num]:
        continue
```
Here’s what each part does:
- **Loop through `hash_nums`**: We loop through each number in our hash map.
- **Skip Already Processed Numbers**: If a number has already been marked `True` in `hash_nums`, it means it was part of a range we’ve already examined, so we skip it.

### **4. Expanding the Range Left and Right**

For each unvisited number, we want to find the largest possible range that includes it:
```python
left = num - 1 
right = num + 1
```
- **Left Expansion**: We start with `left = num - 1` and keep moving left (decreasing `left`) until we reach a number not in `hash_nums`. As we move, we mark each number in `hash_nums` as `True`, indicating it’s been visited. Once the loop breaks, we increment `left` by one to get the correct starting point of the range.
  
    ```python
    while left in hash_nums:
        hash_nums[left] = True
        left -= 1
    left += 1
    ```
    
- **Right Expansion**: Similarly, we start with `right = num + 1` and move right, marking each number as visited until we reach a number not in `hash_nums`. When the loop exits, we decrement `right` by one to set the correct ending point of the range.

    ```python
    while right in hash_nums:
        hash_nums[right] = True
        right += 1
    right -= 1
    ```

### **5. Updating the Largest Range**

After expanding both left and right, we have a complete range from `left` to `right`. We compare the size of this range to our current `largest_range`:
```python
if (right - left) >= (largest_range[1] - largest_range[0]):
    largest_range = [left, right]
```
If this new range is larger than `largest_range`, we update `largest_range` to store the new values of `left` and `right`. The equality condition (`>=`) ensures that if two ranges have the same size, we still update to the newest range.

### **6. Final Output**

At the end of the loop, `largest_range` holds the largest consecutive range found in the array:
```python
print(largest_range)
```
For the provided example, this would output `[76, 89]`, meaning the largest range in the array runs from `76` to `89`, inclusive.

---

## **Efficiency Analysis**

- **Time Complexity**: **O(N)**. Each number in the input array is processed at most once. The hash map allows for **O(1)** lookups, so expanding left and right for each number only happens if necessary.
  
- **Space Complexity**: **O(N)**. We store each number in a hash map, which requires additional memory equivalent to the size of the input.

![Alt Text](o-n-time-complexity.png)

This graphic illustrates the concept of `O(N)` time complexity. As the input size `N` increases, the number of operations grows linearly, showing that for each additional element in the input, one additional operation is required. This "linear growth" is characteristic of `O(N)` complexity, where the time it takes scales directly with the size of the input. 

In the context of our solution, this means that every element in the input is only processed once, making the overall efficiency linearly proportional to `N`.

---

## **Conclusion**

This solution efficiently finds the largest consecutive range of numbers within an array by leveraging a hash map for fast lookups and marking numbers as visited. This prevents redundant operations and keeps the solution performant even for large inputs.


