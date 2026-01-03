# Changelog

All notable changes to AgentsSkillsLibrary will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-01-04

### Added
- Initial release of AgentsSkillsLibrary
- Core documentation: 00_AGENTS_FIRST.md, 01_INDEX.md, 02_SAFE_AND_PERMISSIONS.md
- 7 specialized agents (orchestrator, refactorer, debugger, code-reviewer, test-architect, docs-writer, security-auditor)
- 10 skill documents covering PostgreSQL, Telegram, Google Services, ETL, Architecture, API design, Git, Performance, Testing, Dashboard design
- 6 command modes (architect, rapid, workflow, mentor, review, dashboard-rapid)
- Reference documentation for visualization libraries
- Git repository initialized with remote: https://github.com/riliasov/AgentsSkillsLibrary.git

### Known Issues
- See [audit_report.md](../../../.gemini/antigravity/brain/7f7cc06e-199b-42a9-a219-21f19920f48e/audit_report.md) for detailed audit findings
- Priority fixes needed for `// turbo` validation in workflows
- Lock files policy needs clarification
- Decision tree for mode selection should be added

### Security
- Implemented dangerous commands list
- Secret detection patterns defined
- File protection rules established
