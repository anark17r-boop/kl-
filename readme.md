# Kl+ Programming Language

**Kl+** — современный компилируемый язык программирования, сочетающий низкоуровневый контроль C/C++ с выразительностью высокоуровневых языков.

- **Версия:** 0.1.0
- **Платформы:** Windows.

---

## Установка

Проверка установки:
```bash
kl version
```
> Если `kl` не найдена, добавьте `C:\kl+\bin` в переменную `PATH`.

---

## Быстрый старт

Создайте файл `hello.kl`:
```
fn main() {
    println("Hello, World!");
}
```
Запустите программу:
```bash
kl run hello.kl
```

---

## 1. Переменные

### Неизменяемая (по умолчанию)
```
let x: i32 = 10;
```

### Изменяемая
```
let mut y: i32 = 20;
y = 30;
y += 10;
```

### Короткое объявление (автовывод типа)
```
z := 42;
name := "Alice";
```

### C-style объявление
```
int a = 100;
float b = 3.14;
string s = "Hello";
```

### Константы
```
const PI: f64 = 3.14159265359;
const MAX_SIZE: i32 = 1000;
```

### `var` — короткая изменяемая
```
var count = 0;
count += 1;
```

---

## 2. Типы данных

### Целые числа
| Тип      | Размер  | Диапазон                   |
|----------|---------|----------------------------|
| `i8`     | 1 байт  | -128 до 127                |
| `i16`    | 2 байта | -32768 до 32767             |
| `i32`/`int` | 4 байта | ±2 миллиарда                |
| `i64`    | 8 байт  | ±9 квинтиллионов            |
| `u8`     | 1 байт  | 0 до 255                    |
| `u16`    | 2 байта | 0 до 65535                  |
| `u32`    | 4 байта | 0 до 4 миллиардов           |
| `u64`    | 8 байт  | 0 до 18 квинтиллионов       |

### Числа с плавающей точкой
| Тип        | Размер  | Точность        |
|------------|---------|-----------------|
| `f32`      | 4 байта | ~7 цифр         |
| `f64`/`float` | 8 байт | ~15 цифр        |

### Другие типы
| Тип        | Описание                  |
|------------|---------------------------|
| `bool`     | `true` или `false`        |
| `char`     | Один символ `'A'`         |
| `str`/`string` | Строка `"Hello"`          |

### Литералы чисел
```
let decimal: i32 = 42;
let hex: i32 = 0xFF;
let binary: i32 = 0b1010;
let octal: i32 = 0o77;
let with_sep: i64 = 1_000_000;
let scientific: f64 = 3.14e-2;
```

---

## 3. Функции

### Базовая функция
```
fn add(a: i32, b: i32) -> i32 {
    return a + b;
}

fn main() {
    let result: i32 = add(5, 3);
    println("5 + 3 = %d", result);
}
```

### Без возвращаемого значения
```
fn greet(name: str) {
    println("Hello, %s!", name);
}
```

### Короткая форма
```
fn square(x: i32) -> i32 => x * x;
fn double(x: i32) -> i32 => x * 2;
```

### Значения по умолчанию
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

### Публичная функция
```
pub fn api_function() {
    // Доступна из других модулей
}
```

---

## 4. Операторы

### Арифметические
| Оператор | Описание   | Пример        |
|----------|------------|---------------|
| `+`      | Сложение   | `5 + 3 → 8`   |
| `-`      | Вычитание  | `5 - 3 → 2`   |
| `*`      | Умножение  | `5 * 3 → 15`  |
| `/`      | Деление    | `7 / 2 → 3`   |
| `%`      | Остаток    | `7 % 3 → 1`   |
| `**`     | Степень    | `2 ** 10 → 1024` |

```
fn main() {
    println("10 + 3 = %d", 10 + 3);
    println("10 - 3 = %d", 10 - 3);
    println("10 * 3 = %d", 10 * 3);
    println("10 / 3 = %d", 10 / 3);
}
```

### Сравнения
| Оператор | Описание       |
|----------|----------------|
| `==`     | Равно          |
| `!=`     | Не равно       |
| `<`      | Меньше         |
| `>`      | Больше         |
| `<=`     | Меньше или равно |
| `>=`     | Больше или равно |

```
fn main() {
    let a: i32 = 10;
    let b: i32 = 20;
    if a < b {
        println("a is less than b");
    }
}
```

### Логические
| Оператор | Описание |
|----------|----------|
| `&&`     | И        |
| `\|\|`   | ИЛИ      |
| `!`      | НЕ       |

```
fn main() {
    let age: i32 = 25;
    let has_license: bool = true;
    if age >= 18 && has_license {
        println("OK");
    }
}
```

### Побитовые
| Оператор | Описание     |
|----------|--------------|
| `&`      | AND          |
| `\|`     | OR           |
| `^`      | XOR          |
| `~`      | NOT          |
| `<<`     | Сдвиг влево  |
| `>>`     | Сдвиг вправо |

```
fn main() {
    let a: i32 = 0b1010;
    let b: i32 = 0b1100;
    println("a & b = %d", a & b);   // 8 (0b1000)
    println("a << 2 = %d", a << 2); // 40 (0b101000)
}
```

### Присваивание
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

