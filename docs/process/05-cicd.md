# Настройка CI/CD

**CI/CD** (*Continuous Integration / Continuous Deployment*) — это автоматическая сборка и публикация сайта при каждом обновлении кода в репозитории.

Этот подход позволяет не загружать сайт вручную: достаточно выполнить `git push`, и через несколько минут обновлённая версия появляется на GitHub Pages.

---

## Настройка GitHub Actions

В папке `.github/workflows/` я создал файл `deploy.yml`.

Он описывает, что должно происходить при пуше в ветку `main`:

1. Установить Python и MkDocs.
2. Установить тему Material и плагин Swagger UI.
3. Собрать сайт командой `mkdocs build`.
4. Загрузить собранный сайт как артефакт.
5. Опубликовать его на GitHub Pages.

---

## Содержимое `docs.yml`

```yaml
name: Deploy MkDocs to GitHub Pages

on:
  push:
    branches: [ "main" ]  
  workflow_dispatch:     

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.12'

      - name: Install dependencies
        run: |
          pip install mkdocs
          pip install mkdocs-material
          pip install mkdocs-swagger-ui-tag

      - name: Build the site
        run: mkdocs build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./site

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

---

## Результат

Теперь сайт собирается и публикуется автоматически при каждом пуше в main. Мне не нужно вручную запускать сборку или загружать файлы на сервер — всё делает GitHub Actions.