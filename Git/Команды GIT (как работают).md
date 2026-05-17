## #БАЗОВЫЕ_КОМАНДЫ

#### 1.Git init - инициируем репозиторий локально

```
# Создает пустой Git репозиторий в текущей папке
git init

# Инициализировать в конкретной папке
git init my_project

# Результат:
# Initialized empty Git repository in C:/Users/Анастасия/project/.git/
```

#### 2. Git add - добавляет все сущ. файлы в индекс

```
 Добавить все измененные файлы
git add .

# Добавить конкретный файл
git add index.html

# Добавить все файлы определенной папки
git add src/

# Добавить все .js файлы
git add *.js

# Добавить интерактивно (выбор по частям)
git add -p

```
**Что происходит:** Файлы попадают в staging area (индекс) — подготовку к коммиту.****

#### 3. Git commit  - фиксация изменений

```
# Коммит с сообщением в терминале
git commit

# Коммит с сообщением сразу
git commit -m "Добавил авторизацию"

# Коммит с подробным описанием
git commit -m "Добавил авторизацию" -m "Реализовал через JWT токены"

# Коммит всех файлов без git add
git commit -a -m "Исправил баги"
```

**Что происходит:** Изменения из индекса сохраняются в истории репозитория с уникальным хешем.
#### 4. GIt  remoute add origin - подключение удаленного репозитория

```
# Добавить удаленный репозиторий
git remote add origin https://github.com/твой-логин/имя_репозитория.git

# Проверить подключенные репозитории
git remote -v

# Пример:
git remote add origin https://github.com/anastasia/my-project.git
```

**Что происходит:** Создается связь между локальным и удаленным репозиторием (origin — это псевдоним).

#### 5. Git push - отправка изменений на сервер

```
# Отправить ветку main и установить отслеживание
git push -u origin main

# Отправить без установки отслеживания
git push origin main

# Отправить все ветки
git push --all origin

# Принудительная отправка (осторожно!)
git push -f origin main
```

 **Что происходит** - Ваши локальные коммиты загружаются на GitHub/GitLab. 

#### 6. Git clone - клонирование репозитория 

```
# Клонировать репозиторий
git clone https://github.com/user/repo.git

# Клонировать в конкретную папку
git clone https://github.com/user/repo.git my-folder

# Клонировать конкретную ветку
git clone -b develop https://github.com/user/repo.git

# Клонировать только последнюю версию (без истории)
git clone --depth 1 https://github.com/user/repo.git
```

**Что происходит:** Полностью скачивается репозиторий со всей историей коммитов.

## #РАБОТА_С_ВЕТКАМИ
#### 7. Git branch -  управление ветками

```
# Посмотреть все локальные ветки
git branch

# Посмотреть все ветки (локальные + удаленные)
git branch -a

# Посмотреть удаленные ветки
git branch -r

# Создать новую ветку (без переключения)
git branch feature/login

# Удалить ветку
git branch -d feature/login

# Принудительно удалить
git branch -D feature/login
```

#### 8. Git checkout - переключение веток

```
# Переключиться на существующую ветку
git checkout dev

# Переключиться и создать новую ветку
git checkout -b feature/name

# Создать ветку от конкретной ветки
git checkout -b feature/main dev

# Переключиться на предыдущую ветку
git checkout -

# Переключиться на конкретный коммит (detached HEAD)
git checkout abc1234
```

**Что происходит:** Git заменяет файлы в рабочей папке на версию из указанной ветки.

#### 9. Git pull - получение и слияние 

```
# Скачать и автоматически сделать merge
git pull origin dev

# Скачать изменения с текущей ветки
git pull

# Скачать и сделать rebase вместо merge
git pull --rebase origin main

# Только скачать без слияния (аналог fetch)
git pull --no-commit origin main
```

**Что происходит:**

1. `git fetch` — скачивает изменения с сервера
2. `git merge` — автоматически вливает их в вашу ветку

## #СЛИЯНИЕ_И_ИНТЕГРАЦИЯ

#### 10. Git merge - слияние веток

```
# Влить ветку feature в текущую
git checkout main
git merge feature

# Слияние без создания commit (fast-forward если возможно)
git merge --ff-only feature

# Отменить слияние
git merge --abort

# Посмотреть, что будет при слиянии
git merge --no-commit --no-ff feature
```

Пример

