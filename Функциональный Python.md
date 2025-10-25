#python 

Введем функциональное программирование на пайтоне при помощи следующих правил и модулей:

1. Испольузются только чистые функции. Они зависят только от входных аргументов и не меняют ничего снаружи. Глобальные переменные не используются
2. Изменять объекты запрещено, можно только создавать новые
3. Предпочтительно использование немутабельных типов (пусть и все типы теоретически мутабельные)
4. Функции - объекты первого классса. В них можно передавать функции и возвращать их
5. Данные преобразуются декларативно. `map` `filter` `reduce` должны преобладать над циклами
6. Генераторы и ленивые вычисления предпочтительнее
7. Следует избегать циклов `for` и `while` в пользу рекурсии и функций старшего порядка
8. Следует использовать композиции функций вместо вложенных вызовов
9. Аннотация типов обязательна

Код для композиции:
```python
from functools import reduce

def compose(*functions):
    """
    Принимает функции f1, f2, ..., fn
    Возвращает функцию (f1 ∘ f2 ∘ ... ∘ fn)(x)
    """
    return lambda x: reduce(lambda acc, f: f(acc), reversed(functions), x)
```

Пример кода преобразования строки:
```python
from functools import reduce

def compose(*functions):
    """
    Принимает функции f1, f2, ..., fn
    Возвращает функцию (f1 ∘ f2 ∘ ... ∘ fn)(x)
    """
    return lambda x: reduce(lambda acc, f: f(acc), reversed(functions), x)

def strip(s):
    return s.strip()

def lower(s):
    return s.lower()

def remove_commas(s):
    return s.replace(",", "")

def wrap_in_brackets(s):
    return f"[{s}]"
    
clean_and_format = compose(
    wrap_in_brackets,
    remove_commas,
    lower,
    strip
)

text = "  Hello, World!  "
result = clean_and_format(text)
print(result) # [hello, world!]
```

---
[[Python]] [[Функциональное Программирование]]