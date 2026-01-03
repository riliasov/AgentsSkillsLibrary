# Changelog

All notable changes to AgentsSkillsLibrary will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.1] - 2026-01-04

### Fixed
- **CRITICAL**: Added validation for `// turbo` annotations in workflows to prevent execution of dangerous commands without confirmation
- **CRITICAL**: Lock files policy clarified - automatic regeneration via package managers is now allowed
- Added decision tree in 00_AGENTS_FIRST.md to eliminate ambiguity when choosing between architect and rapid modes

### Security
- `// turbo` now validates commands against the dangerous commands list from 02_SAFE_AND_PERMISSIONS.md
- Prevents auto-execution of `rm`, `git push --force`, `DROP TABLE`, and other destructive commands even with `// turbo` annotation

### Changed
- Updated 02_SAFE_AND_PERMISSIONS.md to explicitly allow lock file regeneration through `npm install`, `yarn install`, etc.
- Updated 00_AGENTS_FIRST.md with comprehensive decision tree for mode selection

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
- See audit_report.md for detailed audit findings
- Medium priority fixes pending: coverage thresholds, testing requirements clarification
- Low priority improvements: error-handling skill, security-checklist skill, migration command

### Security
- Implemented dangerous commands list
- Secret detection patterns defined
- File protection rules established