```
# Вы находитесь в ветке main
git merge feature/login
# Результат:
# Merge made by the 'ort' strategy.
# 2 files changed, 15 insertions(+)
```

**Что происходит:** Git объединяет две ветки, создавая новый merge commit (если есть изменения в обеих ветках).

#### 11. Git rebase - перебазирование

```
# Перенести текущую ветку на основную
git checkout feature
git rebase main

# Интерактивный rebase (редактирование истории)
git rebase -i HEAD~3

# Продолжить после разрешения конфликтов
git rebase --continue

# Отменить rebase
git rebase --abort

# Пропустить текущий коммит
git rebase --skip
```

**Визуализация:**
```
о rebase:
      A---B---C main
     /
    D---E---F feature

После git rebase main (в ветке feature):
      A---B---C main
           \
            D'---E'---F' feature
```

**Что происходит:** Git "отрезает" ваши коммиты и применяет их поверх указанной ветки, делая историю линейной.

⚠️ **ВАЖНО:** Не используйте rebase на публичных ветках, которые используют другие разработчики!

#### 12. Git cherry-pick - выборочное применение коммитов

```
# Взять один конкретный коммит
git cherry-pick abc1234

# Взять несколько коммитов
git cherry-pick abc1234 def5678

# Взять диапазон коммитов
git cherry-pick abc1234^..def5678

# Применить без создания коммита
git cherry-pick --no-commit abc1234

# Отменить cherry-pick
git cherry-pick --abort
```

Пример использования

```
# Вы в ветке hotfix, нужно взять коммит из develop
git checkout hotfix
git cherry-pick 5f8a2b1
# Конфликт! Разрешаем его:
# ... редактируем файлы ...
git add .
git cherry-pick --continue
```

**Что происходит:** Git создает новый коммит с теми же изменениями, что и указанный, но с новым хешем и текущей датой.

## PULL REQUEST / MERGE REQUEST

### **Pull Request (GitHub)** и **Merge Request (GitLab)**

Это не команды Git, а функции платформ:

**Как создать PR/MR:**

```
# 1. Создать ветку
git checkout -b feature/new-feature

# 2. Внести изменения и закоммитить
git add .
git commit -m "Добавил новую функцию"

# 3. Отправить на сервер
git push origin feature/new-feature

# 4. На GitHub/GitLab нажать кнопку "New Pull Request"
```

**Что это:** Предложение внести изменения из вашей ветки в основную ветку проекта с возможностью code review.

### ПОЛНЫЙ ПРИМЕР РАБОЧЕГО ПРОЦЕССА

```
# 1. Клонировать проект
git clone https://github.com/company/project.git
cd project

# 2. Создать ветку для своей задачи
git checkout -b feature/payment-system

# 3. Работать над кодом...
# Создаем файлы, редактируем

# 4. Добавить изменения
git add .

# 5. Сделать коммит
git commit -m "Реализовал оплату картой"

# 6. Синхронизироваться с основной веткой
git checkout main
git pull origin main
git checkout feature/payment-system
git rebase main  # или git merge main

# 7. Отправить на сервер
git push origin feature/payment-system

# 8. Создать Pull Request на GitHub
# 9. После approve — влить в main
```

### СРАВНЕНИЕ: merge vs rebase


| Критерии           | merge                              | rebase                             |
| ------------------ | ---------------------------------- | ---------------------------------- |
| История            | Сохраняет всю историю слияний      | Делает историю линейной            |
| Безопасность       | Безопасен, не переписывает историю | Переписывает историю (меняет хеши) |
| Когда использовать | Публичные ветки, командная работа  | Локальные ветки перед merge в main |
| Конфликты          | Решаются один раз                  | Могут возникать на каждом коммите  |

### #Git_command_short

| Task                   | Command                                      |
| ---------------------- | -------------------------------------------- |
| Начать новый проект    | git init                                     |
| Cкачать существующий   | git clone (url)                              |
| Cохранить изменения    | git add . + git commit -m (message)          |
| Отправить на сервер    | git push origin main                         |
| Получить обновление    | gir pull origin main                         |
| Создать ветку          | git checkout -b feature/name                 |
| Переключить ветку      | gjt checkout  (branch - ветка)               |
| Влить ветку            | git merge  (branch - ветка)                  |
| Обновить ветку линейно | git rebase main                              |
| Взять один коммит      | git cherry-pick (hash имя последнего комита) |
