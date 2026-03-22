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
