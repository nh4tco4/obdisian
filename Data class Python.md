#python 

To make our code cleaner and not define `__init__`, `__eq__` and `__repr__` every single time we write a new class we can create a data class that will already have this fields.
Although we should only use this if our class contains some data.

```python
from dataclasses import dataclass

@dataclass
class Vector:
	x: int
	y: int
	
# instead of 
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y


    def __repr__(self):
        return f"Vector({self.x}, {self.y})"


    def __eq__(self, other):
        return isinstance(other, Vector) and (self.x, self.y) == (other.x, other.y)
```

---
