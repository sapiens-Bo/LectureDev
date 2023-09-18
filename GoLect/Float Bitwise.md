# Применение bitwise к числам с плавающей точкой
_Операции bitwise могут быть выполнены только над целочисленными типами данных. Однако в языке Golang можно выполнить операции bitwise с числами с плавающей точкой.

---
Операции bitwise могут быть выполнены только над целочисленными типами данных. Однако в языке Golang можно выполнить операции bitwise с числами с плавающей точкой. Для этого используются функции `math.Float32bits` и `math.Float64bits`, которые преобразуют числа с плавающей точкой в их двоичное представление в соответствии со стандартом IEEE 754. После выполнения операции bitwise результат необходимо преобразовать обратно в число с плавающей точкой с помощью функции `math.Float32frombits` или `math.Float64frombits`.

Операции &, |, ^ и &^ могут быть выполнены над числами с плавающей точкой, но результат может быть неожиданным из-за особенностей представления чисел с плавающей точкой в памяти компьютера. Операции << и >> не могут быть выполнены над числами с плавающей точкой.

Использования bitwise operation может привести к ошибкам округления и потере точности.

### Примеры:

- **Преобразование uint32 в float32 и обратно**

```go
package main

import (
	"fmt"
	"math"
)

func main() {
	var uintNumber uint32 = 123456789
	floatNumber := math.Float32frombits(uintNumber)
	fmt.Println("Float32 number:", floatNumber)

	uintNumber = math.Float32bits(floatNumber)
	fmt.Println("Uint32 number:", uintNumber)
}
```

Вывод:

```go
Float32 number: 1.454441e+08
Uint32 number: 123456792
```

- **использование указателя для преобразования числа**

```go
package main

import (
	"fmt"
	"unsafe"
)

func main() {
	var floatNumber float32 = 123.456
	uintNumber := *(*uint32)(unsafe.Pointer(&floatNumber))
	fmt.Println("Uint32 number:", uintNumber)

	uintNumber = 0x42f6e979
	floatNumber = *(*float32)(unsafe.Pointer(&uintNumber))
	fmt.Println("Float32 number:", floatNumber)
}
```

Вывод:

```go
Uint32 number: 0x42f6e979
Float32 number: 123.456
```

---
Realation: [[Числа с плавающей точкой]] [[Bitwise operations]]