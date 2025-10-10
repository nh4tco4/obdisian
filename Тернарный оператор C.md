C language has conditional operator `?` with following syntax:

```c
expr1, ? expr2 : expr3
```

For example:

```c
z = (a > b) ? a : b;
// z = a > b ? a : b;
```

If `a > b` is true then `z` is set to the value of `a` else `z` is set to the value of `b`. So basically this is the function `max(a, b)`

---
[[C]]