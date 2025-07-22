# Recursion Basics

Recursion is when a function calls itself to solve a smaller version of the problem.

## 1. Key Concepts
- **Base Case**: The condition under which the function stops calling itself.
- **Recursive Case**: The part where the function calls itself with a simpler input.

## 2. Example: Factorial
```python
def factorial(n):
    if n == 0:
        return 1  # Base case
    else:
        return n * factorial(n - 1)  # Recursive case

print(factorial(5))  # Output: 120
```

## 3. Example: Fibonacci
```python
def fibonacci(n):
    if n <= 1:
        return n
    else:
        return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(6))  # Output: 8
```

## 4. Tips
- Always define a base case to avoid infinite recursion.
- Recursion can often be replaced with loops, but is useful for problems that can be broken into similar subproblems.

---

Practice writing recursive functions to get comfortable with this concept!
