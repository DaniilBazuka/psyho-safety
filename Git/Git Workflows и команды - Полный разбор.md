### 1️⃣ **GitFlow** (классическая модель)

**Для чего:** Большие проекты с релизами и долгосрочной разработкой.

main (master)
  └── develop
        ├── feature/* (новые функции)
        ├── release/* (подготовка релиза)
        └── hotfix/* (срочные исправления)


## **Как работает:**

- ==`main`== — стабильная версия (только релизы)
- ==`develop`==— ветка разработки
- ==`feature/новая-функция`== — создание фичи → merge в develop
- ==`release/1.0`==— подготовка к релизу → merge в main и develop
- ==`hotfix/исправление`== — срочный фикс → merge в main и develop

## Пример 

bash
	1. git checkout -b feature/login
	2. ... работа над функцией
	3. git checkout develop
	4. git merge feature/login

### 2️⃣ **GitHub Flow** (упрощенная модель)

**Для чего:** Веб-приложения, непрерывное развертывание (CI/CD).

#### Принцип работы


```main (всегда рабочая!)
  └── feature-branch → Pull Request → merge в main
```

**Правила:**

1. Всегда работаем от `main`
2. Создаем ветку под задачу: `git checkout -b new-feature`
3. Пушим на GitHub и создаем **Pull Request**
4. После code review → merge в `main`
5. `main` всегда можно выкатить на продакшн

#### Пример

bash 
```
1. git checkout main
2. git pull
3. git checkout -b add-payment
4. # ... работа, коммиты
5. git push origin add-payment
6. # Создаем PR на GitHub → merge
```

### 3️⃣ **GitLab Flow** (гибридная модель)

**Для чего:** Комбинация GitFlow и GitHub Flow.

#### Структура 
```
	main
		feature/*
			merge в main
				environment/* (starting, production)
```
#### Особенности

- Есть `main` (как в GitHub Flow)
- Есть `production` и `staging` ветки
- Feature-ветки → merge в main → deploy в staging → production

### 4️⃣ **Trunk-Based Development**

**Для чего:** Экстремально частые релизы, DevOps.

Принцип:
```
trunk (main) ← все коммитят сюда!
  └── короткие feature-ветки (максимум 1-2 дня)
```

**Правила:**

- Никаких долгих веток
- Фичи включаются через **feature flags**
- Несколько коммитов в день в `main`
- Непрерывная интеграция