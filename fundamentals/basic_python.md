# Basic Python Syntax and Data Types

This section covers the essential Python syntax and built-in data types you need to get started with DSA.

## 1. Variables and Data Types

Variables store data. Python is dynamically typed, so you don't need to declare types explicitly.

```python
x = 5           # Integer
y = 3.14        # Float
name = "Alice"  # String
is_valid = True # Boolean
```

## 2. Basic Data Types
- **int**: Integer numbers (`x = 10`)
- **float**: Decimal numbers (`y = 3.14`)
- **str**: Text (`name = "Bob"`)
- **bool**: True/False (`flag = False`)

## 3. Lists
Lists are ordered, mutable collections.

```python
fruits = ["apple", "banana", "cherry"]
fruits.append("orange")
print(fruits[1])  # Output: banana
```

## 4. Tuples
Tuples are ordered, immutable collections.

```python
point = (2, 3)
print(point[0])  # Output: 2
```

## 5. Dictionaries
Dictionaries store key-value pairs.

```python
person = {"name": "Alice", "age": 25}
print(person["name"])  # Output: Alice
```

## 6. Control Flow
### If Statements
```python
x = 10
if x > 5:
    print("x is greater than 5")
elif x == 5:
    print("x is 5")
else:
    print("x is less than 5")
```

### For Loops
```python
for i in range(3):
    print(i)  # Output: 0 1 2
```

### While Loops
```python
count = 0
while count < 3:
    print(count)
    count += 1
```

## 7. Functions
Functions are defined using `def`.

```python
def greet(name):
    return f"Hello, {name}!"

print(greet("Alice"))
```

---

Practice these basics to build a strong foundation for DSA in Python!
