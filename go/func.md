# Функции

Базовый пример:

```go
func greet() {
    fmt.Println("Привет!")
}

greet()  // Привет!
```

## Параметры

```go
func greet(name string) {
    fmt.Println("Привет,", name)
}

greet("Алиса")  // Привет, Алиса
greet("Боб")    // Привет, Боб
```

Несколько параметров

```go
func add(a int, b int) int {
//      число,  число, ретурн тип
    return a + b
}

result := add(2, 3)  // 5
```

Группировка

```go
func add(a, b int) int {  // a и b — оба int
    return a + b
}
```

## Return type (`RT`)

```go
func add(a, b int) int {
    return a + b
}

result := add(2, 3)  // result = 5
```

Без возвращаемого типа:

```go
func greet(name string) {
    fmt.Println("Привет,", name)
    // нет return - ничего не возвращает
}
```

## Multi RT

- Можно возвращать сразу несколько типов

```go
func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, fmt.Errorf("деление на ноль")
    }
    return a / b, nil
}

result, err := divide(10, 2)
if err != nil {
    fmt.Println("Ошибка:", err)
    return
}
fmt.Println(result)  // 5

result, err := divide(10, 0)
if err != nil {
    fmt.Println("Ошибка:", err) // деление на ноль
    return 
}
```

## Вариативные функции

```go
func sum(nums ...int) int {
    total := 0
    for _, n := range nums {
        total += n
    }
    return total
}

sum(1, 2, 3)       // 6
sum()              // 0
sum(1, 2, 3, 4, 5) // 15
```

- `nums ...int` — `nums` это слайс `[]int`

## Анонимные функции

```go
func() {
    fmt.Println("Анонимная функция")
}()  // сразу вызывается

func(name string) {
    fmt.Println("Привет,", name)
}("Алиса")
```