Стандартный вывод в Rust при помощи макроса `println!()` не эффективен, ибо это все же макрос. Для быстрого вывода можем использовать запись в буфер напрямую при помощи крейтов `Bufwriter` и `Write`

```Rust
use std::io::{BufWriter, Write};

fn main() {
    let stdout = std::io::stdout(); // Переменная вывода
    let mut writer = BufWriter::new(stdout); // Запись в буфер
    for i in 1..=2_000_000 {
        write!(writer, "i: {}\n", i).unwrap(); // Вывод
    }
}
```

`write!` - макрос, который в отличие от `println!` пишет в заданный буфер, а не в `stdout`.
`.unwrap()` разворачивает результат `Result` в `Ok()` или `Err`.

Вариант переписанный с `Result<()>` в конце. Функция возвращает либо `Err()`, либо `Ok()` 

```rust
use std::io::{BufWriter, Write, Result};

fn main() -> Result<()> {
    let stdout = std::io::stdout();
    let mut writer = BufWriter::new(stdout);

    for i in 1..=2_000_000 {
        write!(writer, "i: {}\n", i)?;
    }

    writer.flush()?;

    Ok(())
}
```

---
[[Rust]] [[Rust optimizations]] [[Быстрый вывод Rust]]