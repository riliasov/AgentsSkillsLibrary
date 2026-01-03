---
name: workflow-management
description: Guidelines for creating, using, and proposing workflows with slash commands. Automates repetitive task sequences.
---

# Workflow Management

Workflows — это предопределённые последовательности действий, которые можно быстро запустить через слэш-команды. Это снижает количество промптов и ускоряет выполнение рутинных задач.

## Когда предлагать создание workflow

Предлагай пользователю создать workflow если:
- Обнаружена **повторяющаяся последовательность** команд (≥3 шагов)
- Пользователь просит "сделать то же самое, что в прошлый раз"
- Есть стандартная процедура для проекта (deploy, test, build, setup)

**Примеры кандидатов**:
- Полный цикл деплоя (build → test → push → deploy)
- Setup окружения (venv → install deps → migrate db)
- Генерация отчётов (collect data → process → generate html)

## Формат workflow файлов

Workflows хранятся в `.agent/workflows/` и имеют строгий формат:

```markdown
---
description: [краткое название, например "deploy the application"]
---

[Детальные инструкции по шагам]

1. Первый шаг
   - Описание действия
   - Команда: `example command`

// turbo
2. Второй шаг (безопасный, можно авто-выполнить)
   - Команда: `ls -la`

3. Третий шаг
   - Действие требует подтверждения
```

### Аннотации

- **`// turbo`** над шагом: этот шаг можно выполнить с `SafeToAutoRun: true` (только для `run_command`)
- **`// turbo-all`** в любом месте файла: **все** шаги с `run_command` выполнять автоматически

> [!WARNING]
> Используй `// turbo-all` только для полностью безопасных workflows (например, read-only операции).

## Процесс создания workflow

1. **Обнаружил паттерн** → спроси пользователя: "Это повторяющаяся задача, создать workflow?"
2. **Получил согласие** → создай файл `.agent/workflows/[name].md`
3. **Напиши инструкции**:
   - Используй императивный стиль ("Run X", "Execute Y")
   - Будь максимально конкретным с командами и путями
   - Укажи условия успеха каждого шага
4. **Отметь безопасные шаги** через `// turbo`
5. **Сообщи пользователю**: "Создан workflow `/name`, теперь можешь использовать эту команду"

## Использование workflows

Когда пользователь пишет `/workflow-name`:
1. Прочитай файл `.agent/workflows/workflow-name.md` через `view_file`
2. Следуй инструкциям шаг за шагом
3. Для шагов с `// turbo`: используй `SafeToAutoRun: true`
4. Для остальных: запрашивай подтверждение как обычно

## Пример workflow файла

```markdown
---
description: run full test suite with coverage
---

# Full Test Suite

1. Activate virtual environment
// turbo
2. Run unit tests
   - Command: `pytest tests/unit -v`

// turbo
3. Run integration tests
   - Command: `pytest tests/integration -v`

// turbo
4. Generate coverage report
   - Command: `pytest --cov=src --cov-report=html`

5. Open coverage report in browser
   - Manual action: User should open `htmlcov/index.html`
```

## Best Practices

- **Имя файла**: используй kebab-case (`setup-environment.md`, не `SetupEnvironment.md`)
- **Описание**: краткое, actionable ("deploy to production", не "файл для деплоя")
- **Шаги**: нумерованный список с чёткими командами
- **Turbo осторожно**: помечай только команды из раздела 3 в `02_SAFE_AND_PERMISSIONS.md`
- **Обновляй**: если процесс изменился — обнови workflow
