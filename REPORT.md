## Лабораторная работа 5
### Выполнила Заботкина Марина Александровна K3139
### Ход работы
### Задание 1
1) С помощью следующих команд переходим в скрытую папку Hooks:
```
cd git-practice
cd .git/hooks
```
2) Через текстовый редактор nano создаем файл pre-commit, где будет написан скрипт для проверки коммитов:
```
#!/bin/bash

for file in $(git diff --cached --name-only); do
    if [[ $file == *.txt ]]; then
        if grep -q "Автор:" "$file"; then
            echo "Файл $file соответствует формату и имеет подпись автора."
        else
            echo "Ошибка: Файл $file соответствует формату, но не имеет подписи>
            exit 1
        fi
    else
        echo "Ошибка: Файл $file не соответствует формату!"
        exit 1
    fi
done

exit 0
```
Если файл формата .txt, то начнётся проверка на наличие подписи автора в файле: если подпись в виде Автор: *** имеется, то произойдёт коммит и появится сообщние в консоли, если подписи нет, то коммит прервётся и появится соответствующее собщение в консоли. Если формат файла не .txt, то коммит опять же прервётся и появится сообщение.

3) Возвращаемся в папку репозитория и пишем команды:
```
git add commit_test.txt
git commit -m "Проверка файла"
git push origin main
```
![Снимок экрана 2024-12-01 000449](https://github.com/user-attachments/assets/d08a433c-45d0-4661-83e2-59e3fdb901ba)
![Снимок экрана 2024-12-01 001007](https://github.com/user-attachments/assets/614db718-cb31-4a80-951e-b7bf28c594a0)
![Снимок экрана 2024-12-01 010447](https://github.com/user-attachments/assets/0afacf80-5849-4f7b-be75-2ad67caefc54)

### Задание 2
1. Устанавливаем Git Flow и инициализируем его с помощью данных команд:
```
sudo apt-get install git-flow
git flow init
```
2. Создадим ветку для новой функциональности:
```
git flow feature start task-management
```
3. Создаём файл task_manager.py и напишем какой-нибудь простой скрипт:
```
import random

def create_task(title, description):
    a = random.randint(1, 10)
    b = random.randint(1, 10)
    equation = f"{a}x + {b} = {a + b}"
    print(f"Создана новая задача: {equation}")
```
4. Закоммитим изменения:
```
git add task_manager.py
git commit -m "Добавлен функционал управления задачами"
```
5. После завершения разработки функции завершим фичу и объединим ее с основной веткой:
```
git flow feature finish task-management
```
6. Переключимся на ветку "develop" и начнем создание релиза:
```
git checkout develop
git flow release start v1.0.0
```
7. Внесем изменения, связанные с релизом, например создадим файл version.txt и запишем туда что-нибудь, далее закоммитим наши изменения:
```
echo "v1.0.0" > version.txt
git add version.txt
git commit -m "Обновлена версия для релиза v1.0.0"
```
8. Завершим релиз и объединим его с ветками "develop" и "main":
```
git flow release finish v1.0.0
```
9. Если в процессе использования выявлена критическая ошибка, нужно создать hotfix (у нас нет никакой ошибки, но hotfix все равно создаем, чтобы сымитировать ошибку):
```
git flow hotfix start hotfix-1.0.1
```
10. Создадим новый файл file_with_error.py и запишем туда "исправленный" код:
```
import random

def create_task(title, description):
    a = random.randint(1, 10)
    b = random.randint(1, 10)
    equation = f"{a}x + {b} = {a + b}"
    print("Исправлена критическая ошибка")
```
11. Закоммитим изменения:
```
git add file_with_error.py
git commit -m "Исправлена критическая ошибка"
```
12. Завершим hotfix и объединим его с ветками "develop" и "main":
```
git flow hotfix finish hotfix-1.0.1
```
13. Отправим изменения на удаленный репозиторий:
```
git push origin develop
git push origin main
```
В итоге мы имеем следующие коммиты:
![image](https://github.com/user-attachments/assets/5529bff9-6592-4ab0-8bb7-dd8ea3fe9f15)

**Вывод:** 
Был создан репозиторий и клонирован на локальную машину, была реализована автоматизация проверки формата файлов при коммите, а также сымитировано использование Git Flow.

