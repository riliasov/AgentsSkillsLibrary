# AgentsSkillsLibrary

**Global Knowledge Base** для AI-агентов, работающих в проектах solo-разработчика.

## Назначение

Эта библиотека содержит набор skills, agents, commands и best practices, которые автоматически загружаются через симлинк `.AgentsSkillsLibrary` в проектах.

## Структура

### 📋 Core (Читать первым)
- [00_AGENTS_FIRST.md](00_AGENTS_FIRST.md) — Entry point для AI-агентов
- [01_INDEX.md](01_INDEX.md) — Индекс всех документов
- [02_SAFE_AND_PERMISSIONS.md](02_SAFE_AND_PERMISSIONS.md) — Правила безопасности

### 🤖 Agents (Специализированные роли)
- `agent-orchestrator.md` — Координатор сложных задач
- `agent-refactorer.md` — Эксперт по чистому коду
- `agent-debugger.md` — Систематический анализ багов
- `agent-code-reviewer.md` — Контроль качества
- `agent-test-architect.md` — Дизайн тестов
- `agent-docs-writer.md` — Технический писатель
- `agent-security-auditor.md` — Аудит безопасности

### 🧠 Skills (Области знаний)
- `skill-project-analysis.md` — Методология анализа кодовой базы
- `skill-verification.md` — Протокол самопроверки
- `skill-postgresql.md` — Best practices для Supabase & Postgres
- `skill-telegram-bot.md` — Разработка Telegram ботов
- `skill-google-services.md` — Google Sheets, Apps Script
- `skill-etl-pipeline.md` — ETL и обработка данных
- `skill-architecture-patterns.md` — Паттерны проектирования
- `skill-api-design.md` — Дизайн API
- `skill-git-workflow.md` — Git conventions
- `skill-performance-optimization.md` — Оптимизация производительности
- `skill-testing-strategy.md` — Стратегии тестирования
- `skill-dashboard-design.md` — Дизайн дашбордов

### ⚡ Commands (Стили работы)
- `command-architect.md` — Design-first подход
- `command-rapid.md` — Быстрая разработка
- `command-workflow.md` — Управление workflows
- `command-mentor.md` — Обучающий подход
- `command-review.md` — Строгий peer review
- `command-dashboard-rapid.md` — Быстрая разработка дашбордов

### 📚 References
- `reference-visualization-libs.md` — Справочник по библиотекам визуализации

## Установка

### В новом проекте

```bash
cd /path/to/your/project
ln -s ~/Developer/AgentsSkillsLibrary .AgentsSkillsLibrary
```

### Проверка

```bash
ls -la | grep AgentsSkillsLibrary
# Должен показать симлинк
```

## Использование

AI-агент автоматически обнаружит библиотеку при первом запуске и:
1. Прочитает [00_AGENTS_FIRST.md](00_AGENTS_FIRST.md)
2. Изучит [02_SAFE_AND_PERMISSIONS.md](02_SAFE_AND_PERMISSIONS.md)
3. Выберет подходящий agent/skill/command для задачи

## Философия

- **Единый источник истины** — все изменения делаются здесь
- **Propagation через симлинки** — обновления попадают во все проекты
- **Solo developer first** — оптимизация для одиночной разработки
- **Практичность** — только проверенные паттерны

## Версия

**1.0.0** (2026-01-04)

## Автор

[riliasov](https://github.com/riliasov)

## Лицензия

MIT
