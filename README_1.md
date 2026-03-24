# Отчет по лабораторной работе №2
## Изучение систем контроля версий на примере Git

### Цель работы
Изучить основные возможности системы контроля версий Git, научиться создавать репозитории, работать с удаленными репозиториями на GitHub, освоить базовые операции Git.

### Ход выполнения работы

#### 1. Подготовка рабочего окружения

**1.1 Установка переменных окружения**
```bash
export GITHUB_USERNAME="qwepyhbvc"
export GITHUB_EMAIL="wowtt894@gmail.com"
export GITHUB_TOKEN="ghp_xxxxxxxxxxxx"  # сгенерированный токен
```

**1.2 Настройка конфигурации hub**
Создан конфигурационный файл `~/.config/hub` для автоматической аутентификации:
```yaml
github.com:
- user: qwepyhbvc
  oauth_token: ghp_xxxxxxxxxxxx
  protocol: https
```

**1.3 Настройка Git**
```bash
git config --global user.name "qwepyhbvc"
git config --global user.email "wowtt894@gmail.com"
git config --global hub.protocol https
```

#### 2. Создание и настройка репозитория

**2.1 Создание репозитория на GitHub**
- Создан публичный репозиторий с именем `lab02`
- Добавлена лицензия MIT
- Добавлен файл `.gitignore` с содержимым:
```
*build*/
*install*/
*.swp
.idea/
```

**2.2 Инициализация локального репозитория**
```bash
mkdir -p projects/lab02 && cd projects/lab02
git init
git remote add origin https://github.com/qwepyhbvc/lab02.git
```

#### 3. Создание структуры проекта

Создана следующая структура директорий и файлов:

```
lab02/
├── README.md
├── .gitignore
├── LICENSE
├── sources/
│   └── print.cpp
├── include/
│   └── print.hpp
└── examples/
    ├── example1.cpp
    └── example2.cpp
```

**3.1 Реализация библиотеки print**

*include/print.hpp* - заголовочный файл:
```cpp
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
```

*sources/print.cpp* - реализация:
```cpp
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
```

**3.2 Примеры использования**

*examples/example1.cpp* - вывод в консоль:
```cpp
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
```

*examples/example2.cpp* - вывод в файл:
```cpp
#include <print.hpp>
#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
```

#### 4. Работа с Git

**4.1 Основные операции**
```bash
# Проверка статуса
git status

# Добавление файлов
git add README.md
git add .
git add sources/ include/ examples/

# Создание коммитов
git commit -m "added README.md"
git commit -m "added sources"

# Просмотр истории
git log --oneline
```

**4.2 Результаты коммитов**
```
abc1234 added sources
def5678 added README.md
```

**4.3 Отправка на удаленный репозиторий**
```bash
git push origin master
```

----------------------------------------------------------------------------------------------------------------

#### 5. Решение возникших проблем

В процессе работы возникли следующие проблемы и способы их решения:

**Проблема 1:** Ошибка "Repository not found" при выполнении `git pull`
- **Причина:** Неправильный URL репозитория
- **Решение:** Исправлен URL с помощью `git remote set-url`

**Проблема 2:** Ошибка "remote origin already exists"
- **Причина:** Удаленный репозиторий уже был добавлен
- **Решение:** Использована команда `git remote set-url` вместо `git remote add`

**Проблема 3:** Ошибка "couldn't find remote ref master"
- **Причина:** Отсутствие коммитов в локальном репозитории
- **Решение:** Создан начальный коммит перед выполнением push

**Проблема 4:** Аутентификация на GitHub
- **Причина:** Требуется ввод пароля при каждом взаимодействии
- **Решение:** Настроена аутентификация через токен в URL репозитория

#### 6. Создание отчета

```bash
# Клонирование шаблона отчета
cd ~/workspace/
export LAB_NUMBER=02
git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}

# Создание отчета
mkdir -p reports/lab${LAB_NUMBER}
cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
cd reports/lab${LAB_NUMBER}
edit REPORT.md
```

----------------------------------------------------------------------------------------------------------------

### Результаты работы

1. **Создан публичный репозиторий:** https://github.com/qwepyhbvc/lab02
2. **Настроена автоматическая аутентификация** через токен GitHub
3. **Создана библиотека print** с поддержкой вывода в консоль и файл
4. **Написаны примеры использования** библиотеки
5. **Освоены основные команды Git:**
   - `git init` - инициализация репозитория
   - `git add` - добавление файлов
   - `git commit` - фиксация изменений
   - `git push` / `git pull` - синхронизация с удаленным репозиторием
   - `git log` - просмотр истории
   - `git status` - проверка состояния
   - `git remote` - управление удаленными репозиториями

