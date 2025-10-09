In C programming language there are some rules of type conversion. Usually a narrower type is converted to a wider type like in `f + i` i will be converted to float

A `char` is just small integer by implementation, so we can freely use it in arithmetic operations:

```c
int atoi(char s[]) {
	int i, n;
	
	n = 0;
	for (i = 0; s[i] >= '0' && s[i] <= '9'; i++) {
		n = 10 * n + (s[i] - '0')
	}
	return n;
}
// "123" -> 123
```

Here `s[i] - '0'` gives a numeric value of char stored in `s[i]`.

Another example is function `lower`. We are just subtracting known value from `char`:

```c
int lower(int c) {
	if (c >= 'A' && c <= 'Z')
		return c + 'a' - 'A'
	else
		return c;
}
```

[[C]]