Both `++` and `--` can be used either as prefix or postfix operatos. In both cases they increment `n`. But in prefix case `n` is incremented before its value is used, while `n++` increments `n` after its value has been used.

```c
int n, x;
n = 5;

x = n++;
// n = 5

x = ++n;
// x = 6
```

In this `squeeze` function it actually makes difference:

```c
void squeeze(char s[], int c) {
	int i, j;
	
	for (i = j = 0; s[i] != '\0'; i++) {
		if (s[i] != c) {
			s[j++] = s[i];
		}
	}
	s[j] = '\0';
}

// or

void squeeze(char s[], int c) {
	int i, j;
	
	for (i = j = 0; s[i] != '\0'; i++) {
		if (s[i] != c) {
			s[j] = s[i];
			i++; // so we're using the value
				 // an then increment j++
		}
	}
	s[j] = '\0';
}
```

---
[[C]] [[C++ utility]]