### Выводы

В ходе выполнения лабораторной работы были изучены основные возможности системы контроля версий Git:

1. **Управление версиями** - возможность отслеживать изменения кода, возвращаться к предыдущим версиям
2. **Распределенная разработка** - каждый разработчик имеет полную копию репозитория
3. **Ветвление** - возможность параллельной разработки новых функций
4. **Интеграция с GitHub** - удобный хостинг репозиториев с дополнительными функциями

Полученные навыки являются основой для профессиональной разработки программного обеспечения, позволяя эффективно работать в команде, отслеживать изменения и управлять версиями кода.

### Ссылки

- Репозиторий: https://github.com/qwepyhbvc/lab02
- Официальный сайт Git: https://git-scm.com
- Документация GitHub: https://docs.github.com

----------------------------------------------------------------------------------------------------------------
## Инструкция по отправке отчета

1. Сохраните этот отчет в файл `REPORT.md`
2. Создайте Gist на GitHub с содержимым отчета:
   - Перейдите на https://gist.github.com
   - Вставьте содержимое отчета
   - Назовите файл `lab02_report.md`
   - Нажмите "Create public gist"
3. Скопируйте ссылку на Gist
4. Отправьте ссылку личным сообщением в Slack

**Альтернативный способ через командную строку:**
```bash
# Если установлен gh (GitHub CLI)
gh gist create REPORT.md --public --desc "Lab02 Report"

# Или через curl
curl -X POST \
  -H "Authorization: token ${GITHUB_TOKEN}" \
  -d '{"description":"Lab02 Report","public":true,"files":{"lab02_report.md":{"content":"'"$(cat REPORT.md)"'"}}}' \
  https://api.github.com/gists
```
----------------------------------------------------------------------------------------------------------------

## **Part I: Основы Git и Hello World**

### Шаг 1: Создание пустого репозитория на GitHub

```bash
# Создайте репозиторий через веб-интерфейс
# Название: hello-world (или любое другое)
# Без README, .gitignore, лицензии (пустой)

# Или через командную строку (если установлен gh)
gh repo create hello-world --public --description "Hello World C++ project" --confirm
```

### Шаг 2: Клонирование и первый коммит

```bash
# Перейдите в рабочую директорию
cd ~/wowtt/workspace/projects

# Клонируйте репозиторий
git clone https://github.com/qwepyhbvc/hello-world.git
cd hello-world

# Создайте файл hello_world.cpp с плохим стилем кода
cat > hello_world.cpp <<EOF
#include <iostream>
using namespace std;

int main()
{
    cout << "Hello world!" << endl;
    return 0;
}
EOF

# Проверьте статус
git status

# Добавьте файл
git add hello_world.cpp

# Закоммитьте
git commit -m "Initial commit: add hello_world.cpp with poor coding style"

# Отправьте на GitHub
git push origin master
```

### Шаг 3: Модификация программы

```bash
# Измените программу для ввода имени пользователя
cat > hello_world.cpp <<EOF
#include <iostream>
using namespace std;

int main()
{
    string name;
    cout << "Enter your name: ";
    cin >> name;
    cout << "Hello world from " << name << "!" << endl;
    return 0;
}
EOF

# Проверьте изменения
git diff

# Закоммитьте (git add не нужен, если файл уже отслеживается)
git commit -am "Add user input functionality"

# Отправьте изменения
git push origin master
```

**Почему не надо добавлять файл повторно git add?**
Файл `hello_world.cpp` уже отслеживается Git (был добавлен в предыдущем коммите). Флаг `-a` в команде `git commit -am` автоматически добавляет все измененные отслеживаемые файлы. Это эквивалентно `git add hello_world.cpp && git commit -m "..."`.

### Шаг 4: Проверка истории

```bash
# Просмотр истории коммитов
git log --oneline --graph --all

# Проверьте удаленный репозиторий в браузере
# https://github.com/qwepyhbvc/hello-world
```

---

## **Part II: Ветвление и Pull Requests**

### Шаг 1: Создание ветки patch1

```bash
# Создайте и переключитесь на ветку patch1
git checkout -b patch1

# Проверьте текущую ветку
git branch
```

