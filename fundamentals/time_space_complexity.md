# Time and Space Complexity (Big O Notation)

Understanding how efficient an algorithm is can help you write better code. We use Big O notation to describe the worst-case performance.

## 1. What is Big O Notation?
- Describes how the runtime or space requirements grow as the input size increases.
- Focuses on the dominant term as input size (n) becomes large.

## 2. Common Complexity Classes
- **O(1)**: Constant time (does not depend on input size)
  - Example: Accessing an element in a list by index.
- **O(log n)**: Logarithmic time
  - Example: Binary search.
- **O(n)**: Linear time
  - Example: Looping through a list.
- **O(n log n)**: Linearithmic time
  - Example: Merge sort.
- **O(n^2)**: Quadratic time
  - Example: Nested loops over a list.

## 3. Examples
```python
# O(1)
def get_first_element(arr):
    return arr[0]

# O(n)
def print_all(arr):
    for item in arr:
        print(item)

# O(n^2)
def print_pairs(arr):
    for i in arr:
        for j in arr:
            print(i, j)
```

## 4. Space Complexity
- Measures how much extra memory an algorithm uses.
- Example: Creating a new list of size n is O(n) space.

---

Knowing time and space complexity helps you choose the right algorithm for the job!
