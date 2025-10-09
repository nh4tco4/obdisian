#c

The control-flow of a language specify the order in which computations are performed

Expressions such as `x = 0` or `i++` or `printf(...)` becomes a statement when it is followed by a semicolon as in:

```C
x = 0;
i++;
printf(...);
```

In C, the semicolon is a statement terminator, rather than a separator (like in Rust)

Braces are for grouping the declarations

Basically `if-else` statement is used to express decisions:

```c
if (expression) 
	statement;
else
	statement;
```

---
[[Expressions and statements Rust]]