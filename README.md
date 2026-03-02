# HR Onboarding Hub (1С) — MVP (курс «Архитектор 1С»)

MVP-система управления **онбордингом/оффбордингом** с интеграцией через **RabbitMQ**:
- HR создаёт заявку на онбординг
- система автоматически формирует этапы
- этапы отправляют команды через RMQ
- ответы RMQ переводят этапы в “Выполнено/Ошибка”
- есть контроль **SLA/просрочек**
- покрытие тестами: **Yaxunit** + **Vanessa Automation**

> Репозиторий инициализирован шаблоном **Vanessa Bootstrap**.

---

## Быстрый старт для проверяющего (30 секунд)

### 1) Артефакты для сдачи (всё ключевое тут)
- **BPMN (процесс)**: `doc/bpmn/BPMN.png`
- **C4 (архитектура)**:
  - Картинки: `doc/c4/C4_Context.png`, `doc/c4/C4_Container.png`
  - Исходники: `doc/c4/*.puml`
- **ER (модель данных)**: `doc/er/ER.png` (или `doc/er/ER.pdf`)
- **UI (прототипы форм)**: `doc/ui/UI_Prototype.png` (или 2 файла по формам)
- **Интеграция RabbitMQ (контракт)**: `doc/integration/rmq.md`  
  Примеры JSON: `doc/integration/examples/`
- **Тесты**:
  - Yaxunit: `tests/yaxunit/`
  - Vanessa Automation: `tests/vanessa/`
  - План тестирования (docx): `tests/vanessa/VA_TestPlan.docx`
- **Презентация защиты**: `presentation/HR_Onboarding_Hub_MVP.pptx` (или PDF)

---

## Состав MVP (коротко)

### Роли
- **HR-специалист** — создаёт заявки, контролирует выполнение, повторяет отправку этапов при ошибках
- **ИТ-исполнитель (эмулятор/внешняя система)** — принимает команды из RMQ и возвращает ответы

### Бизнес-процесс
См. BPMN: `doc/bpmn/BPMN.png`

### Архитектура (C4)
См. `doc/c4/`

### Данные (ER)
См. `doc/er/`

---

## Репозиторий (структура)

Ключевые каталоги:
- `src/` — исходники/конфигурация (БСП/демо база/расширение)
- `doc/` — артефакты сдачи (BPMN/C4/ER/UI/Integration/Architecture decisions)
- `tests/` — тесты (Yaxunit + Vanessa)
- `features/` — сценарии (если используются в вашем bootstrap)
- `presentation/` — презентация защиты
- `.gitlab-ci.yml` — CI: проверка структуры + публикация артефактов + уведомление YouTrack

---

## Интеграция RabbitMQ (кратко)

Очереди:
- команды: `hr.onboarding.commands`
- ответы: `hr.onboarding.replies`

Связка команда ↔ ответ:
- `correlation_id` — UUID строки

Детали и примеры: `doc/integration/rmq.md`

---

## Тестирование

- Юнит-тесты: `tests/yaxunit/`
- Сценарный тест: `tests/vanessa/`
- План сценарного тестирования: `tests/vanessa/VA_TestPlan.docx`

---

## Решения по архитектуре (ADR)
- `doc/architecture/decisions.md`

---

## Как запустить (минимально)
> Запуск зависит от окружения 1С и выбранного способа прогона тестов (локально/CI).
См. инструкции в `tests/` и скрипты bootstrap (`*.cmd`, `*.sh`), если они используются в проекте.