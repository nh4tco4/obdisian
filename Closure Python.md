#python

Это запоминание вложенной функцией значений внешней функции, даже если внешняя завершила работу

```python
def outer(x):
	def inner():
		return x
	return inner
	
f = outer(42)
```