To counts 1 bits in in we can use this naive approach:

```c
int bitcount(unsigned x) {
	int b = 0;
	
	for (b = 0; x != 0; x >>= 1) {
		if (x & 1) b++;
	}
}

```

Where `>>=` is the right shift by 1 and assignation to x and & is the logical AND
Or we can use faster Brian Kernighan’s Algorith:

```c
int bitcount(unsigned x) {
    int b = 0;
    while (x) {
        x &= x - 1;
        b++;
    }
    return b;
}
```

It ignores zeros entirely and therefore makes less operations

---
[[Побитовые операции C]]