Вот готовый файл `README.md`, который объясняет весь процесс решения задачи.

Вы можете скопировать этот текст и сохранить как `README.md` в папке `DataProject` или отдельно.

```markdown
# DataProject: Управление версиями с Git (CLI + Visual Studio)

## Описание проекта

Этот проект демонстрирует полный рабочий процесс управления версиями с использованием Git и Visual Studio.

**Цель:** Создать локальный репозиторий, выполнить изменения в коде, объединить коммиты через **интерактивный ребейз** (squash) и отправить результат в удалённый репозиторий.

**Ключевая задача:** Превратить два коммита (`Add Data.cs` и `change data type`) в один чистый коммит `Add Data.cs with final content` перед отправкой на сервер.

---

## Технологии

- **Git** (командная строка)
- **Visual Studio** (Team Explorer / Git Changes)
- **GitHub** (удалённый репозиторий)

---

## Структура репозитория

```
DataProject/
└── Data.cs          # Файл с данными (изменялся в процессе)
```

### Содержимое `Data.cs` (финальное):
```csharp
string data = "Updated";
```

---

## Этапы выполнения

### Часть 1: Работа в командной строке (Git CLI)

1.  **Создание папки и инициализация Git:**
    ```bash
    mkdir DataProject
    cd DataProject
    git init
    ```

2.  **Создание файла и первого коммита (`main`):**
    ```bash
    echo "int data = 0;" > Data.cs
    git add Data.cs
    git commit -m "Add Data.cs"
    ```

3.  **Создание ветки `data-update`:**
    ```bash
    git checkout -b data-update
    ```

4.  **Изменение данных и второй коммит:**
    ```bash
    echo "string data = \"Updated\";" > Data.cs
    git add Data.cs
    git commit -m "change data type from int to string"
    ```

5.  **Проверка истории (должно быть 2 коммита):**
    ```bash
    git log --oneline
    # f1e2d3c (HEAD -> data-update) change data type...
    # a1b2c3d (main) Add Data.cs
    ```

### Часть 2: Интерактивный ребейз (объединение коммитов)

Выполняем команду для объединения двух последних коммитов:
```bash
git rebase -i HEAD~2
```

В открывшемся редакторе (Vim/Nano/VS Code):
1.  **Меняем вторую строку:**
    ```
    pick a1b2c3d Add Data.cs
    squash f1e2d3c change data type from int to string   # Меняем pick на squash
    ```
2.  **Сохраняем и закрываем** (`:wq` для Vim, `Ctrl+X` для Nano).
3.  **Редактируем сообщение нового коммита:**
    ```
    Add Data.cs with final content

    - Initial: int data = 0;
    - Updated: string data = "Updated";
    ```
4.  **Сохраняем.**

**Результат:**
```bash
git log --oneline
# g3h4i5j (HEAD -> data-update) Add Data.cs with final content
```

> **Готово!** В ветке `data-update` теперь один коммит вместо двух.

### Часть 3: Отправка в удалённый репозиторий

#### Способ А: Командная строка
```bash
git remote add origin https://github.com/user/data.git
git push -u origin data-update
```

#### Способ Б: Visual Studio (без команд)

1.  **Открыть проект:**
    - `Файл → Открыть → Проект/Решение` → выбрать папку `DataProject`
2.  **Подключить Git:**
    - `Вид → Team Explorer` (Ctrl + 0, E)
    - `Домашняя → Синхронизация → Опубликовать`
    - Ввести URL репозитория → `Опубликовать`
3.  **Отправить ветку:**
    - В `Team Explorer` → `Синхронизация`
    - Нажать `Отправить (Push)` для ветки `data-update`

**Альтернатива (VS 2022+):**
- `Вид → Git Changes` (Ctrl + 0, G)
- Нажать кнопку `Push` (стрелка вверх) рядом с веткой `data-update`

---

## Результат работы

### В локальном репозитории:
```
$ git log --oneline
b2c3d4e (HEAD -> data-update) Add Data.cs with final content
```

### В удалённом репозитории (GitHub):
- Ветка `data-update` содержит **один** коммит
- История чистая, без промежуточного изменения типа данных

### Содержимое файла:
```csharp
string data = "Updated";
```

---

## Возможные проблемы и решения

| Проблема | Решение |
| :--- | :--- |
| **Конфликт при ребейзе** | `git rebase --abort` → повторить попытку, проверив изменения |
| **Закрылся редактор Vim** | Нажми `Esc`, затем введи `:wq` и Enter |
| **Visual Studio не видит ветку** | Нажми `Fetch` в `Git Changes` |
| **Ошибка "failed to push"** | Убедись, что добавлен remote: `git remote -v` |

---

## Проверочный чек-лист

- [x] Репозиторий `DataProject` инициализирован
- [x] Файл `Data.cs` создан и закоммичен в `main`
- [x] Создана ветка `data-update`
- [x] В `data-update` файл изменён и закоммичен
- [x] Выполнен `git rebase -i HEAD~2` с заменой `pick` на `squash`
- [x] Два коммита объединены в один
- [x] Ветка отправлена в удалённый репозиторий (CLI или VS)

---

## Дополнительная информация

- **Интерактивный ребейз** используется для очистки истории перед публикацией.
- **Visual Studio** поддерживает ребейз через графический интерфейс: `Git → Manage Branches → Rebase`.
- `squash` объединяет коммиты, сохраняя их изменения в одном.

---

## Автор

Решение выполнено в рамках учебного задания по работе с Git и Visual Studio.
```