### Шаг 2: Исправление стиля кода

```bash
# Отредактируйте файл, убрав using namespace std;
cat > hello_world.cpp <<EOF
#include <iostream>
#include <string>

int main()
{
    std::string name;
    std::cout << "Enter your name: ";
    std::cin >> name;
    std::cout << "Hello world from " << name << "!" << std::endl;
    return 0;
}
EOF

# Проверьте изменения
git diff

# Закоммитьте
git commit -am "Fix code style: remove using namespace std"

# Отправьте ветку в удаленный репозиторий
git push origin patch1
```

### Шаг 3: Создание Pull Request

```bash
# Через командную строку (если установлен gh)
gh pr create --base master --head patch1 --title "Fix code style" --body "Remove using namespace std and add std:: prefix"

# Или создайте через веб-интерфейс GitHub
# Перейдите на страницу репозитория -> Pull requests -> New pull request
# base: master, compare: patch1
```

### Шаг 4: Добавление комментариев

```bash
# Убедитесь, что вы в ветке patch1
git checkout patch1

# Добавьте комментарии в код
cat > hello_world.cpp <<EOF
#include <iostream>
#include <string>

// Main function: entry point of the program
int main()
{
    // Variable to store user name
    std::string name;
    
    // Prompt user for input
    std::cout << "Enter your name: ";
    std::cin >> name;
    
    // Output greeting message
    std::cout << "Hello world from " << name << "!" << std::endl;
    
    return 0; // Successful execution
}
EOF

# Закоммитьте и отправьте
git commit -am "Add comments to code"
git push origin patch1
```

**Проверьте:** Новые изменения автоматически появятся в существующем PR.

### Шаг 5: Слияние PR и очистка

```bash
# Выполните слияние через веб-интерфейс GitHub
# Нажмите "Merge pull request" и подтвердите

# Или через командную строку
gh pr merge patch1 --merge --delete-branch

# Локально получите изменения
git checkout master
git pull origin master

# Просмотрите историю
git log --oneline --graph --all

# Удалите локальную ветку
git branch -d patch1

# Проверьте, что ветка удалена
git branch
```

---

## **Part III: Конфликты и rebase**

### Шаг 1: Создание ветки patch2

```bash
# Создайте новую ветку от master
git checkout -b patch2

# Проверьте текущую версию кода
cat hello_world.cpp
```

### Шаг 2: Применение clang-format

```bash
# Установите clang-format если не установлен
# Для Ubuntu/Debian:
sudo apt-get install clang-format

# Примените форматирование в стиле Mozilla
clang-format -style=Mozilla -i hello_world.cpp

# Проверьте изменения
git diff

# Закоммитьте
git commit -am "Apply clang-format with Mozilla style"

# Отправьте в удаленный репозиторий
git push origin patch2

# Создайте pull request
gh pr create --base master --head patch2 --title "Apply clang-format" --body "Format code using Mozilla style"
```

### Шаг 3: Создание конфликта

```bash
# Переключитесь на master
git checkout master

# Измените комментарии (создаст конфликт)
cat > hello_world.cpp <<EOF
#include <iostream>
#include <string>

// Основная функция: точка входа в программу
int main()
{
    // Переменная для хранения имени пользователя
    std::string name;
    
    // Запрос ввода от пользователя
    std::cout << "Enter your name: ";
    std::cin >> name;
    
    // Вывод приветствия
    std::cout << "Hello world from " << name << "!" << std::endl;
    
    return 0; // Успешное выполнение
}
EOF

# Закоммитьте и отправьте
git commit -am "Translate comments to Russian"
git push origin master
```

Теперь в PR patch2 -> master возникнут конфликты, так как обе ветки изменили одни и те же строки (комментарии).

### Шаг 4: Разрешение конфликтов через rebase

```bash
# Переключитесь на ветку patch2
git checkout patch2

# Получите последние изменения из master
git fetch origin

# Выполните rebase на master
git rebase origin/master
```

**Если возникли конфликты:**

