---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - git
  - GitHub
note type: Informational Note
---
**GitHub Actions** — это платформа для автоматизации CI/CD-процессов, которая позволяет запускать сборку, тестирование и деплой проекта прямо из репозитория на GitHub. Основная идея — автоматизировать задачи (workflow) при возникновении событий, вроде *push*, *pull request* или *по расписанию*.
### Основные компоненты

- **Workflow** — конфигурационный файл (YAML) в директории` .github/workflows,` описывающий автоматизированную последовательность задач, которые выполняются при наступлении определённых событий.
- **Job** — набор шагов (steps), которые выполняются на отдельном runner'е (виртуальной машине или container’е).
- **Step** — отдельная команда или часть сценария, часто это запуск action (готовый или кастомный скрипт).

### Как добавить GitHub Actions в свой проект

1. Создай директорию` .github/workflows` в корне репозитория.
2. Добавь туда файл workflow, например` ci.yml` (или создай workflow через вкладку Actions на GitHub).
3. Закоммить файл и запушить изменения — после этого workflow начнёт автоматически запускаться при каждом событии, которое ты указал (например, push в main).
4. Более сложные сценарии включают запуск тестов, загрузку артефактов, деплой и работу с секретами для передачи токенов или ключей.

*Пример* простого workflow для проверки кода при push:
  ```
   name: CI
   on: [push]
   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v4
         - name: Run tests
           run: echo "Running tests!"
```

**Actions can be done with**:
- Docker containers
- JS actions (more compatible and fast)
- Composite actions (multiple workflows)

**Pre-built GitHub actions**:
These are basically templates of some tasks, in order to specify the version the `@v4` should be added (there can be any number instead of 4).
- `actions/checkout` - clones repo's code to workflow runner 
- `actions/cache` - Caches dependencies and build outputs
- `actions/setup-java` - sets up java dev kit

**Jobs** can have different names, which are actually their IDs:
```yaml
jobs:
	test:                 # Job Id
		name: Run test    # Job name 
```