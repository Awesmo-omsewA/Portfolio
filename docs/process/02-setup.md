# Настройка MkDocs

### Шаги:

 1. Установка MkDocs и темы Material.
 2. Инициализация проекта.
 3. Настройка конфигурации.
 4. Первый локальный запуск.

---

## Установка

Установил MkDocs и тему Material:

```bash
pip install mkdocs mkdocs-material
```
> команда в терминале

## Инициализация

Создал проект в папке `docs/`:

```bash
mkdocs new docs
```
> команда в терминале

После этого появились `docs/index.md` и `mkdocs.yml`. Я перенёс `mkdocs.yml` в корень репозитория.

## Конфигурация

В `mkdocs.yml` указал тему:

```yaml
theme:
  name: material
```

Добавил навигацию:

```yaml
nav:
  - Главная: index.md
  - Как я создавал:
      - Введение: process/index.md
      - Выбор инструментов: process/01-tools.md
      - Настройка MkDocs: process/02-setup.md
      - Интеграция Mermaid: process/03-mermaid.md
      - Интеграция Swagger UI: process/04-swagger.md
      - Настройка CI/CD: process/05-cicd.md
  - Проекты:
      - Проект 1: projects/project-1/index.md
      - Проект 2: projects/project-2/index.md
  - Обо мне: about.md
```
> Я добавил структуру навигации сразу, чтобы видеть, как будет выглядеть сайт. 

## Первый запуск

```bash
mkdocs serve
```
> команда в терминале

Открыл браузер по адресу `http://127.0.0.1:8000/` — сайт заработал.

> Остановить сервер - ctrl + c

**Дальше** — [Интеграция Mermaid](03-mermaid.md)