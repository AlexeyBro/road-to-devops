# Linux

## Базовые команды

Выполнить предыдущую команду (обычно используется в связке с новой командой)

```bash
!!
```

Вывести данные в `stdout` (аналог `print`)

```bash
echo
```

---

## Команды навигации

Вывести текущую рабочую директорию

```bash
pwd
```

> `pwd` — *Print Working Directory*

Посмотреть содержимое директории

```bash
ls
```

> `ls` — *List*

Работает аналогично `ls`, но добавляет `/` к папкам

```bash
ls -F
```

Показать содержимое с подробной информацией

```bash
ls -l
```

Перейти в папку

```bash
cd
```

> `cd` — *Change Directory*

Вернуться в родительскую директорию

```bash
cd ..
```

Показать справку по команде

```bash
ls --help
```

Посмотреть дерево файлов

```bash
tree
```

---

## Работа с папками и файлами

Создать файл

```bash
touch {file_name}
```

Создать папку

```bash
mkdir {folder_name}
```

Скопировать файл

```bash
cp {file_name} {folder_name}/{copy_file_name}
```

Переместить или переименовать файл

```bash
mv {file_name} {folder_name}
```

Удалить файл

```bash
rm {file_name}
```

Удалить все файлы с определенным расширением

```bash
rm *.txt
```

Удалить все файлы в директории

```bash
rm *
```

Удалить папку вместе с содержимым

```bash
rm -rf {folder_name}
```

---

## Работа через `sudo`

`sudo` (*Super User Do*) позволяет выполнять команды с правами администратора.

Перейти в режим администратора

```bash
sudo su
```

или

```bash
sudo su {user_name}
```

Переключиться на другого пользователя

```bash
su {user_name}
```

Изменить владельца файла

```bash
sudo chown {user}:{group} {file_name}
```

> `chown` — *Change Owner*

Изменить права доступа

```bash
sudo chmod {permissions} {file_name}
```

> `chmod` — *Change Mode*

---

## Права доступа (`chmod`)

### Базовые права

| Код | Право | Обозначение |
|-----:|--------|-------------|
| 4 | Read | `r--` |
| 2 | Write | `-w-` |
| 1 | Execute | `--x` |

Права складываются:

| Код | Права |
|-----:|--------|
| 4+2 = 6 | `rw-` |
| 4+1 = 5 | `r-x` |
| 4+2+1 = 7 | `rwx` |

Права задаются для трех категорий пользователей:

1. Владелец (Owner)
2. Группа (Group)
3. Остальные пользователи (Others)

Пример:

```bash
sudo chmod 764 {file_name}
```

Расшифровка:

```
7 = rwx
6 = rw-
4 = r--
```

---

## Пакетный менеджер

Вызвать пакетный менеджер

```bash
apt-get
```

Установить программу

```bash
sudo apt-get install {program_name}
```

Удалить программу

```bash
sudo apt-get remove {program_name}
```

Найти пакет

```bash
apt-cache policy {program_name}
```

Обновить программу

```bash
sudo apt-get upgrade {program_name}
```

Обновить все установленные пакеты

```bash
sudo apt-get upgrade
```

---

## Поиск

Поиск файла по имени (с учетом регистра)

```bash
find . -type f -name "{file_name}"
```

Поиск файла без учета регистра

```bash
find . -type f -iname "{file_name}"
```

Поиск папки

```bash
find . -type d -name "{directory_name}"
```

Поиск с использованием шаблона

```bash
find . -type f -name "file.*"
```

Поиск по правам доступа

```bash
find . -type f -perm 0664
```

Поиск по размеру

Больше 10 МБ

```bash
find . -size +10M
```

Меньше 10 МБ

```bash
find . -size -10M
```

Найти все файлы, кроме указанного

```bash
find . -type f -not -name "{file_name}"
```

---

## Просмотр содержимого файла

```bash
cat {file_name}
```

---

## Поиск текста внутри файла (`grep`)

Поиск с учетом регистра

```bash
grep "{search_text}" {file_name}
```

Без учета регистра

```bash
grep -i "{search_text}" {file_name}
```

Показать номера строк

```bash
grep -n "{search_text}" {file_name}
```

---

## Выполнение дополнительной команды (`-exec`)

Выполнить команду для каждого найденного файла

```bash
find . -type f -name "{file_name}" -exec grep "{search_text}" {} \;
```

---

## Сортировка

Отсортировать текст

```bash
sort {file_name}
```

Отсортировать числа

```bash
sort -n {file_name}
```

Отсортировать числа в обратном порядке

```bash
sort -n -r {file_name}
```

Сохранить отсортированный результат в новый файл

```bash
sort {file_name} > {sorted_file_name}
```

---

## Мониторинг системы

Просмотр процессов в режиме реального времени

```bash
top
```

Просмотр использования памяти

```bash
free -h
```

Быстрый снимок процессов

```bash
ps
```

Подробный список процессов

```bash
ps aux
```

---

## Архивация

Создать архив

```bash
tar cf {archive_name}.tar {folder_name}
```

Посмотреть содержимое архива

```bash
tar tf {archive_name}.tar
```

Распаковать архив

```bash
tar xf {archive_name}.tar
```

Сжать архив

```bash
xz {archive_name}.tar
```

Распаковать архив `.xz`

```bash
unxz {archive_name}.tar.xz
```

Создать ZIP-архив

```bash
zip -r {archive_name}.zip {folder_name}
```

Распаковать ZIP

```bash
unzip {archive_name}.zip
```

---

## Текстовые редакторы

- `gedit`
- `nano`
- `pico`
- `vim`

---

## Скачать файл из сети

```bash
wget {file_url}
```

---

## Установка пакета

```bash
sudo dpkg -i {file_name}.deb
```

---

## Работа с сетью

Проверить доступность сайта

```bash
ping {url}
```

Отправить ограниченное количество пакетов

```bash
ping -c {count} {url}
```

Узнать IP-адрес домена

```bash
host {url}
```

Посмотреть сетевые соединения

```bash
netstat
```

Подключиться по SSH

```bash
ssh {user_name}@{server_ip}
```

---

## Перенаправление и конвейер

Перезаписать файл выводом команды

```bash
>
```

Добавить вывод в конец файла

```bash
>>
```

Передать вывод одной команды другой

```bash
|
```

Примеры:

```bash
echo "Hello" > file.txt
```

```bash
echo "World" >> file.txt
```

```bash
cat file.txt | grep Hello
```

---

# Bash Shell

Все команды и скрипты выполняются через **Shell**.

**Shell** — это программа-посредник между пользователем и операционной системой.

Популярные реализации Shell:

- Bash
- Zsh

### Что делает Shell

- принимает команды пользователя;
- разбирает их;
- запускает нужные программы;
- получает результат выполнения;
- выводит результат обратно в терминал.

Схема работы:

```
Пользователь
      │
      ▼
Терминал
      │
      ▼
Shell (bash/zsh)
      │
      ▼
Ядро Linux
      │
      ▼
Программы
```

---

## Bash-скрипты

Любой Bash-скрипт начинается с шебанга:

```bash
#!/bin/bash
```

Пример:

```bash
#!/bin/bash

echo "Hello"

mkdir test

cd test

touch file.txt
```

Запуск скрипта

```bash
bash {script_name}.sh
```

или после выдачи прав на выполнение

```bash
chmod +x {script_name}.sh
./{script_name}.sh
```
