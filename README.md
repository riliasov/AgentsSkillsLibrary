# Agents Skills Library

Этот репозиторий содержит базу знаний и инструкции для AI-агентов.

## Структура
- `Agent_skills/` — основная папка со скиллами, ролями и командами.
- `README.md` — этот файл.
- `CHANGELOG.md` — история изменений структуры и скиллов.

## Использование в проектах
Для подключения библиотеки к проекту используйте симлинк:

```bash
mkdir -p .agent && ln -s ~/Developer/AgentsSkillsLibrary/Agent_skills .agent/skills
```

Это позволит агентам находить инструкции по пути `.agent/skills/00_AGENTS_FIRST.md`.
