# Universal Cursor Rules

Глобальный пакет правил Cursor: process, orchestration, quality gates, documentation workflow.

**Project rules в репозиториях — только стек и домен.** См. `rules/global/project-rules-scope.mdc`.

## Слои контекста

| Слой | Где | Содержание |
|------|-----|------------|
| User Rules | Cursor Settings → Rules | git, PR, стиль |
| **Global** | `~/.cursor/rules/` ← этот репо | orchestrator, intent routing, DoD, docs, gates |
| **Project** | `<repo>/.cursor/rules/` | **только стек + домен** + `*.local.mdc` |
| Skills | `~/.cursor/skills/` или `<repo>/.cursor/skills/` | по задаче |

## Always-on ядро (~6 правил)

- `cursor-orchestrator.mdc`
- `project-rules-scope.mdc`
- `task-intent-routing.mdc`
- `token-economy.mdc`
- `documentation-first.mdc`
- `definition-of-done-gates.mdc`

Остальное — по интенту через `@.cursor/rules/…` (см. `task-intent-routing.mdc`).

## Установка

1. Скачать репо или `git clone https://github.com/alfarius42/universal_cursor_rules`.
2. Скопировать **`rules/global/*.mdc`** → **`~/.cursor/rules/`**:
   - Windows: `C:\Users\<username>\.cursor\rules\`
   - macOS/Linux: `~/.cursor/rules/`
3. Reload Cursor (**Developer: Reload Window**).

### Новый проект

1. Global уже в `~/.cursor/rules/` — **не** копировать весь pack в project.
2. Создать `<repo>/.cursor/rules/` с минимумом:
   - stack rule (React / backend / vanilla — по факту);
   - domain rules или skills;
   - `*.local.mdc` — пути docs, CI-команды, high-risk paths.

## Содержимое (`rules/global/`)

27 универсальных правил + `project-rules-scope.mdc`:

- **Orchestration:** orchestrator, intent routing, project scope
- **Docs & context:** documentation-first, token-economy, tech-stack
- **Quality:** DoD, lint, testing, code-quality, code-cleanliness, ci-cd
- **Risk:** risk-scoring, high-risk-review-packet, anti-hallucination
- **Architecture:** architecture-gates, modular-monolith-boundaries, architecture-decision-log
- **API/DB:** api-contract-gate, deprecation, migrations
- **Performance:** algorithm-complexity, highload-io-memory, highload-resilience-deps
- **Process:** project-conventions, project-playbooks, dev-server, secrets

Личные правила (`ssh-keys-inventory`, `ponytail` и т.п.) в пакет **не входят**.

## CI (GitHub)

`.github/workflows/` — проверки при push в этот репо (path safety, route integrity). На локальный Cursor не влияют.

## Обновление

`git pull` в clone → снова скопировать `rules/global/*.mdc` в `~/.cursor/rules/`, заменив файлы.
