# Тестирование функции `main`
---

Функция `main` может быть протестирована с помощью пакета `testing`. Для тестирования функции `main` с `os.Stdout, os.Stderr, os.Stdin, os.Args` мы можем использовать пакет `os`.

- `os.Stdout` — это переменная, которая представляет стандартный вывод в операционной системе.

- `os.Stderr` — это переменная, которая представляет стандартный вывод ошибок в операционной системе.

- `os.Stdin` — это переменная, которая представляет стандартный ввод в операционной системе.

- `os.Args` — это переменная, которая представляет аргументы командной строки в операционной системе.

Для тестирования функции `main` с `os.Stdout` и `os.Stderr` мы можем использовать функцию `os.Pipe()` из пакета `os`. Эти методы позволяют ==перенаправить вывод из функции main в буфер==, который может быть прочитан в тесте.

### Пример 1
---
В этом примере мы тестируем функцию main, которая выводит результат в стандартный поток вывода. Мы используем переменную os.Stdout для перехвата вывода и сравнения его с ожидаемым результатом.

```go
func TestMainFunc(t *testing.T) {
    old := os.Stdout
    r, w, _ := os.Pipe()
    os.Stdout = w

    main()

    w.Close()
    os.Stdout = old

    var stdout bytes.Buffer
    stdout.ReadFrom(r)

    expected := "expected output"
    if stdout.String() != expected {
        t.Errorf("got %q, want %q", stdout.String(), expected)
    }
}
```

Здесь мы сохраняем старое значение переменной os.Stdout, создаем канал для перехвата вывода, устанавливаем его в качестве стандартного потока вывода, вызываем функцию main, считываем вывод из канала и сравниваем его с ожидаемым результатом.

### Пример 2
---
В этом примере мы тестируем функцию main, которая читает данные из стандартного потока ввода и записывает результат в стандартный поток вывода. Мы используем переменные os.Stdin и os.Stdout для перехвата ввода и вывода и сравнения их с ожидаемым результатом.

```go
func TestMainFunc(t *testing.T) {
    oldStdin := os.Stdin
    oldStdout := os.Stdout

    r, w, _ := os.Pipe()
    os.Stdin = r
    os.Stdout = w

    input := "input data"
    go func() {
        defer w.Close()
        fmt.Fprint(w, input)
    }()

    main()

    w.Close()
    os.Stdin = oldStdin
    os.Stdout = oldStdout

    var stdout bytes.Buffer
    stdout.ReadFrom(r)

    expected := "expected output"
    if stdout.String() != expected {
        t.Errorf("got %q, want %q", stdout.String(), expected)
    }
}
```

Здесь мы сохраняем старые значения переменных os.Stdin и os.Stdout, создаем буфер для перехвата ввода и вывода, записываем данные в канал ввода, вызываем функцию main, считываем вывод из канала и сравниваем его с ожидаемым результатом.