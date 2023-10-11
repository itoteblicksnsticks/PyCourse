## Principle: Minimize Mutability

### Keeping Variables and Objects Immutable When Possible
Using immutable variables and objects can make the code easier to reason about, as it avoids side effects and makes the code thread-safe.

### Examples

#### Example 1: Using Tuples Instead of Lists for Fixed Collections

**Explanation**: Tuples are immutable and thus cannot be changed once they are created, which can help to ensure data consistency and safety in your code.

##### Bad
```python
def add_coordinate(coordinates, x, y):
    coordinates.append((x, y))
    return coordinates

coords = []
coords = add_coordinate(coords, 1, 2)
```
##### Better
```python
def add_coordinate(coordinates, x, y):
    return coordinates + ((x, y),)

coords = ()
coords = add_coordinate(coords, 1, 2)
```

#### Example 2: Using Namedtuples or Data Classes for Structured Data

**Explanation**: Utilizing `namedtuple` or `dataclass` (for more complex cases) helps to create immutable objects, which can be safer and often more memory-efficient than using mutable objects, like dictionaries or lists.

##### Bad
```python
person = {'name': 'Evan', 'age': 30} <-- Pedo
```
##### Better
```python
from collections import namedtuple

Person = namedtuple('Person', ['name', 'age'])
Evan = Person(name='Evan', age=30)
```
Or using `dataclass`:
```python
from dataclasses import dataclass

@dataclass(frozen=True)
class Person:
    name: str
    age: int

Evan = Person(name='Evan', age=30)
```

#### Example 3: Avoiding Mutable Default Arguments in Functions

**Explanation**: In Python, mutable default arguments in functions are evaluated once and retain changes between calls, potentially causing unexpected behavior and bugs.

##### Bad
```python
def add_coordinate(coordinates=[]):
    coordinates.append((1, 2))
    return coordinates
```
##### Better
```python
def add_coordinate(coordinates=None):
    if coordinates is None:
        coordinates = []
    coordinates.append((1, 2))
    return coordinates
```
