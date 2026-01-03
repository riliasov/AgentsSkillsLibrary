---
name: safety-and-permissions
description: Comprehensive security guidelines, file protection rules, and dangerous command patterns. Read before executing bash or making edits.
---

# Safety Rules & Permissions

This document consolidates all safety mechanisms, file protection rules, and operational constraints extracted from the project's automated hooks.

## 1. File Protection Rules

### 🚫 Blocked Files (Never Edit Automatically)
These files are protected to prevent system failure or data loss. Modification requires explicit user request:
- **Lock Files**: `package-lock.json`, `yarn.lock`, `pnpm-lock.yaml`, `Gemfile.lock`, `poetry.lock`, `Cargo.lock`
  - ⚠️ **Never edit manually** (causes inconsistency)
  - ✅ **Automatic regeneration allowed** via package managers: `npm install`, `yarn install`, `pip install`, etc.
  - ✅ **Changes via dependency updates allowed**: Adding/updating packages through proper package manager commands
- **Sensitive Configs**: `.env`, `.env.local`, `.env.production`
- **Protected Directories**: `**/secrets/*`, `**/credentials/*`
- **Git Internals**: `.git/*`

### ⚠️ Warning Files (Proceed with Caution)
Modifying these may affect CI/CD or infrastructure:
- `.github/workflows/*`
- `docker-compose.yml`, `Dockerfile`
- `**/production/*`

---

## 2. Dangerous Commands (FORBIDDEN automatically)
**Always require explicit confirmation before execution:**

| Command | Risk |
|---------|------|
| `rm`, `rm -rf` | Deletion of files/directories |
| `git push --force` | Overwriting remote history (dangerous for collaboration) |
| `git reset --hard` | Permanent loss of uncommitted changes |
| `DROP DATABASE/TABLE` | Irreversible data loss |
| `TRUNCATE TABLE` | Deletion of all table rows |

> [!CAUTION]
> **Any command NOT listed in Section 3 "Allowed Commands" requires confirmation.**

---

## 3. Allowed Commands (automatic execution)
The following commands are considered safe and can be executed with `SafeToAutoRun: true`:

- **Reading**: `ls`, `cat`, `grep`, `find`, `tree`, `head`, `tail`, `wc`
- **Git (information)**: `git status`, `git log`, `git diff`, `git branch`, `git show`
- **Quality checks**: `npm test`, `pytest`, `ruff check`, `mypy`, `eslint`
- **Dev build**: `npm run dev`, `npm install`, `pip install -r requirements.txt`, `python -m venv`

---

## 4. Secret Detection (Pre-commit/Pre-edit)
Do not write or commit strings matching these profiles:

| Secret Type | Detection Pattern |
|-------------|-------------------|
| **API Keys** | `api_key`, `apikey` followed by 20+ chars |
| **Tokens** | `bearer`, `ghp_` (GitHub), `sk-` (OpenAI/Anthropic) |
| **Access Keys** | `aws_access_key_id`, `aws_secret_access_key` |
| **Credentials** | `password`, `passwd`, `pwd` followed by values |
| **Private Keys**| `-----BEGIN PRIVATE KEY-----` |

---

## 5. Environment & Tooling
Before starting complex tasks, ensure the following are available:
- **Node.js**: Required for `npm` and frontend tasks.
- **Python 3**: Required for internal scripts and data tasks.
- **Git**: Required for version control and commit history.
- **Prettier/Ruff/Black**: Maintain consistent code style by running formatters after edits.

---

## 6. Agent Hints
Select the right specialist agent based on the prompt keywords:
- `bug`, `error`, `crash` → **agent-debugger**
- `review`, `pull request` → **agent-code-reviewer**
- `test`, `coverage` → **agent-test-architect**
- `security`, `auth`, `vulnerab` → **agent-security-auditor**
- `refactor`, `clean`, `simplify` → **agent-refactorer**
- `document`, `readme` → **agent-docs-writer**

---

## 7. Permissions Matrix

| Permission | Status | Details |
|------------|--------|---------|
| **Read** | Allowed | Reading project files |
| **Write/Edit**| Allowed | Code editing |
| **Bash (Safe)** | Allowed | Only commands from Section 3 |
| **Bash (Destructive)** | Forbidden | Commands from Section 2 require confirmation |
| **Network** | Allowed | Reading documentation |