### Инкремент и декремент
```
fn main() {
    let mut i: i32 = 0;
    i++;      // постфиксный
    ++i;      // префиксный
    i--;
    --i;
    println("i = %d", i);
}
```

### Тернарный оператор
```
fn main() {
    let age: i32 = 20;
    let status: str = age >= 18 ? "adult" : "minor";
    println("Status: %s", status);
}
```

---

## 5. Управляющие конструкции

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

### For (диапазон)
```
fn main() {
    // 0..10 (не включая 10)
    for i in 0..10 {
        println("%d", i);
    }
    
    // 1..=10 (включительно)
    for i in 1..=10 {
        println("%d", i);
    }
}
```

### For с шагом
```
fn main() {
    for i in 0..10 step 2 {
        println("%d", i);  // 0, 2, 4, 6, 8
    }
}
```

### For с фильтром
```
fn main() {
    for i in 0..20 where i % 2 == 0 {
        println("%d", i);  // чётные числа
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
        println("Not found");  // выполнится, если break не сработал
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

### Loop (бесконечный)
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

### Break и Continue
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

## 6. Структуры

### Объявление и использование
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

### Методы (impl)
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

## 8. Работа с памятью

### Выделение и освобождение
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

### Указатели
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

### sizeof и cast
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

### Unsafe блок
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

## 9. Встроенные функции

### Ввод/Вывод
| Функция          | Описание               |
|------------------|------------------------|
| `print("text")`  | Вывод без переноса     |
| `println("text")`| Вывод с переносом      |
| `input()`        | Ввод строки            |
| `input_int()`    | Ввод целого числа      |
| `input_float()`  | Ввод числа с плавающей точкой |

```
fn main() {
    print("Enter name: ");
    let name: str = input();
    print("Enter age: ");
    let age: i32 = input_int();
    println("Hello, %s! Age: %d", name, age);
}
```

### Математика
| Функция               | Описание                    |
|-----------------------|-----------------------------|
| `sqrt(x)`             | Квадратный корень           |
| `pow(base, exp)`      | Возведение в степень        |
| `abs(x)`              | Модуль (целые)              |
| `fabs(x)`             | Модуль (float)              |
| `floor(x)`, `ceil(x)` | Округление вниз/вверх       |
| `round(x)`            | Математическое округление   |
| `sin(x)`, `cos(x)`, `tan(x)` | Тригонометрия         |
| `log(x)`, `log10(x)`  | Логарифмы                   |
| `exp(x)`              | Экспонента                  |
| `min(a,b)`, `max(a,b)`| Минимум/максимум (целые)    |
| `fmin(a,b)`, `fmax(a,b)` | Минимум/максимум (float) |
| `clamp(x, lo, hi)`    | Ограничение значения        |

```
fn main() {
    println("sqrt(16) = %f", sqrt(16.0));
    println("pow(2, 10) = %f", pow(2.0, 10.0));
    println("abs(-42) = %d", abs(-42));
    println("clamp(15, 0, 10) = %d", clamp(15, 0, 10));  // 10
}
```

### Случайные числа
| Функция               | Описание                    |
|-----------------------|-----------------------------|
| `rand()`              | Случайное число (0..RAND_MAX) |
| `rand_range(min, max)`| Число в заданном диапазоне  |
| `srand(seed)`         | Установка seed              |

```
fn main() {
    srand(42);
    println("rand() = %d", rand());
    println("rand_range(1, 100) = %d", rand_range(1, 100));
}
```

### Строки
| Функция        | Описание                        |
|----------------|---------------------------------|
| `strlen(s)`    | Длина строки                    |
| `strcmp(a, b)` | Сравнение (0 = равны)           |

```
fn main() {
    let s: str = "Hello";
    println("Length: %d", strlen(s));
    
    if strcmp("abc", "abc") == 0 {
        println("Equal!");
    }
}
```

### Утилиты
| Функция             | Описание                    |
|---------------------|-----------------------------|
| `exit(code)`        | Выход из программы          |
| `assert(cond, msg)` | Проверка условия            |
| `sizeof(type)`      | Размер типа в байтах        |

---

## 10. Форматирование вывода

| Спецификатор | Тип       | Пример                  |
|--------------|-----------|-------------------------|
| `%d`         | `i32`     | `println("%d", 42)`     |
| `%lld`       | `i64`     | `println("%lld", 123456789)` |
| `%f`         | `f64`     | `println("%f", 3.14)`   |
| `%s`         | `str`     | `println("%s", "hello")`|
| `%c`         | `char`    | `println("%c", 65)`     |
| `%%`         | символ %  | `println("100%%")`      |

---

## 11. Команды CLI

```bash
kl build main.kl --console output.exe    # Компиляция консольного приложения
kl build main.kl --app output.exe        # Компиляция GUI приложения
kl run main.kl                           # Сборка и запуск
kl check main.kl                         # Проверка синтаксиса
kl tokens main.kl                        # Показать токены
kl version                               # Версия компилятора
kl help                                  # Справка
```

---

## 12. Примеры программ

### Числа Фибоначчи
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

### Простые числа
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

### Угадай число
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

### Калькулятор
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

### Шаблон консольной игры
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
```
скачать последнюю версию языка можно в Realese
```
