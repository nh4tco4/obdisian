Пока что есть 4 способа оптимизации вывода

## cout -> printf

`printf` является функцией с меньшим количеством имплементаций, чем поток вывода `cout`:

```cpp
#include <stdio.h>

void prf() {
  for (int i = 0; i < 2000000; ++i) {
    printf("i: %i \n", i);
  }
}
```

## sync_with_stdio

Можем отключить синхронизацию с хедером `stdio` для ускорения работы программы, оставив при этом `cout`, а также отвязка `cout` от `cin` для того чтобы убрать лишний `flush`:

```cpp
void out_fast() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);
    
    for (int i = 1; i <= 2000000; ++i) {
        std::cout << i << '\n';
    }
}
```

## Buffered

Записываем данные напрямую в буфер при помощи `sstream`:

```cpp
void out_buffered() {
    std::ostringstream oss; // создание переменной буфера
    for (int i = 1; i <= 2000000; ++i) {
        oss << i << '\n'; // загрузка в буфер
    }
    std::cout << oss.str(); // вывод буфера
}
```

---
[[C++]] [[C++ optimizations]]