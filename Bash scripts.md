# Linux

# Bash Scripts

## Shebang

Каждый Bash-скрипт рекомендуется начинать с **shebang** — строки, которая сообщает операционной системе, каким интерпретатором выполнять скрипт.

```bash
#!/bin/bash
```

---

## Переменные

### Числовые переменные

```bash
number=123
```

### Строковые переменные

```bash
string="Hello"
```

### Сохранить результат выполнения команды

```bash
command=$(ls)
```

> Современный синтаксис — `$(...)`. Старый вариант с обратными кавычками `` `...` `` также работает, но считается устаревшим.

### Вывести значения переменных

```bash
echo "$string $number $command"
```

---

## Зарезервированные переменные

Название операционной системы

```bash
uname -a
```

Имя текущего Bash-скрипта

```bash
echo "$0"
```

Количество переданных аргументов

```bash
echo "$#"
```

Все аргументы

```bash
echo "$@"
```

Код завершения предыдущей команды

```bash
echo "$?"
```

Идентификатор текущего процесса (PID)

```bash
echo "$$"
```

---

## Ввод данных

### Через аргументы командной строки

Первые девять аргументов доступны через:

```bash
$1
$2
...
$9
```

Начиная с десятого аргумента необходимо использовать фигурные скобки:

```bash
${10}
${11}
...
```

Пример:

```bash
#!/bin/bash

echo "First argument: $1"
echo "Second argument: $2"
echo "Tenth argument: ${10}"
```

Запуск:

```bash
bash script.sh one two three four five six seven eight nine ten
```

---

### С помощью `read`

Все введенные пользователем данные сохраняются в специальную переменную `REPLY`.

```bash
read

echo "$REPLY"
```

---

### Сохранить ввод в указанную переменную

```bash
read number

echo "$number"
```

Пример:

```bash
echo "Enter number:"
read number

echo "$number"
```

---

### Использование флага `-p` (Prompt)

Позволяет вывести приглашение перед вводом.

```bash
read -p "Enter number: " number

echo "$number"
```

Эквивалентно:

```bash
echo "Enter number:"
read number

echo "$number"
```

---

## Арифметика

В Bash арифметические выражения вычисляются с помощью конструкции `$(())`.

```bash
a=10
b=20

result=$((a+b))

echo "$result"
```

Основные операции:

```bash
$((a+b))   # сложение
$((a-b))   # вычитание
$((a*b))   # умножение
$((a/b))   # деление
$((a%2))   # остаток от деления
```

---

## Условия

### Простое условие

```bash
if [ condition ]; then
    # действия
else
    # действия
fi
```

Пример:

```bash
number=10

if [ "$number" -gt 5 ]; then
    echo "Greater than 5"
else
    echo "Less or equal 5"
fi
```

---

### Несколько условий

```bash
if [ condition ]; then
    # действия
elif [ condition ]; then
    # действия
else
    # действия
fi
```

Пример:

```bash
number=10

if [ "$number" -lt 5 ]; then
    echo "Less than 5"
elif [ "$number" -eq 10 ]; then
    echo "Equals 10"
else
    echo "Other value"
fi
```

---

### Виды условий

#### Базовый синтаксис

```bash
[ condition ]
```

Например:

```bash
if [ "$a" -eq "$b" ]; then
```

---

#### Расширенный синтаксис

```bash
[[ condition ]]
```

Преимущества:

- поддерживает логические операторы `&&` и `||`;
- безопаснее при работе со строками;
- удобнее использовать регулярные выражения.

Пример:

```bash
if [[ $name == "Alex" ]]; then
    echo "Hello"
fi
```

---

#### Арифметические условия

```bash
(( condition ))
```

Используется для работы с числами.

Пример:

```bash
if (( a > b )); then
    echo "a > b"
fi
```

---

## Циклы

### Цикл `for`

Перебор списка значений.

```bash
for item in one two three; do
    echo "$item"
done
```

---

Перебор диапазона чисел

```bash
for i in {1..5}; do
    echo "$i"
done
```

---

Перебор файлов

```bash
for file in *.txt; do
    echo "$file"
done
```

---

### Цикл `while`

Выполняется, пока условие истинно.

```bash
count=1

while [ "$count" -le 5 ]; do
    echo "$count"
    ((count++))
done
```

---

### Цикл `until`

Выполняется, пока условие ложно.

```bash
count=1

until [ "$count" -gt 5 ]; do
    echo "$count"
    ((count++))
done
```

---

## Функции

### Объявление функции

```bash
function hello() {
    echo "Hello!"
}
```

или более короткий вариант

```bash
hello() {
    echo "Hello!"
}
```

---

### Вызов функции

```bash
hello
```

---

### Функция с параметрами

```bash
sum() {
    local result=$(($1 + $2))
    echo "$result"
}

sum 10 20
```

---

### Возврат значения через `echo`

В Bash функции обычно возвращают данные через `echo`.

```bash
get_name() {
    echo "Alex"
}

name=$(get_name)

echo "$name"
```

---

### Код завершения функции (`return`)

Команда `return` возвращает только числовой код завершения (от `0` до `255`).

```bash
check_number() {
    if (( $1 > 0 )); then
        return 0
    fi

    return 1
}

check_number 10

echo $?
```

> `0` означает успешное выполнение, любое ненулевое значение — наличие ошибки или иного результата выполнения.
