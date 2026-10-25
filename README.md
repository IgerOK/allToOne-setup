# AllToOne — engine/config (bootstrap-репо)

**Что это.** Переиспользуемый «двигатель» протокола AllToOne для любой машины. Внутри:
- `AGENTS.md` — протокол + L1/L2 override + «Цикл развёртки» (читает любой агент автоматически);
- `context/` — **пустой scaffold** (state.json, decisions-active.md, open-questions.md);
- `handoff.md` — пустой шаблон пакета;
- `.gitignore` + `LICENSE` + этот README.

**Память конкретного проекта сюда НЕ входит** — это по модели DECO. Память = per-project L2-пакет, который **переносит пользователь** (git clone проекта / копирование L2-файлов). Bootstrap даёт только «движок».

---

## Как настроить машину (одноразово)

1. **Клонировать bootstrap** (разовая «настройка»):
   ```
   git clone <все-покед-все-репо allToOne-setup> allToOne-setup
   ```
   Затем любой агент, открывший папку, сам читает `AGENTS.md` и знает протокол.

2. **(Опционально) Skill для авто pack/unpack** в `~/.agnes/skills` — чтобы агент сам собирал/разворачивал L2 без явных команд. Не требуется, но удобнее.

3. **Память проекта на эту машину:** для каждого проекта — `git clone <проект>` (там свой `AGENTS.md` + `context/` + `handoff.md`). Или просто скопировать L2-файлы (`context/`, `handoff.md`, `AGENTS.md`) в папку проекта.

---

## Первый ход на новой машине

Открыв папку проекта с `AGENTS.md`, агент (или скажите ему явно):
> «Прочитай `handoff.md` + `context/state.json`, сделай health-check, предложи начать.»

Агент восстановит контекст (L2 из git, не из `.agnes/` — он не источник cross-machine). После вашего «идём» — старт.

---

## Модель DECO (двухслойный перенос)

| Слой | Где | Кто переносит |
|------|-----|----------------|
| **Движок** (bootstrap) | `AGENTS.md` + пустой `context/` scaffold + README | этот репо (git clone на каждую машину, разово) |
| **Память проекта** (L2) | заполненный `context/*` + `handoff.md` + `AGENTS.md` проекта | пользователь (git clone проекта / копирование L2-файлов) |

Л2 — source of truth для восстановления (git, не `.agnes/`). Л1 (`.agnes/session-state.json`) — только локальная записка, в перенос не входит.

---

## Структура

```
AGENTS.md             ← протокол + L1/L2 override + чек-лист deploy (движок)
README.md             ← этот файл (как настроить машину)
LICENSE               ← MIT
.gitignore            ← .agnes/ (L1) не в git
context/              ← ПУСТОЙ scaffold (state.json, decisions, open-questions)
handoff.md            ← пустой шаблон пакета
```

> Bootstrap-репо — сейчас **локально**. Публикация на GitHub — по явной команде пользователя.
