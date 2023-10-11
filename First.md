## Principle: Readability > Complexity
  
### Using Self-Explanatory Code Instead of Comments
Choose variable and function names that describe their purpose or usage rather than short, ambiguous names.

### Examples

#### Example 1: Descriptive Variable Names and Avoiding Magic Numbers

_**Explanation**_: Descriptive names and avoiding "magic numbers" (using named constants instead of direct numbers) ensure the code is easier to understand and modify.

##### Bad
```python
def p(r):
    return 3.14 * r * r
```
##### Better
```python
def calculate_circle_area(radius):
    PI = 3.14  # Defining a constant instead of using a magic number
    return PI * radius * radius
```

#### Example 2: Avoid Deep Nesting and Provide Early Exits

_**Explanation**_: Avoiding deep nesting and providing early exits where possible can make the code easier to follow.

##### Bad
```python
def find_xyz(n):
    for i in range(n):
        for j in range(n):
            for k in range(n):
                if i + j + k == n:
                    return i, j, k
```
##### Better
```python
def find_xyz(n):
    for i in range(n):
        for j in range(n - i):
            k = n - i - j
            if i + j + k == n:
                return i, j, k
```

#### Example 3: Use List Comprehensions Judiciously

_**Explanation**_: List comprehensions provide a concise way to create lists. They can be useful and readable in simple cases but should be used judiciously to avoid reducing readability in more complex situations.

##### Bad
```python
squares = []
for x in range(10):
    squares.append(x**2)
```
##### Better
```python
squares = [x**2 for x in range(10)]
```
