#python 

Magic methods or dunder methods are used by python automatically in response to specific operations or built-in functions. By implementing them in classes we can redefine operands and set how our objects behave in different contexts.

For classes we have these dunder methods:

| Magic method              | What used for                                                              | Simular methods                                                            |
| ------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `__repr__`                | Representation of a class for developer                                    |                                                                            |
| `__str__`<br>             | Friendly representation of class for user                                  |                                                                            |
| `__init__`                | Attributes that class will have when we create it's instance<br>           |                                                                            |
| `__new__`                 | Control of creating a new instance                                         |                                                                            |
| `__eq__`                  | Redefinition of `==` operator for class. Can also redefine other operators | `__ne__` `__lt__` `__le__` `__gt__` `__ge___`                              |
| `__add__`                 | Redefinition of `+` operator for class. Can also redefine other operators  | `__sub__` `__mul__`<br>`__truediv__`<br>`__floordiv__` `__mod__` `__pow__` |
| `__call__`                | Makes our object callable                                                  |                                                                            |
| `__getitem__`             | Implementation of indexing elements                                        | `__setitem__`                                                              |
| `__contains__`            | Checking if element is in class                                            |                                                                            |
| `__bool__`                | Setting a boolean representation for class                                 |                                                                            |
| `__len__`                 | Getting a length of a class                                                |                                                                            |
| `__exit__`<br>`__enter__` | Context manager interaction                                                |                                                                            |
| `__iter__`                | Iterators for for loops. Next just returns next element of a class         | `__next__`                                                                 |
|                           |                                                                            |                                                                            |

```python
class Vector:
	# intialisation of a vector
    def __init__(self, x, y):
        self.x = x
        self.y = y

	# representation
    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

	# friendly representation
    def __str__(self):
        return f"({self.x}, {self.y})"

	# redifining + operator
    def __add__(self, other):
        if isinstance(other, Vector):
            return Vector(self.x + other.x, self.y + other.y)
        return NotImplemented

	# redifining == operator
    def __eq__(self, other):
        return isinstance(other, Vector) and (self.x, self.y) == (other.x, other.y)

	# getting a length of vector
    def __len__(self):
        return int((self.x**2 + self.y**2) ** 0.5)

	# setting boolean representation
    def __bool__(self):
        return self.x != 0 or self.y != 0
```

---
[[Context Manager Python]] [[Data class Python]] [[Class Python]]