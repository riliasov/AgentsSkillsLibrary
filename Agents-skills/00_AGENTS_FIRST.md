---
name: onboarding
description: Primary entry point for AI agents. Defines initial steps and role selection.
---

# Onboarding (Agents First)

Welcome! If you are reading this, the **Global Skills Library** is active in this project. This is your primary resource for maintaining engineering standards.

## 🚀 Initial Steps
1. **Explore the Index**: Read [01_INDEX.md](./01_INDEX.md) to understand available tools.
2. **Review Safety Rules**: Read [02_SAFE_AND_PERMISSIONS.md](./02_SAFE_AND_PERMISSIONS.md) before executing commands.
3. **Adopt a Role**: Choose a specialist agent from the root directory based on the task (bug, feature, refactor).
4. **Choose a Style**: Unless specified otherwise, use `command-architect.md` for planning or `command-rapid.md` for simple fixes.

## 📌 Key Guidelines
- **Always Analyze**: Consult `skill-project-analysis.md` when entering a new codebase.
- **Git Perfection**: Use `skill-git-workflow.md` for all commits.
- **Clean Code**: Propose refactoring based on `agent-refactorer.md` if tech debt is spotted.
- **DB Expertise**: Consult `skill-postgresql.md` for any database-related work.

## 🎯 Выбор режима работы (Decision Tree)

| Сценарий | Режим | Обоснование |
|----------|-------|-------------|
| Новая фича (≥ 3 файлов) | `command-architect` | Дизайн сначала, код потом |
| Новая архитектура | `command-architect` + `skill-architecture-patterns` | Требуется анализ trade-offs |
| Багфикс (1-2 файла) | `command-rapid` | Быстрое решение, минимум накладных расходов |
| Рефакторинг | `command-architect` + `agent-refactorer` | Планирование изменений, затем рефакторинг |
| Security аудит | `agent-security-auditor` | Специализированная роль |
| Написание тестов | `agent-test-architect` | Дизайн тестовой стратегии |
| Code review | `agent-code-reviewer` + `command-review` | Систематический анализ |
| Документация | `command-rapid` + `agent-docs-writer` | Быстрая генерация, минимум церемоний |
| Dashboard/Аналитика | `command-dashboard-rapid` | Специализированный workflow |
| Отладка сложных багов | `agent-debugger` | Систематический root cause анализ |

**По умолчанию:** Если не уверен — используй `command-architect` для безопасности.

## 🔄 Library Updates
This repository (`~/Developer/AgentsSkillsLibrary`) is the "source of truth". To use it in projects, link the inner folder:
`ln -s ~/Developer/AgentsSkillsLibrary/Agents-skills .AgentsSkillsLibrary`

