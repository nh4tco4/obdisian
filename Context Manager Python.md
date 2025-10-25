A **context manager** in Python is a protocol (or design pattern) that enables **safe and automatic resource management** — ensuring that setup and cleanup logic are always executed, even if an error occurs 

```python
with open("demo_data.txt", "w", encoding="utf-8") as demo_file:
	print("Hello World!", file=demo_file) 
```

A simple example of a class that works as a context manager

```python
def connect_to_db():
	...
	
	
class DatabaseConnection:
    def __enter__(self):
        print("Opening database connection")
        self.conn = connect_to_db()
        return self.conn


    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Closing database connection")
        self.conn.close()
        return False
		
with DatabaseConnection() as db:
	db.execute("SELECT * FROM USERS")
```


A **context manager** in Python is a protocol (or design pattern) that enables **safe and automatic resource management**—ensuring that setup and cleanup logic are always executed, even if an error occurs.

It’s most commonly used with the **`with` statement**, which guarantees that resources like files, locks, network connections, or database transactions are properly acquired and released.

---

### 🔧 How It Works

To be a context manager, an object must implement two special methods:

1. **`__enter__(self)`**  
   - Called when entering the `with` block.
   - Typically acquires a resource (e.g., opens a file).
   - The return value is bound to the variable after `as`.

2. **`__exit__(self, exc_type, exc_value, traceback)`**  
   - Called when leaving the `with` block—**always**, even if an exception occurs.
   - Used to release/clean up the resource (e.g., close a file).
   - If it returns `True`, any exception that occurred inside the block is **suppressed**.

---

### 📁 Classic Example: File Handling

Without a context manager:
```python
f = open('data.txt', 'r')
try:
    content = f.read()
finally:
    f.close()  # Easy to forget!
```

With a context manager:
```python
with open('data.txt', 'r') as f:
    content = f.read()
# File is automatically closed here—even if an exception happened!
```

The file object returned by `open()` is a built-in context manager.

---

### 🛠️ Creating Your Own Context Manager

#### Option 1: Using a Class

```python
class DatabaseConnection:
    def __enter__(self):
        print("Opening database connection")
        self.conn = connect_to_db()  # pseudo-code
        return self.conn

    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Closing database connection")
        self.conn.close()
        # Return False (or nothing) to propagate exceptions
        return False

# Usage
with DatabaseConnection() as db:
    db.execute("SELECT * FROM users")
```

#### Option 2: Using `@contextmanager` Decorator (from `contextlib`)

This is more concise and uses a generator:

```python
from contextlib import contextmanager

@contextmanager
def database_connection():
    print("Opening connection")
    conn = connect_to_db()
    try:
        yield conn  # This is what gets assigned after `as`
    except Exception as e:
        print(f"Handling error: {e}")
        raise  # Re-raise or suppress by not raising
    finally:
        print("Closing connection")
        conn.close()

# Usage
with database_connection() as db:
    db.execute("SELECT 1")
```

> The code before `yield` = `__enter__`,  
> the code after `yield` (in `finally`) = `__exit__`.

---

### 💡 Common Use Cases

- **File operations** (`open`)
- **Thread locks** (`threading.Lock`)
- **Database transactions**
- **Temporary directories or files** (`tempfile.TemporaryDirectory`)
- **Timing code blocks** (custom timer context managers)
- **Changing and restoring global state** (e.g., locale, working directory)

Example: Timing execution
```python
import time
from contextlib import contextmanager

@contextmanager
def timer():
    start = time.time()
    yield
    print(f"Elapsed: {time.time() - start:.2f}s")

with timer():
    time.sleep(1)
# Output: Elapsed: 1.00s
```

---

### 🔗 Multiple Context Managers

You can combine them:
```python
with open('input.txt') as fin, open('output.txt', 'w') as fout:
    fout.write(fin.read())
```

Or use `contextlib.ExitStack` for dynamic numbers of context managers.

---

### ✅ Key Benefits

- **Automatic cleanup** — no resource leaks.
- **Exception safety** — cleanup runs even on errors.
- **Clean, readable code** — avoids `try/finally` boilerplate.
- **Composability** — context managers can be nested or combined.

---

### ⚠️ Important Notes

- `__exit__` receives exception info:  
  - If no exception: all three args are `None`.  
  - If exception occurred: `exc_type`, `exc_value`, `traceback` are set.
- Returning `True` from `__exit__` **suppresses the exception**.
- Never ignore exceptions silently unless intentional.

---

### 🔚 Summary

A **context manager** is Python’s elegant solution to the **"acquire-use-release"** pattern. By using the `with` statement, you write code that is **safer**, **cleaner**, and **more maintainable**—ensuring critical cleanup logic never gets skipped.

Whether you use built-in ones (`open`, `Lock`) or create your own (via class or `@contextmanager`), context managers are a cornerstone of **Pythonic** resource handling.
---
[[SQL]] [[CSV]]