```bash
# Просмотрите конфликтующие файлы
git status

# Отредактируйте hello_world.cpp, разрешив конфликты
# В файле будут маркеры:
# <<<<<<< HEAD
# ... версия из master
# =======
# ... версия из patch2
# >>>>>>> patch2

# Отредактируйте файл, оставив нужные изменения
cat > hello_world.cpp <<EOF
#include <iostream>
#include <string>

// Main function: entry point of the program
// Основная функция: точка входа в программу
int main()
{
    // Variable to store user name
    // Переменная для хранения имени пользователя
    std::string name;
    
    // Prompt user for input
    // Запрос ввода от пользователя
    std::cout << "Enter your name: ";
    std::cin >> name;
    
    // Output greeting message
    // Вывод приветствия
    std::cout << "Hello world from " << name << "!" << std::endl;
    
    return 0; // Successful execution / Успешное выполнение
}
EOF

# Добавьте разрешенный файл
git add hello_world.cpp

# Продолжите rebase
git rebase --continue

# Если нужно пропустить или прервать:
# git rebase --skip
# git rebase --abort
```

### Шаг 5: Force push и завершение

```bash
# После успешного rebase, сделайте force push
git push origin patch2 --force-with-lease

# Проверьте, что конфликты в PR исчезли
# Откройте PR в браузере - должно быть "Ready to merge"

# Выполните слияние PR
gh pr merge patch2 --merge --delete-branch

# Или через веб-интерфейс GitHub

# Локально обновите master
git checkout master
git pull origin master

# Удалите локальную ветку
git branch -d patch2

# Просмотрите финальную историю
git log --oneline --graph --all
```

---

## **Объяснение ключевых концепций**

### **1. Почему git add не нужен после изменения файла?**
```bash
# Вместо
git add hello_world.cpp
git commit -m "message"

# Можно использовать
git commit -am "message"  # -a = --all
```
Флаг `-a` автоматически добавляет все измененные *отслеживаемые* файлы.

### **2. Разница между merge и rebase**

**Merge:**
```bash
git checkout master
git merge patch2
# Создает merge commit, сохраняя историю веток
```

**Rebase:**
```bash
git checkout patch2
git rebase master
# Переписывает историю, делая ее линейной
# Требует force push
```

### **3. Force push с --force-with-lease**
```bash
git push origin patch2 --force-with-lease
```
Более безопасная версия force push - проверяет, что никто не обновил ветку.

### **4. Pull Request workflow**
1. Создать ветку
2. Внести изменения
3. Push ветку
4. Создать PR
5. Обсуждение/исправления
6. Merge
7. Удалить ветку

### **5. Разрешение конфликтов**
Конфликты возникают, когда разные ветки меняют одни и те же строки:
- Маркеры `<<<<<<<`, `=======`, `>>>>>>>` показывают конфликтующие версии
- Нужно вручную выбрать правильный код
- После разрешения: `git add` → `git rebase --continue` или `git commit`

---

## **Проверка результатов**

```bash
# Просмотр всей истории
git log --oneline --graph --all

# Должны увидеть:
# * merge commit (patch2 -> master)
# |\
# | * patch2 changes
# * | master changes (Russian comments)
# |/
# * patch1 changes
# * user input feature
# * initial commit

# Проверка удаленного репозитория
git remote -v
git branch -r
```

## **Итоговые команды для быстрого выполнения**

Если нужно быстро выполнить все шаги:

```bash
# Part I
git clone https://github.com/qwepyhbvc/hello-world.git
cd hello-world
echo -e "#include <iostream>\nusing namespace std;\n\nint main()\n{\n    cout << \"Hello world!\" << endl;\n    return 0;\n}" > hello_world.cpp
git add hello_world.cpp
git commit -m "Initial commit: add hello_world.cpp"
git push origin master

# Part II
git checkout -b patch1
echo -e "#include <iostream>\n#include <string>\n\nint main()\n{\n    std::string name;\n    std::cout << \"Enter your name: \";\n    std::cin >> name;\n    std::cout << \"Hello world from \" << name << \"!\" << std::endl;\n    return 0;\n}" > hello_world.cpp
git commit -am "Fix code style"
git push origin patch1
# Создать PR через веб-интерфейс
git checkout master
git pull origin master
git branch -d patch1

# Part III
git checkout -b patch2
clang-format -style=Mozilla -i hello_world.cpp
git commit -am "Apply clang-format"
git push origin patch2
# Создать PR
git checkout master
echo -e "#include <iostream>\n#include <string>\n\n// Основная функция\nint main()\n{\n    std::string name;\n    std::cout << \"Enter your name: \";\n    std::cin >> name;\n    std::cout << \"Hello world from \" << name << \"!\" << std::endl;\n    return 0;\n}" > hello_world.cpp
git commit -am "Translate comments"
git push origin master
# Разрешить конфликты через rebase
```
