# Типы данных

## Числа

| Тип | Размер | Диапазон | Диапазон un- |
|----|----|----|----|
| int8 | 8 бит | `-128; 127` | `0; 255` |
| int16 | 16 бит | `-32 768; 32 767` | `0; 65 535` |
| int32 | 32 бита | `±2.1 млрд` | `0; 4.29 млрд` |
| int64 | 64 бита | очень много | тоже много |
| int | зависит от архитектуры |||

```go
var a int = 42
var b uint8 = 255
var c int64 = 1000000
```

### Руна и байты

```go
// src: go/src/builtin/builtin.go

// byte is an alias for uint8 and is equivalent to uint8 in all ways. It is
// used, by convention, to distinguish byte values from 8-bit unsigned
// integer values.
type byte = uint8

// rune is an alias for int32 and is equivalent to int32 in all ways. It is
// used, by convention, to distinguish character values from integer values.
type rune = int32
```

> Руна используется для Unicode/UTF-8. Байты - восьмибитные, для чисел

```go
data := []byte("hello")     // читается: «байты текста»
// vs
data := []uint8("hello")    // читается: «восьмибитные числа»

r := rune('A')
// vs
var x int32 = 'A'
```

## Числы с плавающей точкой

| Тип | Размер | Точность |
|----|----|----|
| float32 | 32 бита | 7 знаков |
| float64 | 64 бита | 15 знаков |

```go
var x float64 = 3.14
var y float32 = 2.5
```

## Логический тип

```go
var flag bool = true
var empty bool = false
```

## Строки

```go
s := "Привет, мир"
len(s)              // длина в БАЙТАХ (не символах!)
s[0]                // байт, не символ
```

- Строки неизменяемы

## Массивы

```go
var a [5]int              // [0 0 0 0 0]
b := [3]string{"a", "b", "c"}
c := [...]int{1, 2, 3, 4} // компилятор сам посчитает длину

len(a) // 5
```

- Массивы копируются при присваивании:

```go
x := [3]int{1, 2, 3}
y := x        // копия!
y[0] = 100
fmt.Println(x[0]) // 1
```

## Слайсы

```go
s := []int{1, 2, 3}
var empty []int             // nil-слайс
made := make([]int, 5)      // длина 5, все нули
made2 := make([]int, 0, 10) // длина 0, ёмкость 10
```

- Динамически, в отличии от массива

| Тип | Размер | Смысл |
|----|----|----|
| array | 8 байт | Указатель на первый элемент базового массива |
| len | 8 байт | Длина - сколько элементов доступно для чтения/записи |
| cap | 8 байт | Ёмкость - сколько элементов влезет без перевыделения памяти |

- `len` **`≤`** `cap` всегда.

## Мапы

```go
m := map[string]int{
    "apple":  5,
    "banana": 3,
}
m["cherry"] = 10
delete(m, "apple")

v := m["banana"]        // 3
v, ok := m["missing"]   // v=0, ok=false — проверка наличия
```

- `[string]int` значит - `ключ: строка - значение: число`
- `v, ok` - возвращают значение из массива, а `ok` призваивает `bool` наличия

## Struct

```go
type User struct {
    Name string
    Age  int
    Email string
}

u := User{Name: "Алиса", Age: 30}
u.Age = 31

p := &u          // указатель
p.Name = "Боб"   // авто-разыменование
```

### Встраивание

```go
type Animal struct {
    Name string
}

type Dog struct {
    Animal  // встроенное поле
    Breed string
}

d := Dog{Animal{"Рекс"}, "Лабрадор"}
fmt.Println(d.Name) // Рекс — доступ через embedding
```

## Указатели

```go
x := 42
p := &x       // p — *int
*p = 100      // разыменование - изменил перменную по адресу &x 
fmt.Println(x) // 100
```

## Интерфейс

```go
type Stringer interface {
    String() string
}

type Person struct{ Name string }

func (p Person) String() string {
    return "Person: " + p.Name
}

var s Stringer = Person{"Алиса"}
fmt.Println(s.String())
```

- Интерфейс — это набор методов. Не данные, не поля — только методы.
