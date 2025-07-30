# Hashmap in Python: From Beginner to Advanced

A hashmap (or dictionary in Python) is a data structure that stores key-value pairs with fast access times.

## 1. Beginner Level: Understanding Hashmaps

### What is a Hashmap?
- A hashmap stores data as key-value pairs
- Uses a hash function to convert keys into array indices
- Provides O(1) average time complexity for insert, delete, and search operations

### Basic Python Dictionary Usage
```python
# Creating a dictionary
student = {
    "name": "Alice",
    "age": 20,
    "grade": "A"
}

# Accessing values
print(student["name"])  # Output: Alice

# Adding/updating values
student["city"] = "New York"
student["age"] = 21

# Checking if key exists
if "name" in student:
    print("Name exists")

# Getting value with default
grade = student.get("grade", "N/A")
```

## 2. Intermediate Level: How Hashmaps Work

### Hash Function
A hash function converts a key into an integer (hash value):
```python
# Python's built-in hash function
print(hash("hello"))  # Output: varies by Python version
print(hash(42))       # Output: 42
print(hash((1, 2)))   # Output: varies
```

### Collision Handling
When two keys hash to the same index, we have a collision. Python uses open addressing with probing.

### Custom Hashmap Implementation
```python
class SimpleHashMap:
    def __init__(self, size=10):
        self.size = size
        self.buckets = [[] for _ in range(size)]  # List of lists for chaining
    
    def _hash(self, key):
        return hash(key) % self.size
    
    def put(self, key, value):
        index = self._hash(key)
        bucket = self.buckets[index]
        
        # Check if key already exists
        for i, (k, v) in enumerate(bucket):
            if k == key:
                bucket[i] = (key, value)
                return
        
        # Add new key-value pair
        bucket.append((key, value))
    
    def get(self, key):
        index = self._hash(key)
        bucket = self.buckets[index]
        
        for k, v in bucket:
            if k == key:
                return v
        return None
    
    def delete(self, key):
        index = self._hash(key)
        bucket = self.buckets[index]
        
        for i, (k, v) in enumerate(bucket):
            if k == key:
                del bucket[i]
                return True
        return False

# Usage
hm = SimpleHashMap()
hm.put("name", "Alice")
hm.put("age", 25)
print(hm.get("name"))  # Output: Alice
```

## 3. Advanced Level: Advanced Hashmap Concepts

### Load Factor and Resizing
```python
class AdvancedHashMap:
    def __init__(self, initial_size=16, load_factor=0.75):
        self.size = initial_size
        self.load_factor = load_factor
        self.buckets = [[] for _ in range(initial_size)]
        self.count = 0
    
    def _resize(self):
        old_buckets = self.buckets
        self.size *= 2
        self.buckets = [[] for _ in range(self.size)]
        self.count = 0
        
        for bucket in old_buckets:
            for key, value in bucket:
                self.put(key, value)
    
    def put(self, key, value):
        if self.count / self.size >= self.load_factor:
            self._resize()
        
        index = self._hash(key)
        bucket = self.buckets[index]
        
        for i, (k, v) in enumerate(bucket):
            if k == key:
                bucket[i] = (key, value)
                return
        
        bucket.append((key, value))
        self.count += 1
```

### Custom Hashable Objects
```python
class Student:
    def __init__(self, id, name):
        self.id = id
        self.name = name
    
    def __hash__(self):
        return hash(self.id)  # Use id for hashing
    
    def __eq__(self, other):
        return self.id == other.id
    
    def __str__(self):
        return f"Student({self.id}, {self.name})"

# Usage
student_map = {}
s1 = Student(1, "Alice")
s2 = Student(2, "Bob")

student_map[s1] = "Grade A"
student_map[s2] = "Grade B"

print(student_map[s1])  # Output: Grade A
```

### Performance Analysis
```python
import time

def benchmark_hashmap():
    # Test different sizes
    sizes = [100, 1000, 10000, 100000]
    
    for size in sizes:
        # Create dictionary
        d = {}
        start = time.time()
        
        # Insert operations
        for i in range(size):
            d[i] = f"value_{i}"
        
        insert_time = time.time() - start
        
        # Search operations
        start = time.time()
        for i in range(size):
            _ = d.get(i)
        
        search_time = time.time() - start
        
        print(f"Size: {size}, Insert: {insert_time:.6f}s, Search: {search_time:.6f}s")

# Run benchmark
benchmark_hashmap()
```

## 4. Real-World Applications

### Word Frequency Counter
```python
def word_frequency(text):
    words = text.lower().split()
    frequency = {}
    
    for word in words:
        frequency[word] = frequency.get(word, 0) + 1
    
    return frequency

text = "hello world hello python world"
result = word_frequency(text)
print(result)  # Output: {'hello': 2, 'world': 2, 'python': 1}
```

### Caching with LRU (Least Recently Used)
```python
from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity):
        self.capacity = capacity
        self.cache = OrderedDict()
    
    def get(self, key):
        if key in self.cache:
            # Move to end (most recently used)
            self.cache.move_to_end(key)
            return self.cache[key]
        return -1
    
    def put(self, key, value):
        if key in self.cache:
            # Update existing key
            self.cache.move_to_end(key)
        else:
            # Check capacity
            if len(self.cache) >= self.capacity:
                # Remove least recently used (first item)
                self.cache.popitem(last=False)
        
        self.cache[key] = value

# Usage
cache = LRUCache(2)
cache.put(1, "value1")
cache.put(2, "value2")
print(cache.get(1))  # Output: value1
cache.put(3, "value3")  # Removes key 2
print(cache.get(2))  # Output: -1
```

## 5. Common Interview Questions

### Two Sum Problem
```python
def two_sum(nums, target):
    seen = {}
    
    for i, num in enumerate(nums):
        complement = target - num
        
        if complement in seen:
            return [seen[complement], i]
        
        seen[num] = i
    
    return []

# Test
nums = [2, 7, 11, 15]
target = 9
print(two_sum(nums, target))  # Output: [0, 1]
```

### Group Anagrams
```python
def group_anagrams(strs):
    groups = {}
    
    for s in strs:
        # Sort string to get canonical form
        sorted_s = ''.join(sorted(s))
        
        if sorted_s in groups:
            groups[sorted_s].append(s)
        else:
            groups[sorted_s] = [s]
    
    return list(groups.values())

# Test
strs = ["eat", "tea", "tan", "ate", "nat", "bat"]
print(group_anagrams(strs))
# Output: [['eat', 'tea', 'ate'], ['tan', 'nat'], ['bat']]
```

## 6. Best Practices

1. **Choose good hash functions**: Should distribute keys evenly
2. **Handle collisions**: Use chaining or open addressing
3. **Monitor load factor**: Resize when needed
4. **Use immutable keys**: Keys should be hashable and immutable
5. **Consider thread safety**: Use `collections.defaultdict` or `threading.Lock` for concurrent access

## 7. Time Complexity Summary

| Operation | Average Case | Worst Case |
|-----------|--------------|------------|
| Insert    | O(1)         | O(n)       |
| Delete    | O(1)         | O(n)       |
| Search    | O(1)         | O(n)       |
| Space     | O(n)         | O(n)       |

---

Practice implementing these concepts to master hashmap usage in Python! 