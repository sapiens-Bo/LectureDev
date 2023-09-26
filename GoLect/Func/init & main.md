# init & main

**Точка входа в программировании** — ==*это место в программе, где начинается ее выполнение*==. Это может быть функция, метод, класс или любой другой элемент программы, который запускается первым. Точка входа является важным элементом программы, поскольку она определяет, как программа будет выполняться.

В языке программирования Golang точкой входа является **функция main**. Функция main должна быть определена в пакете main и иметь следующую сигнатуру:
```go
func main() {
	// код программы
}
```
Функция main выполняется автоматически при запуске программы на Golang. Она обязательна для каждой программы на Golang и должна быть определена только один раз в пакете main.

**Функция init** — это функция, которая выполняется до функции main в программе на Golang. Функция init может быть определена в любом пакете и иметь следующую сигнатуру:

```go
func init() {
	// код инициализации
}
```
==*Функция init выполняется автоматически при импорте пакета, в котором она определена*==. Если в пакете определено несколько функций init, то они будут выполнены в порядке их определения. Функция init ==*может использоваться для инициализации переменных, настройки параметров и выполнения других действий, которые необходимы до запуска основной программы*==.

Пример использования функции init в Golang

```go
package main

import "fmt"

func init() {
	fmt.Println("Инициализация переменных")
}

func main() {
	fmt.Println("Hello, world!")
}
```

---

Relation [[Функции]]